# 0005 — A window beside the stream, never inside YouTube's page

**Date:** 2026-10-29
**Decided by:** Krischan
**Status:** accepted

## Context

The theater could be drawn on top of YouTube's player (by injecting into the page) or in its own window. An agent suggested a silhouette row of your party along the bottom of the video.

## Decision

The theater is always a separate window next to the stream: "just a visualizer for the seating." It never draws into or changes YouTube's page. Krischan: "I would prefer to draw a new window instead of messing with the DOM."

On desktop Chrome and Edge the window uses Document Picture-in-Picture so it stays on top, even when the stream is fullscreen (proposed by an agent, 2026-10-29). Elsewhere it's a normal popup.

The extension may **read** from YouTube's page (video ID, live state, the user's own sent chat), never write to it.

## Why

- YouTube is the heavy part of the tab; touching its layout costs performance.
- YouTube changes its page often; injected UI breaks.
- Capturing or re-embedding the video would be heavy and break YouTube's terms.

## Alternatives considered

- Silhouette row over the video: dropped, because it needs page injection.
- Pulling the video into our own canvas: not doable and against YouTube's terms.
