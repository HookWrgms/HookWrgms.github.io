---
title: "Context Engineering & Agent Patterns — The Anthropic Playbook"
date: 2026-04-04T18:00:00-04:00
draft: false
tags: ["anthropic", "agents", "context", "mcp", "engineering"]
---

## Research Focus

Anthropic's engineering blog on building effective agents and context engineering best practices

## Workflows vs Agents — The Critical Distinction

**Workflows:** LLMs and tools orchestrated through predefined code paths. Predictable, consistent, easier to debug.

**Agents:** LLMs dynamically direct their own processes and tool usage. Flexible, autonomous, emergent behavior.

**The Engineering Insight:** Don't build agents when workflows suffice. Agents add complexity that should be justified by demonstrably better outcomes.

## Five Practical Agent Patterns

| Pattern | Structure | Best For |
|---------|-----------|----------|
| **Prompt Chaining** | Sequential steps with programmatic gates | Marketing copy → translation |
| **Routing** | Input classification → specialized handler | Customer service triage |
| **Parallelization** | Independent subtasks run concurrently | Code reviews, content moderation |
| **Orchestrator-Workers** | Central LLM delegates dynamically | Multi-file code changes |
| **Evaluator-Optimizer** | Generate → evaluate → loop | Literary translation, complex search |

## Context Engineering — The New Frontier

**Definition:** Curating the optimal set of tokens during inference, not just writing better prompts.

**The Attention Budget:** LLMs have finite attention. Every token depletes it.

### Just-in-Time Context Strategy

- Don't pre-process all data upfront
- Maintain lightweight identifiers (file paths, stored queries)
- Dynamically load data at runtime using tools

**Claude Code's Hybrid Approach:**
- CLAUDE.md files loaded upfront (stable context)
- Primitives like glob/grep for just-in-time navigation

## MCP + Code Execution = 98.7% Token Reduction

**The Problem:** Tool definitions overload context windows. 1000s of tools = 100,000s of tokens.

**The Solution:** Present MCP servers as code APIs, not direct tool calls.

| Approach | Tokens |
|----------|--------|
| Direct | 150,000 |
| Code execution | 2,000 |
| **Reduction** | **98.7%** |

## Long-Horizon Task Techniques

**Compaction:** Summarize conversation near context limit, reinitiate with summary.

**Structured Note-Taking:** Agent writes NOTES.md persisted outside context.

**Sub-Agent Architectures:**
- Specialized sub-agents handle focused tasks
- Main agent coordinates with high-level plan
- Sub-agents explore deeply (10k+ tokens), return condensed summary (1-2k tokens)

## Engineering Takeaways

1. **Start simple.** Workflows before agents.

2. **Context is precious.** Find the smallest set of high-signal tokens.

3. **Use code execution with MCP.** 98.7% token reduction is achievable.

4. **Design tools like APIs for junior devs.** Clear docstrings, minimal overlap.

5. **Framework warning:** Frameworks add abstraction that obscures prompts/responses. Start with direct LLM API calls.
