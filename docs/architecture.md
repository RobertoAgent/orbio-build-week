# Architecture notes (submission)

This document describes the **public architecture** of Roberto as it relates to Orbio. It intentionally omits proprietary implementation details and contains **no source code**.

## Surfaces

* **Web:** Next.js product + marketing ([robertoagent.com](https://robertoagent.com))
* **Mobile:** React Native / Expo (iOS + Android)
* **Desktop:** Electron (macOS, Windows, Linux)
* **API:** Hono control plane (agents, rooms, secrets, billing, Impact, remote MCP)
* **Runtime:** dedicated agent containers (warm pool); OpenClaw based agent loop

## Orbio in the stack

```text
User pastes Orbio key (onboarding)
        │
        ▼
Encrypted user_secrets (BYOK)
        │
        ▼
Agent / room model selector
  └─ default: DeepSeek V4 Flash Latest via Orbio route
        │
        ▼
Runtime LLM calls (OpenAI compatible)
  ├─ user Orbio key (preferred)
  └─ managed Orbio → OpenRouter fallback
        │
        ▼
llm_usage_events (+ cost_source provenance)
```

## Rooms

Rooms are the shared workspaces (internally chat sessions). Guests do not pay; usage draws from the owner’s plan / keys. Roberto acts inside the Room with tools (browser, files, skills, Impact queries, etc.).

## Diagram slots

Drop polished visuals here:

* `assets/diagrams/system-overview.png` clients → API → runtime → Orbio
* `assets/diagrams/orbio-key-flow.png` BYOK → default model → fallback → usage
* `assets/diagrams/room-session.png` Room participants + agent tools

ASCII overview also lives in the root [`README.md`](../README.md).
