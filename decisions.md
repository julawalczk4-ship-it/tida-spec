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

---

## D6 — During the period, Tida doesn't default to "rest"

**Decision:** Tida follows the 7-phase model in `flows/daily-recommendation.md`. During the period: days 1–2 are regeneration without technical or precision work; days 3–5 are metabolic training (anaerobic, lactate-based and strength work) — not rest or "just yoga".

**Why:**
- Most cycle apps tell women to rest during their period. That doesn't work for competitive athletes, or for women with demanding jobs.
- The research behind the model shows that removing technical and precision work while bleeding — when reaction time is slower — lowers injury risk, while metabolic and strength work still gives a high-quality session.
- This is Tida's core difference from other cycle apps.

**Trade-off:**
- Goes against what users expect from other apps — the copy must explain *why*.
- It's still a suggestion: the daily check-in overrides it (see D4).

**Status:** ✅ Spec updated · 🔄 recommendation content in the app to follow.

---

## D7 — Protect Intellectual Property (Local Teasers vs Remote Data)

**Decision:** The app binary (APK/IPA) contains only small "freemium" teasers of the Knowledge Base and Recipes. Full catalogs live strictly on Supabase and are fetched only for authenticated users.

**Why:**
- Protects the core IP from being extracted by reverse-engineering the app binary.
- Keeps the initial app download size small and lightweight.

**Trade-off:**
- Requires an internet connection to read the full content.
- We need robust caching logic to handle offline states gracefully.

**Status:** ✅ Built and working.

---

## D8 — Absolute Data Privacy (Row Level Security)

**Decision:** Strict Supabase RLS (Row Level Security) policies mandate that a user can only read, update, or delete their own health and cycle logs. Knowledge Base articles are strictly read-only.

**Why:**
- Tida processes highly sensitive health data. Absolute isolation at the database level is non-negotiable for user trust.
- It is a foundational requirement for GDPR compliance and Apple's privacy review.

**Trade-off:**
- More complex database setup and local testing.
- Requires careful handling of authentication states in the client.

**Status:** ✅ Built and working.

---

## D9 — Secure AI Architecture & Guardrails

**Decision:** OpenAI API calls run strictly on the backend via Supabase Edge Functions. The AI System Prompt strictly forbids medical diagnoses and relies on injected background context (cycle phase, athlete mode).

**Why:**
- Hides the OpenAI API key from the client app, preventing quota theft.
- Guarantees the AI behaves like a holistic coach, not a doctor (crucial for keeping our non-medical positioning from D2).

**Trade-off:**
- Costs us execution time (Edge Function latency) compared to direct client calls.
- Requires maintaining separate server-side code in Deno/TypeScript.

**Status:** ✅ Built and working.

---

## D10 — Opt-in Integrations via Apple Health / Health Connect

**Decision:** Tida reads external device data (Garmin, Whoop, Strava) exclusively through Apple HealthKit / Google Health Connect. We do not integrate direct third-party APIs.

**Why:**
- Keeps the codebase lightweight and respects user privacy by using native OS aggregators.
- External data acts as an "invisible boost" to recommendations, meaning the app remains 100% fully functional without a smartwatch.

**Trade-off:**
- We rely on the OS aggregators and cannot access raw, proprietary metrics that aren't shared with Apple/Google.

**Status:** 🔄 In the spec, to be built.

---

## D11 — Freemium & Subscription Model (Paywall)

**Decision:** RevenueCat handles subscriptions. Free accounts get basic tracking and teasers; PRO status (`is_pro`) unlocks full catalogs. 50% of revenue goes to women's health research.

**Why:**
- Offloads receipt validation and app store compliance to a reliable third party (RevenueCat).
- The 50% charity split is a core brand pillar and must be clearly communicated on the paywall.

**Trade-off:**
- RevenueCat takes a small percentage of sales.
- UI logic must clearly and gracefully gate premium features without frustrating the user.

**Status:** 🔄 In the spec, to be built.
