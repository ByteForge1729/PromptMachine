# Risks

| Risk | Likelihood | Damage | Mitigation | Status |
|---|---|---|---|---|
| GPay declines app-opened payments to personal UPI IDs | medium (widely reported, not confirmed) | Pay button fails for many users | "I paid" works without the button; test GPay, PhonePe and Paytm on real devices in M3 | open, `[UNVERIFIED]` |
| UPI app returns a fake or missing "success" | high | Debts cleared without payment | The response is ignored; only people confirm (D4) | mitigated |
| Visible ranks embarrass someone | low in close friend groups | People quietly stop opening the app | Monster blames the debt (A26); a per-group "hide ranks" switch is the fallback | **accepted by user** |
| Ghost data: names and debts of people who never agreed to be in the app | medium | Privacy complaint | Store only a name; delete a ghost on request | open |
| AI-generated characters look inconsistent | high | The Arena looks like a collage | Style sheet first, generate against it (06) | mitigated |
| Blaze plan needs a card; a bug loops and runs up cost | low | Unexpected bill | ₹100 budget alert; functions idempotent | mitigated |
| Rounding or sync bug shows a wrong balance | medium | Breaks the must-never rule; trust gone | Invariant tests, server-only computation, property-based tests | mitigated |
| The switch to dev builds slows iteration | medium | Slower testing than Expo Go's QR code | One dev client build, then JS reloads as before | accepted |
| Old app versions still installed | high | Different behaviour across friends | Force-update setting (A18) | mitigated |
| Under-18 users' data stored without parental consent | medium (some first-years are 17) | Breach of DPDP Rules once in force; complaint or takedown | None, by choice (D16) | **accepted by user** |
| Missing privacy and deletion requirements block the Play listing | high if skipped | Release rejected | A42, A43 | mitigated |
