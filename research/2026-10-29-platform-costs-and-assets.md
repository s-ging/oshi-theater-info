# 2026-10-29 — Platform costs, limits and emoji sets

**Method:** read vendor pricing pages and GitHub repositories during the 2026-10-29 conversation. Prices and limits change; re-check before relying on them.

## Findings

### Cloudflare Durable Objects

Source: [developers.cloudflare.com/durable-objects/platform/pricing](https://developers.cloudflare.com/durable-objects/platform/pricing) and [/limits](https://developers.cloudflare.com/durable-objects/platform/limits), read 2026-10-29.

- Workers Free plan: only SQLite-backed Durable Objects. 100,000 requests per day, 13,000 GB-s per day. Going over fails with an error; limits reset at 00:00 UTC.
- Paid plan: 1 million requests per month included, then $0.15 per million. 400,000 GB-s per month included, then $12.50 per million GB-s. Pricing examples assume a $5 monthly minimum.
- Requests include HTTP requests, RPC sessions, WebSocket messages and alarms. Opening a WebSocket is one request.
- Outgoing WebSocket messages are free. Incoming are billed 20 to 1 (100 messages = 5 requests). Incoming protocol pings are free.
- `setWebSocketAutoResponse` replies add no billed time.
- Objects that are idle and eligible for hibernation are not billed for duration. Hibernation needs no pending timers, fetches or requests, and the Hibernation WebSocket API.
- Up to 32,768 WebSocket connections per object (practical limit lower).
- In-memory state is lost on hibernation; per-socket data must be kept with `serializeAttachment()`.
- Free plan: 5 GB total Durable Object storage per account.

### Supabase

Source: [supabase.com/pricing](https://supabase.com/pricing.md), read 2026-10-29.

- Free plan: 50,000 monthly active users, 500 MB database per project, up to 2 active projects; projects pause after one week without activity.
- Pro plan: from $25 a month, 100,000 monthly active users included, then $0.00325 each.

### Pixel emoji sets Krischan found

- [linusg/serenityos-emoji-font](https://github.com/linusg/serenityos-emoji-font): a TrueType font of the SerenityOS pixel emoji, with flags and ZWJ combinations; ships a TTF and CSS. The license type was not confirmed from the page; check the repository's LICENSE before any use.
- [R74nCom/R74moji-Essentials](https://github.com/R74nCom/R74moji-Essentials): 85 stickers (the full R74moji set at [r74n.com/moji](https://r74n.com/moji/) has over 1,000). Licensed CC-BY-SA-4.0; the share-alike term can extend to assets built from it, a problem for anything sold. Krischan found them "a little big".
- Krischan's view: hand-maintaining a pixel emoji pack is tedious, and AI-made packs won't fly with the fandom.

### A possible partner (not pursued)

- A 2023 article described one local VTuber Krischan mentioned as independent, streaming on Twitch, mostly Valorant ([vtubernewsdrop.com](https://vtubernewsdrop.com/onlive-convention-hosts-vtubers-pan-the-bread-kitsui-akira-kometas-elaine-and-virgil/)). May be out of date. Krischan later said not to focus on specific VTubers for now.

## What this means for the project

- The free plan covers a soft launch; even a busy first month is estimated at $5 to $20 ([architecture](../product/architecture.md#costs)).
- One Durable Object per stream is the cost lever ([decision 0010](../decisions/0010-server-on-durable-objects.md)).
- No emoji pack adopted; oshi marks use the device's own emoji ([experience](../product/experience.md#oshi-marks)).
- Twitch support matters if the first partner streams on Twitch.

## Next steps

- Re-check Cloudflare and Supabase pricing before building.
- Confirm the SerenityOS emoji license if it's ever considered.
