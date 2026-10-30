# How I build with AI

> Tida is built by one person. AI agents do most of the code writing — my job is the intent, the spec and checking what comes back.

## The workflow

```
  Spec (this repo)
       │
       ▼
  Gemini Pro  ── I discuss the feature, split it into small, clear tasks
       │
       ▼
  Cursor agent ── writes the code in the React Native / Supabase project
       │
       ▼
  Me  ── run the app, test the flow, compare with the spec
       │
       ├── matches the spec → done, tick the "Done when" checklist
       └── doesn't match   → fix the task description (or the spec) and repeat
```

## My rules

1. **Spec first, code second.** If I can't describe the feature clearly, the agent can't build it.
2. **Small tasks.** One screen or one piece of logic at a time — big tasks come back messy.
3. **Every flow has a "Done when" checklist.** That's how I check the agent's work, not by reading every line.
4. **When the AI gets it wrong, I fix the instructions first.** A wrong result usually means an unclear spec.
5. **Secrets never go into the repo.** `.env` files with keys stay local.

## What I've learned

- AI is fast at writing code, but it doesn't know *what* the product should be. That part stays with me.
- Debugging taught me the architecture — I understand every part of the app because I had to fix it.
