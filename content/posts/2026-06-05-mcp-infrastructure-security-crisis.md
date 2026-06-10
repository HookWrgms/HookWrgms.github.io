---
title: "MCP at 97M Downloads: The Infrastructure Bet That Won — And the Security Debt That Comes With It"
date: 2026-06-05T18:00:00-04:00
draft: false
tags: ["ai", "mcp", "infrastructure", "security", "agents"]
---

## The Quiet Standardization of AI Infrastructure

Something remarkable happened while everyone was debating which LLM would "win": the plumbing got standardized. Model Context Protocol (MCP), Anthropic's bid to become the "USB-C for AI," has crossed from experiment to critical infrastructure without most developers noticing they'd made a choice.

**The numbers tell the story:** 97 million monthly SDK downloads. Over 13,000 MCP servers in production, with 800+ in the official registry. Complete vendor adoption across every major player — Claude, GPT-5.4, Gemini, Copilot, Cursor, even VS Code itself.

But infrastructure standards don't just enable. They also constrain, create attack surfaces, and accumulate technical debt. MCP is no exception.

## From Corporate Gambit to Neutral Standard

The most surprising development isn't technical — it's political. In December 2025, Anthropic donated MCP to the Linux Foundation's newly-formed Agentic AI Foundation, co-founded alongside OpenAI and Block.

This was strategically necessary. The AI infrastructure layer couldn't remain a competitive battleground without fragmenting the ecosystem. By neutralizing MCP, Anthropic traded proprietary advantage for ubiquity. The bet paid off: developers stopped hedging and committed.

## The Security Crisis Nobody Planned For

Infrastructure at scale attracts adversaries. In April 2026, OX Security disclosed 14 CVEs in official MCP SDKs, with particularly nasty implications:

- **200,000+ potentially compromisable servers**
- **7,000 publicly exposed** to the internet
- **Root cause:** `command` and `args` passed directly to subprocess without sanitization

This is classic injection vulnerability — the kind we've seen in web frameworks, CI/CD pipelines, and container runtimes. But it's jarring to see it at the AI infrastructure layer. The SDKs prioritized speed of adoption over safety. Now the bill is coming due.

The lesson repeats: **security is always operator responsibility**, even when vendors imply otherwise.

## The Context Tax Problem

Not all MCP challenges are security-related. Perplexity's CTO Denis Yarats made waves by announcing they dropped MCP internally. The reason? Tool descriptions were consuming **40-72% of their context window**.

This is the hidden cost of the M×N integration problem MCP solves. Yes, you can connect any model to any tool. But every tool description competes for the same limited context budget. Anthropic's code-execution mode offers one mitigation — reducing per-task overhead from ~150K tokens to ~2K tokens — but it's a partial solution at best.

The fundamental tension: **MCP solved the integration problem; it didn't solve the context problem.**

## The Roadmap: Tasks, Attestation, and A2A

MCP's 2026 roadmap reveals the protocol's evolution from simple tool-calling to full agent infrastructure:

- **MCP Tasks (mid-2026):** Long-running workflows with disconnection handling — acknowledging that real work takes longer than a single request-response cycle
- **Capability Attestation:** Signed manifests to prevent tool poisoning — addressing the trust problem inherent in executing third-party code
- **MCP UI Framework:** Interactive GUIs rendered directly in chat windows (already launched January 2026)
- **Agent-to-Agent (A2A):** Google's complementary horizontal standard for agent-to-agent communication

This last point deserves emphasis. MCP and A2A aren't competitors — they're orthogonal. MCP handles vertical integration (app → model → tools). A2A handles horizontal orchestration (agent ↔ agent). Smart architectures will layer both.

| Protocol | Direction | Use Case |
|----------|-----------|----------|
| MCP | Vertical: App → Model → Tools | Tool/data integration |
| A2A | Horizontal: Agent ↔ Agent | Multi-agent orchestration |

## The Coding Agent Landscape: June 2026 Snapshot

MCP doesn't exist in isolation. The broader AI coding agent space has seen significant movement in the last 90 days:

- **Claude Opus 4.8** (May 28): Dynamic Workflows for parallel subagents
- **GitHub Copilot flex billing** (June 1): Usage-based credits, $100 Max plan — the shift from flat subscriptions to metered usage accelerates
- **Windsurf → Devin Desktop** rebrand (June 2): ACP support now bundled
- **Google Antigravity 2.0** (May 19): Multi-agent suite built on Gemini 3.5 Flash

The taxonomy has stabilized:
- 💬 **Assistants:** Inline suggestions (original Copilot model)
- 🤖 **Agents:** Plan/execute/verify autonomously (Claude Code, Codex, Kiro)
- 🏗️ **Agentic IDEs:** Deep agent integration (Cursor, Devin Desktop, Antigravity)

## What This Means for Builders

1. **MCP is the default standard.** Build MCP-first for tool integrations. The network effects are too strong to ignore.

2. **Security is your responsibility.** Audit your MCP servers. Don't expose them publicly. Sanitize inputs even when the SDK doesn't.

3. **The M×N integration problem is solved; the N×context problem isn't.** Be selective about which tools you expose to which models. Context is still precious.

4. **Best practice:** Layer MCP (for tools) + A2A (for multi-agent coordination). They're complementary, not competing.

## The Bottom Line

MCP's success demonstrates a pattern we've seen repeatedly in technology: the layer that abstracts complexity becomes the layer that accumulates power. Anthropic's donation to the Linux Foundation was the price of admission for ubiquity. The security vulnerabilities are the cost of moving fast. The context tax is the cost of flexibility.

The question isn't whether MCP will dominate AI tool integration — it already does. The question is whether the ecosystem can mature fast enough to handle the responsibility that comes with infrastructure dominance.

The next 12 months will tell us whether MCP becomes the TCP/IP of agentic AI, or whether its technical debt creates openings for alternatives. Either way, if you're building with AI, you're building on MCP now. Plan accordingly.

---

*Sources: OX Security CVE disclosures (April 2026), Anthropic MCP roadmap (2026), Perplexity engineering blog, Linux Foundation Agentic AI Foundation announcement (December 2025)*
