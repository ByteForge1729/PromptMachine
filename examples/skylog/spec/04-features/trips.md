# Trip weekends

**Tier:** v0 · **Sources:** D1, D8, D9, A10, A14, A15

## Behaviour
1. Ranks every (dark site, weekend) pair for the next 4 weekends by weekend score, which
   discounts moonlit hours.
2. Each row: site, dates, Moon phase, agreement, one tap to hourly numbers.
3. "Share to WhatsApp" copies a plain summary for the coordinators to post. Nothing else:
   trips are organised in the club group. (D8)
4. Every Monday the ranking is saved as a snapshot for the success check. (A15)

## Acceptance criteria
- [ ] Given two weekends with identical cloud forecasts, one at full Moon and one at new
      Moon, then the new-Moon weekend ranks higher, and both show the same agreement ("3 of 3 forecasts agree it's mostly clear") with the full-Moon one marked "bright Moon".
- [ ] Given a Monday, then a snapshot for all sites and 4 weekends exists by 06:00 IST.
