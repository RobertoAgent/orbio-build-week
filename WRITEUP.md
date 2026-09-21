# Short write-up — Orbio Build Week

**Project:** Roberto — personal always-on AI agents  
**Builder:** `@JussCubs` (approved on Orbio Build Week)  
**Repo:** this packet only (product is closed source)  
**Live:** [robertoagent.com](https://robertoagent.com)

## What it does

Roberto is an always-on personal agent. You create a Roberto, open a **Room** (shared with family, friends, or teammates), and hand off real work: research, browsing, bookings, writing, code, follow-ups. The agent runs on its own dedicated runtime and pings you when it needs a decision.

## What we built on Orbio

We treated Orbio as the default path to “one key, all the models”:

1. **Bring your Orbio key on first run** — encrypted secret, same vault as other harnesses.
2. **Auto-select DeepSeek V4 Flash Latest (Orbio)** once that key is connected, so the welcome meeting and room brain hit `api.orbio.so` with the user’s key.
3. **Managed Orbio → OpenRouter fallback** so empty balances or outages don’t kill the session.
4. **Spend tracking** — managed Orbio inference is attributed per user, agent, and Room for Impact and ops.
5. **Onboarding that actually sends people to Orbio** (affiliate referral) without turning the product into a banner ad for a hackathon.

## Why it should win

- It is a **real always-on agent**, not a notebook that calls an API once.
- Orbio is **wired into the product spine** (onboarding → default model → usage ledger), not a side demo.
- Engineering bar is production: multi-surface clients, warm pool, billing, Impact SQL, closed-source runtime already disclosed to Orbio.

## Demo

Polished video is **in production** and will be linked from [`assets/demo/`](./assets/demo/). Until then, judges can use the live site with early access / invite.

## Ask

Evaluate Roberto as an Orbio-powered personal agent runtime: one key, continuous work, shared Rooms, measured spend.
