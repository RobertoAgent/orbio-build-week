# Roberto × Orbio Build Week

**Always-on personal agents that run on one Orbio key.**

> **Submission status:** Orbio Build Week · builder `@JussCubs` (approved)  
> **Product:** [robertoagent.com](https://robertoagent.com)  
> **Source:** closed source (disclosed to Orbio). This public repo is the **hackathon packet only** — README, write-up, architecture notes, and demo assets. No product source code is included.

---

## The one-liner

Roberto is a personal AI agent you own. It lives in shared **Rooms**, runs 24/7 on its own runtime, and does real work — browse, book, write, code, follow up — instead of handing you a to-do list.

For Orbio Build Week we wired Roberto so **one Orbio key** can power that agent end-to-end: first-run BYOK, DeepSeek Flash as the default brain on the connected key, and managed spend tracking when Roberto falls back to its own Orbio/OpenRouter path.

That is the brief: *build an agent on your key.*

---

## Demo video

> **Coming soon.** A polished walkthrough is being recorded and will land in [`assets/demo/`](./assets/demo/).
>
> Until then, try the live product: [robertoagent.com](https://robertoagent.com) (invite / early access).

**Slot for the video:** drop the final file at `assets/demo/orbio-build-week-demo.mp4` (or link it from `assets/demo/README.md`).

---

## What we built (Orbio-facing)

| Piece | What it does |
| --- | --- |
| **BYOK on first-run** | New users can paste an Orbio API key during onboarding. The key is stored encrypted like other harness secrets. |
| **DeepSeek Flash default** | After an Orbio key is connected, first-run auto-selects **DeepSeek V4 Flash Latest (Orbio)** on that route for the welcome meeting and room brain. |
| **Managed fallback** | If the user key is empty/expired (402 / outage), Roberto-managed inference continues the session (Orbio first → OpenRouter fallback). |
| **Spend provenance** | Managed Orbio usage is attributed per user / agent / Room (`cost_source` on usage events) so Impact and ops can see what the key actually burned. |
| **Affiliate onboarding** | “Get a key at orbio.so” keeps friendly link text but routes through the referral URL. |
| **Always-on runtime** | Each Roberto is a dedicated container runtime (warm pool on Hetzner). The agent stays up; Orbio is the brain meter. |

Product copy deliberately **does not** lean on hackathon language — Orbio is presented as discounted, OpenAI-compatible inference (RWA-funded), because this is a real product shipping to users, not a weekend demo.

---

## Architecture (high level)

```text
                    ┌─────────────────────────────┐
                    │  Clients (web / mobile /    │
                    │  desktop / Telegram / …)    │
                    └──────────────┬──────────────┘
                                   │ Privy JWT
                    ┌──────────────▼──────────────┐
                    │  Control plane (Hono API)    │
                    │  agents · rooms · secrets   │
                    │  billing · Impact · MCP     │
                    └──────────────┬──────────────┘
                                   │
              ┌────────────────────┼────────────────────┐
              │                    │                    │
   ┌──────────▼──────────┐  ┌──────▼──────┐  ┌─────────▼─────────┐
   │  Agent runtime      │  │  Supabase   │  │  Stripe / mailer  │
   │  (OpenClaw in       │  │  Postgres   │  │                   │
   │   Hetzner pool)     │  │  + Realtime │  │                   │
   └──────────┬──────────┘  └─────────────┘  └───────────────────┘
              │
              │  OpenAI-compatible
              ▼
   ┌─────────────────────┐
   │  Orbio key (BYOK)   │──── models / tools / voice / …
   │  or managed Orbio   │
   │  → OpenRouter FB    │
   └─────────────────────┘
```

See also: [`docs/architecture.md`](./docs/architecture.md) and placeholder diagram slots under [`assets/diagrams/`](./assets/diagrams/).

---

## Why this fits Orbio Build Week

1. **One key, agentic app** — Roberto is not a chat wrapper. It is an always-on agent with tools, Rooms, browser, and routines, pointed at Orbio.
2. **Ecosystem pull** — onboarding features Orbio, defaults the connected key to a strong cheap model, and measures managed spend so Orbio usage is real, not ornamental.
3. **Engineering quality** — parity across web/mobile/desktop, server-controlled product flags, warm-pool provisioning, Impact SQL for agents, gateway repair — the agent has to stay up for the key to matter.
4. **Honest closed source** — the runtime and control plane stay private; this repo is the public submission surface judges asked for (repo + demo + write-up).

---

## Short write-up

Full one-pager: [`WRITEUP.md`](./WRITEUP.md).

**TL;DR for judges:** We shipped Orbio as a first-class brain for Roberto — BYOK on day zero, DeepSeek Flash default on the user’s key, managed Orbio spend tracking, and an always-on personal agent that actually uses that key to do work in shared Rooms.

---

## Assets

| Path | Purpose |
| --- | --- |
| [`assets/demo/`](./assets/demo/) | **Demo video slot** (fancy cut coming from the builder) |
| [`assets/screenshots/`](./assets/screenshots/) | Product UI screenshots (placeholders ready) |
| [`assets/diagrams/`](./assets/diagrams/) | Architecture diagram placeholders |
| [`docs/architecture.md`](./docs/architecture.md) | Longer architecture notes |
| [`WRITEUP.md`](./WRITEUP.md) | Short hackathon write-up |

---

## Links

- Product: [https://robertoagent.com](https://robertoagent.com)
- Orbio Build Week: [https://www.orbio.so/build](https://www.orbio.so/build)
- Builder: GitHub [`JussCubs`](https://github.com/JussCubs) · org [`RobertoAgent`](https://github.com/RobertoAgent)

---

## License / source notice

© Roberto Agent. Product source is **not** published here. Materials in this repository are for Orbio Build Week evaluation only unless otherwise noted.
