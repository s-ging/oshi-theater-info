# Scope: v0, the weekend launch

Proposed by an agent on 2026-11-02 after Krischan asked how to turn this into a weekend project and launch it. **Not started.** Waiting on Krischan's go-ahead.

## The question v0 answers

Does a group of friends keep the window open for a whole stream? If yes, the extension is worth building. If not, we learn what's missing cheaply.

## What v0 is

Browser-only. No extension, no accounts.

1. **Join:** open the site, paste a YouTube live link or a friend's party code, type a name and pick an emoji. The two-screen window pops out beside the stream (Document Picture-in-Picture on desktop Chrome and Edge; a normal popup elsewhere).
2. **Top screen:** the theater for that stream. Your party sits in one row; strangers are seats without names.
3. **Bottom screen:** your party up close with names, marks, and here or away.
4. **Reactions:** a few buttons (草, 👏, penlight in the oshi's color, 😭) that pop above your seat. Bursts merge.
5. **Away:** a "brb" button, and automatically when someone closes the window. The site can't see whether you're watching the YouTube tab.
6. **Server:** one Cloudflare Worker, one Durable Object per stream. Nothing saved; a room forgets everything once it empties. The free plan covers a soft launch.

## Prerequisites

- **Art:** nothing blocks, because v0 has no illustrated avatars. Seats are colored squares; the party shows emoji marks and names; the stage shows the oshi's emoji. All AI placeholder sprites are dropped.
- **Marks:** plain emoji (zero risk) or pixelated, from the lab results.
- **Name and domain:** only needed before the public launch. A soft launch can run on a free Cloudflare address.
- **Testers and a stream:** 3 to 5 friends and one scheduled stream.
- **Privacy note:** a display name and an emoji while seated; nothing after.
- **Safety basics:** see [safety.md](../product/safety.md#v0-browser-version).
- **Who writes the code:** if an AI writes it, the promise is "no AI art", not "no AI anywhere".
- **Browser limits:** the floating window works only in desktop Chrome and Edge; v0 is desktop-only.

## Schedule (estimate)

- **Day 1:** build v0: room server, site, pop-out window with both screens, party codes, reactions. Test locally with several simulated viewers in one room. Krischan deploys with `npx wrangler deploy` from his Cloudflare login.
- **Weekday evenings:** Krischan and a friend try it; ask the cousin about the name.
- **Saturday:** fixes from testing; turn the landing page mockup into the real home page; privacy note; domain if named.
- **Sunday:** the launch is a watch party: friends in one theater for a real stream, then post a clip of the window.

## Out of scope for v0

The extension, chat flying up, typing bubbles, waving and cards, accounts (Supabase, D1), superchats, cosmetics, Twitch, phones, the OBS view. See [roadmap.md](roadmap.md).
