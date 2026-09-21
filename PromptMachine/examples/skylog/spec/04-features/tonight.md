# Tonight (campus)

**Tier:** v0 · **Sources:** D1, D6, D9, A6, A14, A25

## Behaviour
1. Shows the next 5 nights for the campus site, ranked by night score (03-data-model.md).
2. Each night: rank, "2 of 3 forecasts agree it's mostly clear", dark hours, Moon phase
   and rise/set, planets up. Tap for the hourly cloud numbers from each model.
3. Forecast fetched from Open-Meteo, three independent models, at most every hour,
   cached on the phone. Source credited on screen. (A6)
4. Wording is fixed: "more promising", "less promising", never "best", "go" or "will be
   clear". (D9)

## States
- Offline: last forecast shown with "fetched 3 h ago". Older than 6 hours: numbers stay,
  ranking hidden, "Forecast out of date". (A25)
- Fewer than 2 models returned: ranking hidden, numbers shown.

## Acceptance criteria
- [ ] Given three models with 10%, 20% and 80% cloud across all dark hours, then
      agreement reads "2 of 3" and the night scores 0.67.
- [ ] Given a forecast 7 hours old, then no ranking is shown.
- [ ] Given any state, then the interface contains none of "best", "go", "will be clear".
- [ ] Given only 1 of 3 models returns data, then hourly numbers show and no ranking is shown.
- [ ] Given any forecast view, then the fetch time and the forecast source credit are visible.
