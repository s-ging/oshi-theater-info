# Architecture

How it is built and what it costs. Last updated: 2026-11-03.

Almost everything here is **proposed** by an agent (2026-10-29 to 2026-11-02). What Krischan stated or accepted is marked. Prices and limits come from vendor pages on the date shown; re-check before relying on them ([research](../research/2026-10-29-platform-costs-and-assets.md)).

## Shape

```
YouTube tab (the stream)      Our window (website or extension)       Cloudflare
-----------------------       ---------------------------------       ----------
                              two 256×192 screens, drawn on change  <-> Worker
extension only: reads                                                   └─ one Durable Object per stream
live state, video ID,         party code, presence, reactions             (rooms, sections of 72 seats,
your own sent chat  ------->  chat fly-ups                                  parties, WebSocket hibernation)
```

- **Website (v0):** paste a YouTube live link or a party code. The page parses the video ID; the room is keyed by it. No video is embedded or captured. (Krischan chose browser-first, 2026-10-29)
- **Extension (later):** reads only. It never writes to YouTube's page. (Krischan: "I do not want to manipulate the DOM", 2026-10-29)
- **Server:** Cloudflare Worker plus one Durable Object per stream; theaters of 72 seats are sections inside it, and each viewer only receives updates for their own section. (proposed; [decision 0010](../decisions/0010-server-on-durable-objects.md))

## Performance budget

Krischan wants maximum performance gains "whatever means necessary" without trading UX (2026-10-29), and his standing rules: cheapest correct thing with a number on it, idle costs nothing, old hardware is the target (2026-11-02). Accepted items (Krischan said yes or ok on 2026-10-29) are marked ✓.

| Rule | Why | Status |
| --- | --- | --- |
| No fixed render loop. Redraw only when something changes; a short timer runs only while an animation plays. A quiet theater uses zero CPU. | A 12fps loop still wakes the CPU 12 times a second with nothing to draw. | ✓ |
| Real DS resolution: 256×192 per screen, whole-number scaling only (`image-rendering: pixelated`). | Every pixel stays the same size; smaller than the handoff's 480×270. | ✓ |
| No CSS 3D tilt. Perspective, if any, is drawn into the art. | Tilting pixel art blurs it. | ✓ |
| Avatars fetched once, shrunk to 16×16, reduced to a small palette; only the tiny bitmap is kept. | Memory and draw cost stay flat. | ✓ (custom avatars come later) |
| Leave YouTube's page alone. | YouTube is the heavy part of the tab; never trigger its layout. | ✓ |
| Binary protocol: a seat change fits in a few bytes, "typing" is one bit, sent at most once a second. | Bytes and wakeups. | ✓ |
| Heartbeat under 30 seconds; pings answered by `setWebSocketAutoResponse` without waking the Durable Object. | Chrome stops an idle extension service worker after about 30 seconds; auto-responses are not billed. | ✓ |
| Presence sent only on change, never on a timer. | Lazy over live. | proposed |
| Measure what the extension adds, not the browser's total memory. | Chrome's own per-extension overhead can't be cut. | proposed |

To do: put numbers on each (bytes per message, wakeups per minute per viewer, cost per viewer-hour) once the protocol is written.

## Costs

Cloudflare Durable Objects pricing, read 2026-10-29 from developers.cloudflare.com:

- Workers Free plan: SQLite-backed Durable Objects only, 100,000 requests per day, 13,000 GB-s duration per day.
- Paid plan: 1 million requests per month included, then $0.15 per million; 400,000 GB-s per month included, then $12.50 per million GB-s. $5 monthly minimum.
- Outgoing WebSocket messages are free. Incoming messages are billed 20 to 1. Auto-responses are free. Objects idle and eligible for hibernation are not billed for duration.

Estimate (agent, 2026-10-29), not measured: 2,000 viewers across 5 streams, about 3 hours a day.

- One Durable Object per stream: about 200,000 GB-s a month, inside the included amount. Close to the $5 minimum.
- One Durable Object per 72 or 100-seat theater: about 4 times as many objects, roughly $15 to $20 a month.

Correction: an earlier estimate said a 15-second heartbeat from 100 people (576,000 messages a day) would break the free plan's 100,000 requests a day. With 20-to-1 billing that is about 28,800 requests, and auto-response pings cost nothing, so it fits.

## Accounts and storage

- **v0: no accounts.** A display name and an emoji while seated; nothing saved on the server; a room forgets everything when it empties. (proposed 2026-11-02; [decision 0011](../decisions/0011-accounts-later.md))
- **Extension:** your profile (name, mark, links, party) lives in the browser's own storage (`chrome.storage.sync`), which syncs across your computers. A few hundred bytes. (proposed 2026-10-29) This replaces the handoff's "no persistence" rule, which conflicted with having friends.
- **When accounts are needed** (purchases, lasting friend lists, bans): Supabase for sign-in only, D1 (SQLite) for data, R2 for files such as fan-drawn marks. Krischan knows Supabase and was weighing it against Cloudflare D1 (2026-10-29). Cloudflare has no consumer sign-in, so login would otherwise be built by hand.
- **YouTube identity:** do not read YouTube cookies (store reviewers flag it and fans distrust it). Take the name from the page, let people choose, or later use Google sign-in for the channel name and avatar, which may need Google's app review. (proposed 2026-10-29; Krischan: "yep no need")

## Platforms

- **Document Picture-in-Picture:** Chrome and Edge on desktop. Firefox and Safari get a normal popup that doesn't stay on top.
- **Firefox extension:** runs Manifest V3 extensions on background scripts, not service workers. Test it separately.
- **Phones:** iOS does not let any app draw over the YouTube app. Android does, with the overlay permission. Safari on iPhone and iPad supports web extensions, which reaches people who watch in the browser.
- **Discord:** Activities are web apps in an iframe, so the renderer would port over, but the video isn't ours to embed there; the theater would sit next to the stream, not around it.
- **Twitch:** not planned for v0. Needed early if the first streamer partner streams on Twitch.
- **OBS (v3, parked):** a streamer's view would be a read-only page subscribed to the room, added as a browser source. Analytics need the streamer to sign in.

## Code

The code repository does not exist yet. Keep code out of this knowledge base; record its location in [map/accounts.md](../map/accounts.md) once created.
