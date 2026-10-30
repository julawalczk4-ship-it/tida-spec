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

## Phases (working model)

| Phase | Training direction | Recovery direction |
|---|---|---|
| Menstrual | Lighter movement, mobility, yoga | Rest, warmth, sleep |
| Follicular | Building intensity, try new things | Normal |
| Ovulatory | Peak — strength, intense cardio | Normal |
| Luteal | Steady, moderate; lower intensity late in phase | More recovery, sauna, sleep |

> ⚠️ Content and exact day ranges to be validated with an expert (see `open-questions.md` → Q1).

## Steps

1. User opens the app → lands on **Today** screen.
2. Top: cycle day + phase name, in plain language (e.g. *"Day 9 · Follicular — energy's building"*).
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
