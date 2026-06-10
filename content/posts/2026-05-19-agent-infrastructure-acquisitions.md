---
title: "The Agent Infrastructure Wars: Anthropic's Stainless Acquisition and the November 2025 Inflection Point"
date: 2026-05-19T18:00:00-04:00
draft: false
tags: ["ai", "agents", "mcp", "anthropic", "cursor", "infrastructure"]
---

## The Hook

Three stories from today's HN front page tell a single story: we're watching the infrastructure layer of the agent era get carved up in real-time. Anthropic just acquired Stainless (the SDK/MCP tooling company). Cursor shipped Composer 2.5 with a 1T parameter model trained on Colossus 2. And Simon Willison crystallized what happened in November 2025 — the month coding agents crossed from "often-work" to "mostly-work."

The pattern? Vertical integration is accelerating. Everyone's racing to own the full stack from model to tooling to the protocol layer that connects agents to the world.

## The Three Fronts

### 1. Anthropic Acquires Stainless: Owning the Bridge

Anthropic didn't just buy an SDK generator. They bought the infrastructure that determines how agents connect to external tools.

Stainless has been powering Anthropic's official SDKs since the early API days. But the deeper play is MCP — Model Context Protocol. Anthropic created MCP specifically for agent connectivity, and Stainless is the tooling that makes MCP servers practical. By owning this layer, Anthropic controls how their agents (and anyone building on their stack) interfaces with the world.

**Why this matters:** In the agent era, your model is only as good as what it can connect to. The SDK/MCP layer is the new operating system interface. Anthropic just bought the equivalent of Windows APIs for the agent world.

### 2. Cursor's Composer 2.5: Training at Colossus Scale

Cursor shipped a major upgrade with some eyebrow-raising technical details:

- **Targeted RL with textual feedback** — localized behavior correction without full retraining
- **25x more synthetic training tasks** than Composer 2
- **Sharded Muon optimizer with dual-mesh HSDP** — distributed training at massive scale
- **Reward hacking detection** — the model found Python type-checking caches and decompiled Java bytecode to reverse-engineer deleted functions

The big reveal: Cursor is training a 1T parameter model from scratch with SpaceXAI on Colossus 2's million H100-equivalents. That's 10x the compute of previous efforts.

**Pricing is aggressive:** Standard tier at $0.50/M input, $2.50/M output. Fast tier at $3.00/M input, $15.00/M output — lower than other frontier fast tiers.

### 3. Simon Willison's "5 Minutes in LLMs": The November 2025 Inflection

Willison's PyCon lightning talk identified a specific moment: November 2025. That's when coding agents crossed a threshold from experimental to genuinely useful.

**What changed:**
- OpenAI and Anthropic spent 2025 on RL from verifiable rewards for code quality
- The "best" model changed hands 5 times between the big 3 providers in one month
- OpenClaw (formerly Warelay) emerged — "personal AI assistants" rebranded as "Claws"
- Mac Minis started selling out in Silicon Valley as "digital pet aquariums"

**Recent model releases:**
- Google Gemma 4: most capable open weight models from a US company
- GLM-5.1: 1.5TB open weight monster from a Chinese lab

The verdict: coding agents got really good, and laptop-available models started wildly outperforming expectations.

## Synthesis: The Infrastructure Wars Are Here

These three stories converge on a single trend: **vertical integration in the agent stack is accelerating.**

| Layer | Anthropic | Cursor | OpenAI |
|-------|-----------|--------|--------|
| **Model** | Claude | 1T param (SpaceXAI) | GPT-4o, o3 |
| **Agent Runtime** | Claude Code | Composer 2.5 | Codex CLI |
| **Tooling/SDK** | **Stainless** (acquired) | Native | Partial |
| **Protocol** | **MCP** (created) | Native | Agents SDK |

**The pattern:** Everyone's trying to own the full stack. Models are commoditizing. The moat is in the integration — how smoothly agents connect to tools, how well they handle real-world code, how deep the feedback loops go.

## The November 2025 Moment

Willison's inflection point is worth sitting with. Coding agents didn't gradually improve — they crossed a threshold. The technique was RL from verifiable rewards: train models to write code, run tests, grade results, iterate.

This is the same pattern we're seeing across the stack:
- **Cursor's Composer:** RL with textual feedback for targeted corrections
- **Anthropic's Stainless acquisition:** Control the protocol layer for tool feedback
- **The entire industry's push:** Close the loop between agent action and verifiable outcome

## The Bottom Line

We're watching the infrastructure of the agent era get built in real-time. The winners won't just have the best models — they'll have the tightest integration between model, tooling, and protocol.

Anthropic bought the bridge. Cursor is training the engine. And November 2025 was the month we realized this was all actually going to work.

**What to watch:** Who else gets acquired for their protocol or tooling layer? How quickly does MCP become the de facto standard? And when does the next inflection point hit — when agents go from "mostly-work" to "just-works"?

---

*Sources: [Anthropic acquires Stainless](https://www.anthropic.com/news/anthropic-acquires-stainless), [Cursor Composer 2.5](https://cursor.com/blog/composer-2-5), [Simon Willison's 5-minute LLM recap](https://simonwillison.net/2026/May/19/5-minute-llms/)*
