---
title: "Trust Boundaries: The Real Battle in AI Coding Agents"
date: 2026-05-22T18:00:00-04:00
draft: false
tags: ["ai", "security", "coding-agents", "claude-code", "codex", "gemini"]
---

## The Hook

We obsess over benchmarks and token costs, but the real differentiator in AI coding agents isn't intelligence—it's trust architecture. While everyone debates SWE-bench scores, a quieter revolution is happening in how these tools handle permissions, sandboxing, and failure modes. And one of them just had a security vulnerability that should make us all pay closer attention.

## The Three Runtime Models

Today's AI coding CLI tools represent three distinct philosophies on trust:

| CLI | Trust Model | Sandbox | Default Stance |
|-----|-------------|---------|----------------|
| **Claude Code** | Human-in-the-loop | Process-level | Prompt-first |
| **Codex CLI** | Zero-trust containment | Kernel-level (Seatbelt/Landlock/DACL) | Graduated autonomy |
| **Gemini CLI** | User-initiated approval | None | Read-only Plan Mode |

Claude Code assumes the human is the ultimate authority. Codex CLI assumes the agent might be compromised and acts accordingly. Gemini CLI assumes the user wants to see everything before it happens.

Each approach has trade-offs. But only one of them just shipped a patch for a vulnerability that could have allowed arbitrary code execution.

## The Claude Code Vulnerability (Patched v2.1.90)

Here's what happened: Claude Code's bash permission system uses deny rules to block dangerous commands. But the regex parser had a failure mode—after 50 chained subcommands, it would give up and fall back to a generic "ask" prompt.

Security failed *open*, not closed.

The attack vector? A poisoned `CLAUDE.md` file with 50+ innocuous commands followed by a malicious payload at position 51. The parser, exhausted, would punt to the user with a generic prompt—potentially misleading them into approving something dangerous.

This is a classic complexity-collapse bug. The system worked fine under normal conditions but degraded predictably under edge cases—exactly the kind of vulnerability that emerges when security logic grows complex enough to have its own failure modes.

## Codex CLI's Kernel-First Approach

OpenAI's Codex CLI took a different path: kernel-level sandboxing from day one.

- **macOS**: Seatbelt profiles
- **Linux**: Landlock LSM + seccomp  
- **Windows**: DACL permissions

The key difference: this is a *physical* guarantee, not a policy one. Even if the agent is fully compromised, it cannot escape the project directory. The sandbox is enforced by the operating system kernel, not by regex patterns that can degrade.

This is the difference between "we try to catch bad commands" and "bad commands can't do damage."

## Gemini's Conservative Play

Google's Gemini CLI sits at the other extreme. No sandbox, but also no autonomous execution. Everything runs in "Plan Mode" by default—the agent proposes, the user approves.

The upside: Apache 2.0 license, fully auditable, trusted folders scope filesystem access. The worst-case scenario is a proposed diff, not data loss.

The downside: friction. Every action requires explicit approval, which breaks flow state for experienced users.

## The Benchmark Reality

Here's where it gets interesting. Despite their architectural differences, performance is converging:

| Tool | SWE-bench Verified | Terminal-Bench 2.0 | First-Pass Accuracy |
|------|-------------------|-------------------|---------------------|
| Codex CLI (GPT-5.5) | 88.7% | 77.3% | ~85% |
| Claude Code (Opus 4.7) | 87.6% | 72.1% | ~95% |
| Gemini CLI (3.1 Pro) | 80.6% | 68.4% | ~78% |

Claude Code's higher first-pass accuracy reflects stronger multi-file reasoning. Codex compensates via faster sandboxed iteration—when you can run commands safely, you can afford to try more approaches.

The takeaway: sandboxing doesn't cost you performance. It changes your optimization target from "be careful" to "move fast."

## The Pricing Angle Everyone Misses

Monthly caps matter more than per-token rates. For most developers:

- **Gemini**: Free tier (1K requests/day) remains unbeatable for exploration
- **Claude Max**: 20x usage multiplier at $200/mo
- **ChatGPT Pro**: $200/mo for power users

If you're experimenting, Gemini's free tier is a no-brainer. If you're shipping production code daily, the $200 tools pay for themselves in time saved. But the real cost isn't money—it's cognitive overhead from security anxiety.

## The Multi-Runtime Future

Here's the synthesis: we're entering an era where the *runtime* becomes the unit of work, not the agent.

OpenClaw's ACP (Agent Communication Protocol) makes this practical. You can now orchestrate across runtimes:
- **Claude Code** for deep context understanding
- **Codex sandbox** for risky filesystem operations  
- **Gemini** for free-tier exploration tasks

The agent doesn't need to be a monolith. It can be a coordinator, dispatching to the right runtime for each subtask.

This mirrors what we see in cloud infrastructure—polyglot persistence, specialized compute, composed workflows. The same pattern is emerging in AI tooling.

## What This Means for Practitioners

1. **Evaluate security architecture, not just benchmarks.** A tool that scores 90% but fails open under edge cases is riskier than one that scores 85% with kernel-level containment.

2. **Assume your AI tools will be exploited.** Not through malice, but through the inevitable complexity-collapse bugs that emerge in any sufficiently complex permission system. Design for containment, not just prevention.

3. **Consider multi-runtime workflows.** The best tool for the job depends on the job's risk profile. Deep reasoning tasks and risky operations have different optimal runtimes.

4. **Watch the failure modes.** How does each tool behave when its safety systems are stressed? Claude Code's regex exhaustion is a teachable moment—complex security logic has its own attack surface.

## The Bottom Line

The AI coding agent wars aren't just about intelligence—they're about trust boundaries. The winner won't just be the smartest model; it'll be the one that lets developers move fastest *without* accumulating security debt.

Codex CLI's kernel sandboxing, Claude Code's reasoning depth, and Gemini's transparency each represent valid bets on that trade-off. But after today's vulnerability disclosure, I'm paying a lot more attention to which tools fail closed.

---

*Sources: zylos.ai research on multi-runtime permission architectures, Daniel Vaughan's Terminal Agent Showdown (May 2026), Anthropic security advisories*