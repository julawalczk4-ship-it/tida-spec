# Decisions log

> Every important decision with its **why** and its **trade-off**.
> Format: what we decided · why · what it costs us · status.

---

## D1 — Build the whole app myself, with AI, instead of hiring developers

**Decision:** No external developers. I build frontend and backend myself in Cursor, with AI agents doing most of the code writing.

**Why:**
- 100% independence — no waiting on contractors, no handover gaps
- Full control over the architecture (especially the Supabase data model)
- Deep understanding of my own product — I can explain and change any part of it

**Trade-off:**
- Much longer learning curve — architecture and debugging are on me
- Slower start than hiring a dev team would have been

**Status:** ✅ Holding. Foundation (Expo app, Supabase, auth, navigation) is in place.

---

## D2 — Position Tida as sport / wellbeing, not health / medical

**Decision:** Tida is a training & lifestyle guide. We never position it as a health or medical app.

**Why:**
- The real user need is *"how should I train today"*, not diagnosis
- Keeps the product focused on the active woman, not on patients
- Medical positioning brings much heavier requirements on claims and content

**Trade-off:**
- We can't make health claims, even when they'd sell well
- Every piece of copy must be checked against this line

**Status:** ✅ Holding. Shapes onboarding (expectations note) and all recommendation copy.

---

## D3 — Tech stack: React Native + Expo + Supabase

**Decision:** One codebase for iOS and Android (React Native + Expo), Supabase for database and login.

**Why:**
- One codebase for both platforms — essential for a one-person team
- Well-known stack → AI agents write good code for it
- Supabase gives database + auth out of the box, without building a backend from scratch

**Trade-off:**
- Some dependency on Expo and Supabase as platforms

**Status:** ✅ Built and working.

---

## D4 — The user's feeling overrides the calendar

**Decision:** If the daily check-in says "low energy" on a phase that's normally high-energy, the recommendation softens.

**Why:** The product promise is *"in tune with your body"* — a calendar that ignores how she actually feels would break it.

**Trade-off:** More complex recommendation logic; phase alone isn't enough.

**Status:** 🔄 In the spec, to be built (see `flows/daily-recommendation.md`).

---

## D5 — A late period is never treated as a new cycle

**Decision:** If more days have passed than the cycle length and the user hasn’t logged a new period, the app shows the period as late instead of silently starting a new cycle.

**Why:** Found in the pre-launch code audit — the app showed ‘day 12 of a new cycle’ instead of ‘12 days late’. For a cycle app this is a factual error users notice immediately and it breaks trust.

**Trade-off:** One more state in the logic and UI. The ‘late’ message must stay neutral and non-medical (see D2).

**Status:** ✅ Spec updated · ✅ Fixed in code (`lib/cycleMetrics.ts`, Today screen, PL/EN copy) and verified in tests + iOS simulator.
