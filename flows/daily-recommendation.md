# Flow: Daily recommendation (core flow)

> **Status:** 🔄 In progress — logic being built
> This is the heart of the app. If this flow isn't great, nothing else matters.

## Goal

When the user opens Tida, within a few seconds she knows **what to do today** for training, food and recovery — and *why*.

## Inputs

| Input | Source |
|---|---|
| Current cycle day | Calculated from cycle data entered in onboarding / calendar |
| Current phase | Derived from cycle day (see phase table below) |
| How she feels today | Optional daily check-in |

## Phase model

Based on a 28-day cycle. Source: "Piłka nożna kobiet
Narodowy Model Gry PZPN" autors: Katarzyna Barlewicz, Andrzej Dawidziuk, Bartłomiej Gąsior, Marcin Kasprowicz,
Paulina Kawalec, Adam Matuszczak, Mariusz Paszkowski, Nina Patalon, Miłosz Stępiński,
Anna Szymańska, Marta Walczak, Zuzanna Walczak, Michał Wandzel— the table that inspired Tida, found during my master's thesis research on women in sport.

| Days | Phase | Hormones | Focus | Intensity | Session priority | Key guidance |
|---|---|---|---|---|---|---|
| 1–2 | Early follicular (period) | Low estrogen, progesterone, testosterone | Regeneration | Low | Mixed: conditioning + strength | No technical skill or precision work. Reduce stress and volume. Mood changes and slower reaction time → higher risk of accidents. |
| 3–5 | Early follicular (period) | Low estrogen, progesterone, testosterone | Metabolic training | Low–medium | Mixed: conditioning + strength | Anaerobic and strength work, lactate-based efforts. Still no precision work. |
| 6–8 | Mid follicular | Rising estrogen, low progesterone | Metabolic & strength | Medium | Speed | High intensity, low volume, complex tasks. Anaerobic and strength work. |
| 9–13 | Late follicular | Estrogen peak | Aerobic training & injury prevention | Medium–high | Conditioning → strength + speed | Low-intensity, high-volume aerobic work. Non-weight-bearing and long sessions. |
| 14 | Ovulation | Testosterone peak | Max strength & power | Very high | Strength + speed | Strength and power training. |
| 15–20 | Early luteal | Rising progesterone | Max strength & power | Very high | Strength + speed | High intensity, low volume, complex tasks. Anaerobic and strength work. |
| 21–24 | Mid luteal | Estrogen & progesterone peak | Aerobic training & injury prevention | Medium | Hard conditioning | Low-intensity, high-volume aerobic work. Non-weight-bearing, long sessions. Stress management. |
| 25–28 | Late luteal | Low estrogen, progesterone, testosterone | Regeneration | Low | Mixed | No individual or precision tasks. Simple, low-stress tasks. Reduce stress and volume, include strength training. |

> ⚠️ Other cycle lengths: see open-questions.md → Q8. Late period: stay in late luteal guidance (see D5). Content to be reviewed by an expert (Q1).

## Steps

1. User opens the app → lands on **Today** screen.
2. Top: cycle day + phase name, in plain language (e.g. *"Day 9 · Late follicular — aerobic & injury prevention"*).
3. Three cards: **Train · Eat · Recover**, each with one short recommendation.
4. Tap a card → short explanation of *why* this fits today.
5. Optional: quick check-in — *"How's your energy today?"* (1–5).
6. If check-in disagrees with phase (e.g. low energy on a "peak" day) → **her feeling wins**, recommendation softens.

## Rules

- **The body beats the calendar.** Check-in always overrides phase-based defaults.
- Language is supportive, never guilt-tripping. No "you should", prefer "today could be a good day to…".
- No medical claims. Recommendations are suggestions, not prescriptions.

## Edge cases

| Case | Behaviour |
|---|---|
| No cycle data yet | Show general guidance + prompt to add cycle info |
| Period is late (days since last period > cycle length) | Do NOT start a new cycle. Show ‘Your period is X days late’ and a button to log a new period. Keep recommendations from the late luteal phase. See D5. |
| Irregular cycles | ⚠️ Open question — see Q2 |
| User skipped check-in | Use phase defaults only |

## Done when

- [ ] Correct phase shown for any cycle day
- [ ] All 3 cards show phase-specific content
- [ ] Low-energy check-in visibly changes the recommendation
- [ ] Empty state works with no data
- [ ] Late period handled: cycle 28 days, last period 40 days ago → shows ‘period is 12 days late’, not ‘day 12 of a new cycle’
