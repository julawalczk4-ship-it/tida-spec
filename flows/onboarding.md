# Flow: Onboarding

> **Status:** ✅ Login works · 🔄 cycle setup in progress
> Goal: get from first launch to a useful **Today** screen in under 2 minutes.

## Principle

Ask only what's needed to show the first recommendation. Everything else can come later.

## Steps

1. **Welcome** — one screen, one promise: *"Train with your cycle, not against it."*
2. **Account** — sign up / log in (Supabase Auth). ✅ Built.
3. **Clear expectations** — short note: Tida is a wellbeing & training guide, not a medical or contraception tool. User taps *"Got it"*.
4. **Cycle setup**
   - First day of last period (date picker)
   - Typical cycle length (default 28, editable)
   - "Not sure" option → use defaults, refine later
5. **Activity profile** (optional, skippable)
   - Main activities: gym · running · outdoor · yoga · other
6. → Land on **Today** screen (see [`daily-recommendation.md`](daily-recommendation.md)).

## Rules

- Every step after Account can be skipped. Skipping never blocks the app.
- No more than one question per screen.
- Data she enters is hers — editable anytime in settings.

## Edge cases

| Case | Behaviour |
|---|---|
| User doesn't know her last period date | "Not sure" → general guidance + gentle reminder later |
| Irregular cycles | ⚠️ See `open-questions.md` → Q2 |
| User quits mid-onboarding | Resume at the last unfinished step |

## Done when

- [ ] New user reaches Today screen with phase-based content
- [ ] Skipping cycle setup still lands on a working (generic) Today screen
- [ ] Expectations note shown once, before any cycle data is collected
