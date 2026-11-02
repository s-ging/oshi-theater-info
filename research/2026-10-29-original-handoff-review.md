# 2026-10-29 — Original handoff review

**Method:** read the "Pixel Theater" handoff document Krischan brought from an earlier chat with another AI (kept verbatim in [files/2026-10-29-original-handoff.md](files/2026-10-29-original-handoff.md)), then reworked it with Krischan over the 2026-10-29 conversation.

## Findings

What the handoff specified, and what happened to each part. "Kept", "changed" and "dropped" reflect Krischan's answers unless marked as a proposal.

| Handoff said | Now | Why |
| --- | --- | --- |
| Name "Pixel Theater" | Dropped; name undecided | Krischan is not using it |
| Chrome, Firefox, Edge extension, day one | Changed: website first, extension later | [decision 0006](../decisions/0006-browser-first.md) |
| One global theater, 100-user cap, waitlist with email collection | Changed (proposed): rooms per stream, 72-seat theaters, overflow theaters, no waitlist | Friends need to sit together on the stream they're watching |
| No persistence, no localStorage | Changed (proposed): a few hundred bytes of synced browser storage in the extension | Remembering your party and mark needs it |
| Read YouTube cookies for channel, name, avatar | Dropped | Store reviewers flag it; fans distrust it ([decision 0011](../decisions/0011-accounts-later.md)) |
| 480×270 canvas, 12fps loop, 6fps in background | Changed: 256×192 per screen, draw only on change | [decision 0009](../decisions/0009-performance-budget.md) |
| 2.5D `rotateX(5deg)` tilt | Dropped | Blurs pixel art |
| Bird's-eye dots and 5×5 close-up, zoom switching | Changed: two DS screens | [decision 0007](../decisions/0007-two-screens-and-seating.md) |
| Regions ("Blue Region") instead of seat numbers | Changed: row letters A to F; regions may return for VCT's two sides | |
| "Sit beside" and group seating deferred to v2 | Changed: sitting with friends is the core | Krischan: that is the whole point |
| Node.js and uWebSockets, self-hosted, ngrok | Changed (proposed): Cloudflare Durable Objects | [decision 0010](../decisions/0010-server-on-durable-objects.md) |
| Client and server under 10MB RAM | Changed (proposed): measure what the extension adds | Browser overhead can't be cut |
| Typing speech bubbles, hover names | Kept | |
| Stream-end detection from the page | Kept for the extension | |
| Reconnect backoff 1s to 30s | Kept (not yet discussed again) | |
| Update toast "AppName updated to vX" | Not discussed again | |
| Akasupa and superchat integration deferred | Changed: wanted, v2 | |
| Organic discovery, no streamer outreach at first | Kept, with an indie VTuber partner as a bonus | |

## What this means for the project

The handoff's instruction to "not iterate on the spec" was overridden: Krischan chose to rework the vision ("you've captured what I wanted, even if it isn't the original vision that I had"). Files updated: everything in [product/](../product/).

## Next steps

- Leave the original file as history. Treat it as superseded wherever this table says so.
