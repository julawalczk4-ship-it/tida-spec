# Tida — Product Spec

> **Status:** Living document · pre-launch · last updated: 2026-10

Tida helps active women match their training, nutrition and recovery to the current phase of their cycle — instead of following one-size-fits-all plans that ignore how energy naturally changes across the month.

This repo is the **single source of truth for what Tida is, who it's for, and why it works the way it does.** It's written so that a person *or* an AI agent can build from it without guessing.

## How this repo is organised

| File | What's inside | Read it when… |
|---|---|---|
| [`vision.md`](vision.md) | Problem, target user, positioning, what Tida is *not* | You're new to the project |
| [`flows/daily-recommendation.md`](flows/daily-recommendation.md) | The core flow: open app → see today's guidance | You're building or reviewing the main screen |
| [`flows/onboarding.md`](flows/onboarding.md) | First launch → account → cycle setup | You're building sign-up |
| [`decisions.md`](decisions.md) | Key product & tech decisions with their trade-offs | You want to know *why*, not just *what* |
| [`open-questions.md`](open-questions.md) | What's still undecided | Before you assume anything |
| [`how-i-build-with-ai.md`](how-i-build-with-ai.md) | How specs turn into code via AI agents | You want to understand the workflow |

## Ground rules

1. **If it's not in the spec, it's not decided.** Add it to `open-questions.md` instead of guessing.
2. **Every decision has a "why".** New decisions go to `decisions.md` with the trade-off.
3. **Changes go through pull requests**, so the history of *why the spec changed* stays visible.

## Current state (snapshot)

- ✅ React Native + Expo app skeleton, environment set up
- ✅ Supabase database connected, login working
- ✅ Basic navigation based on Figma designs
- 🔄 Recommendation logic by cycle day — in progress
- 🔄 AI assistant modules — in progress
- ⏳ Final UX polish — before launch
