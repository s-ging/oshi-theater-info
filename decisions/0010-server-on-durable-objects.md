# 0010 — Server on Cloudflare Durable Objects, one per stream

**Date:** 2026-10-29
**Decided by:** proposed by an agent; not confirmed by Krischan
**Status:** proposed

## Context

The original handoff planned a self-hosted Node.js server with uWebSockets behind ngrok, then free cloud tiers, with one global 100-seat theater.

## Proposal

- A Cloudflare Worker with one Durable Object per stream (keyed by YouTube video ID).
- Theaters of 72 seats are sections inside that object; each viewer only receives updates for their own section; parties are kept together.
- WebSocket Hibernation API, with `setWebSocketAutoResponse` for pings.
- No database in v0.

## Why

- Hibernating objects aren't billed for duration, and a quiet theater is idle most of the time.
- Outgoing messages are free; incoming are billed 20 to 1.
- One object per stream instead of per theater keeps the bill near the $5 minimum (estimate: [architecture.md](../product/architecture.md#costs)).
- No server to run on someone's machine, no tunnel, TLS included.

## Alternatives considered

- Self-hosted Node.js and uWebSockets (original handoff): more work to run and keep online.
- One Durable Object per theater: simpler code, but about 4 times the cost.
