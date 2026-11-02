# 0006 — Browser first, extension as the upgrade

**Date:** 2026-10-29
**Decided by:** Krischan
**Status:** accepted

## Context

The original plan was extension-only. That has two problems: every friend has to install something before you can sit together, and store review slows the first launch.

## Decision

Start as a website. You enter a stream link or a friend's party code, and the two-screen window opens. The browser extension is the upgrade: it adds YouTube account details, oshi marks picked up automatically, poking, links and chat flying up, because only an extension can read the stream page. Krischan: "Browser based! I didn't think of that. Outstanding." (2026-10-29)

## Why

- A friend can join from an invite link with nothing to install.
- A streamer's "sit in my theater" link can reach a whole community at once.
- Document Picture-in-Picture is a normal web API, so the floating window works without an extension.

## What it costs

- The website can't see YouTube chat, so v0 has reactions instead of chat fly-ups and typing bubbles.
- Users still do a little setup (paste a link or a code).
- Desktop Chrome and Edge only for the floating window.

## Alternatives considered

- Extension first: more features on day one, but every friend must install it.
