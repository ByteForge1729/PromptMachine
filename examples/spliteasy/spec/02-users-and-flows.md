# Users and flows

## Who

Priya is back from a Goa trip where she paid for the hotel. Four friends owe her, one of
them (Amit) will never install another app. She opens SplitEasy in the cab to log it
before anyone forgets, then again a week later to see who has paid. (A6)

## Flows

Names used throughout: **Priya** (group creator, paid), **Rahul** (member, owes),
**Amit** (ghost).

### F-1 Create a group and bring friends in
1. Priya taps "New group", enters a name, picks the currency (default INR). (D3)
2. She adds members two ways:
   - **Invite:** she taps "Invite", SplitEasy opens the share sheet with a WhatsApp-ready
     link. Rahul taps it; with the app installed he lands in the group, without it he
     sees a web page with an install button and a join code. (A38)
   - **Ghost:** she types "Amit". Amit exists in the group with no account. (D2)
3. After creating her first group, Priya is asked for notification permission. (A16)
   - Denied: the app works; a small banner in the group says reminders are off.

### F-2 Add an expense
1. Priya opens the group, taps "Add expense".
2. Enters amount ₹4,000, description "Hotel", paid by Priya (default: herself), split
   equally among selected members (default: everyone). (A7)
3. Taps Save. Done in under 10 seconds.
4. Online: the balance updates for everyone within 5 seconds. Offline: the expense shows
   "not synced yet" and uploads automatically on reconnect. (D15)
5. Everyone included gets a notification. (A14)
6. "Undo" shows for 10 seconds. (A12)

### F-3 Rahul pays Priya back
1. Rahul opens the group and sees "You owe Priya ₹1,000" and a Pay button. (A28)
2. Taps Pay. SplitEasy opens GPay with Priya's UPI ID and ₹1,000 filled in. (D1, A29)
   - Priya has no UPI ID saved: button reads "Ask Priya for her UPI ID" and sends her a
     push notification. (A29)
   - Group is not in INR: no Pay button; Rahul pays however he likes and taps "I paid". (D3)
   - GPay missing or fails: Rahul returns and can still tap "I paid" manually.
3. Returning to SplitEasy, Rahul confirms the amount and taps "I paid". He can change the
   amount for a partial payment. (A33)
4. Rahul's balance now reads "₹1,000 · you say paid, awaiting Priya". (D5)

### F-4 Priya confirms or rejects
Timeline, measured on the server clock from when the server receives "I paid" (A3, A39):

| When | What happens |
|---|---|
| Any time | Priya taps "Got it": final at once |
| Any time before day 30 | Priya taps "Not paid": rejected; Rahul's debt and monster come back; both are notified |
| Day 3 | Rahul's monster shrinks and his rank moves (game only); the number still says awaiting (D5) |
| Day 29 | Priya is notified: "Rahul says he paid ₹1,000. This confirms tomorrow." (A15) |
| Day 30 | Final. The balance number updates. |

If the receiver is a ghost, the group creator sees the "Got it" and "Not paid" buttons for
them. (A30)

### F-5 Amit claims his ghost
1. Any member taps Amit's name → "Send claim link". (D2)
2. WhatsApp opens with a single-use link valid for 14 days. (A37)
3. Amit installs, opens the link (or types the code from the web page), signs in with
   Google, and is asked "Are you Amit in 'Goa trip'?"
4. He becomes a full member with all history. The group is notified "Amit joined". (A37)
   - Link expired or used: "Ask your group for a new link."

### F-6 Remind a ghost
1. Priya taps "Remind Amit".
2. SplitEasy renders a card: Amit's current character, the amount, the group, and the
   claim link. (D11)
3. The share sheet opens with WhatsApp preselected. Priya sends it.

### F-7 Open the app with no signal
1. The group shows the last balances saved on the phone, labelled "as of 2 h ago". (D15)
2. Adding expenses works; each shows "not synced yet".
3. Pay, "Got it" and "Not paid" are disabled with "Needs internet". "I paid" is allowed
   and queued. (A39)
