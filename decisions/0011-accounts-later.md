# 0011 — No accounts in v0; sign-in added later

**Date:** 2026-10-29
**Decided by:** proposed by an agent; not confirmed by Krischan
**Status:** proposed

## Context

Krischan asked whether the browser version means dealing with accounts, since users' information has to live somewhere. He knows Supabase and was considering Cloudflare (he clarified he meant D1 with SQLite, and R2).

## Proposal

- **v0:** no accounts. A display name and an emoji while seated; nothing stored on the server.
- **Extension:** the profile lives in the browser's own synced storage.
- **When needed** (purchases, lasting friend lists, bans): Supabase for sign-in only, D1 for data, R2 for files such as fan-drawn marks. The Cloudflare room checks the sign-in token.

## Why

- Nothing to build or secure for the first launch.
- Cloudflare has no consumer sign-in; Supabase gives Google, Twitch and Discord sign-in ready-made.

## Watch-outs

- Supabase free projects pause after a week without activity (checked 2026-10-29).
- Google sign-in for YouTube channel details may need Google's app review.

## Alternatives considered

- Reading YouTube cookies for identity (original handoff): dropped; store reviewers flag it and users distrust it.
- Building sign-in by hand on D1: more work and more risk.
