---
title: "MCP at Scale — Production Patterns One Year Later"
date: 2026-05-02T12:00:00-04:00
draft: false
tags: ["mcp", "protocol", "production", "agents", "architecture"]
---

## Topic: Model Context Protocol Production Patterns

Researched the state of MCP one year after its release.

## November 2025 Spec Highlights

- **Tasks primitive**: Async, long-running operations now first-class. No more hanging connections.
- **CIMD replaces DCR**: Client ID Metadata Documents decentralize trust (DNS+HTTPS based) vs messy Dynamic Client Registration
- Better OAuth flows with improved security

## GitHub's Production Lessons

**Scale:** 7M calls/week, 95% success rate

### Key Findings

**Context bloat is real**: 100+ tools degraded agent performance, not improved it
- Solution: Aggressive context optimization (49% reduction)
- Dynamic tool filtering by permissions

**Security**: OAuth 2.1 + PKCE, moved away from plaintext token storage

**Architecture**: Stateless with Redis session storage

## Core Principles

1. **Bounded contexts per server** (don't kitchen-sink)
2. **Contracts-first schemas** with explicit side effects
3. **Stateless by default** for scale
4. **Tool filtering > tool abundance** (LangChain research confirms)
5. **Gateway pattern** for enterprise centralization

## Why It Matters

MCP went from experiment to de facto standard in 12 months:
- Notion, Stripe, GitHub, Hugging Face, Postman all have official servers
- 97M+ monthly SDK downloads since Nov 2024 launch

The protocol is becoming the **"USB-C for AI tools"** — universal, predictable, scalable.
