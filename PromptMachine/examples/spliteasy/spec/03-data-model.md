# Data model

Money is always an **integer in minor units** (paise for INR, satang for THB). IDs are
UUIDs. Timestamps are UTC, set by the server. (A4, A34)

## Entities

### User
| Field | Type | Rule |
|---|---|---|
| id | uuid | |
| name | text | from Google account, editable |
| upi_id | text, optional | shown only to members of shared groups, only through the Pay button (A29) |
| created_at | timestamp | |

**Owned by:** the user. **Deletion:** name becomes "Deleted user"; memberships and
expenses stay (A13).

### Group
| Field | Type | Rule |
|---|---|---|
| id | uuid | |
| name | text | 1–40 characters |
| currency | ISO 4217 code | locked once the first expense exists (A34) |
| creator_id | user id | |
| big_debt | integer, minor units | default 50000 (₹500); only the creator may change it; every change written to history (D10, A31) |
| created_at | timestamp | |

### Member
| Field | Type | Rule |
|---|---|---|
| id | uuid | |
| group_id | group id | |
| user_id | user id or null | null means ghost (D2) |
| display_name | text | |
| claim_token_hash | text or null | single-use, expires 14 days after creation (A37) |
| left_at | timestamp or null | only allowed when ledger_net = 0 and no open settlements (A13) |

### Expense
| Field | Type | Rule |
|---|---|---|
| id | uuid | created on the phone, so offline creation works |
| group_id | group id | |
| description | text | 1–60 characters |
| amount | integer | > 0 |
| paid_by | member id | |
| shares | list of {member_id, amount} | sum must equal amount (see Split) |
| created_by | member id | only this member or the group creator may edit or delete (A12) |
| created_at, deleted_at | timestamp | soft delete |

### Settlement
| Field | Type | Rule |
|---|---|---|
| id | uuid | |
| group_id | group id | |
| from_member, to_member | member id | |
| amount | integer | > 0, may be less than owed (A33) |
| method | enum: upi, manual | upi only in INR groups (D3) |
| status | enum | see lifecycle |
| received_at | timestamp | server time the claim arrived; all timers start here (A3, A39) |
| decided_by | member id or "auto" | |

**Lifecycle:**
```
claimed ──day 3──▶ provisional ──day 30──▶ final
   │                   │
   ├──"Got it"─────────┴──────────────────▶ final
   └──"Not paid"───────┴──(before final)──▶ rejected
```
Only the receiver may tap "Got it" or "Not paid"; for a ghost receiver, the group creator
(A30). Status never moves backwards.

### HistoryEvent
Append-only record of every expense, edit, delete, settlement change, threshold change and
membership change: actor, type, before, after, time. (A12)

### Balance (derived, written only by the server)
One per member per group: `ledger_net`, `pending_out`, `pending_in`, `game_net`, `tier`,
`anger`, `in_debt_since`, `updated_at`.

### AppConfig
`min_supported_version`: older app versions show a blocking update screen. (A18)

## Invariants

These must each have an automated test.

1. For every group, the sum of `ledger_net` across members is exactly 0.
2. For every group, the sum of `game_net` across members is exactly 0.
3. For every expense, the sum of `shares` equals `amount`.
4. No client can write a Balance, a Settlement status, or a HistoryEvent.
5. A settlement's status never moves backwards.
6. No money field is ever a fraction.
7. Two phones showing the same group and the same `updated_at` show identical numbers.
8. Removing a person's name (account deletion or a ghost's removal request) never changes any balance. (A42, A46)

## Derived values

### Split (A4)
```
equal_split(amount, members, payer):
    base = floor(amount / n)
    remainder = amount - base * n            # 0 .. n-1 paise
    shares = base for each member
    if payer in members: payer.share += remainder
    else: add 1 to the first `remainder` members by join order
```

### Balances
```
ledger_net(m) = Σ expenses paid by m
              - Σ shares of m
              + Σ settlements from m where status = final
              - Σ settlements to m   where status = final

game_net(m)   = ledger_net(m)
              + Σ settlements from m where status = provisional
              - Σ settlements to m   where status = provisional

pending_out(m) = Σ settlements from m where status in (claimed, provisional)
```
Displayed number: `ledger_net`, with `pending_out` shown as "awaiting confirmation". (D5)

### Tier (D8, D9, D10, A31)
```
tier(game_net, B):
    if |game_net| < 100: Villager                  # within ₹1
    owed = game_net > 0; x = |game_net|
    if owed:  x >= 2B → Emperor; x >= B → King;    else Prince
    else:     x >= 2B → Dragon;  x >= B → Monster; else Goblin
```

### Anger (D9, A32)
Only for Goblin, Monster, Dragon. `in_debt_since` is set when `game_net` goes below 0
and cleared when it reaches 0 or above.
```
days = now - in_debt_since
days < 7 → calm;  days < 21 → annoyed;  else → furious
```

### Settle-up suggestions (A28)
```
open(m) = ledger_net(m) + pending_out(m) - pending_in(m)   # already-claimed payments excluded
repeat until every open(m) is within ₹1:
    d = member with most negative open
    c = member with most positive open
    suggest d pays c min(|open(d)|, open(c))
```
