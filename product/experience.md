# Experience

How the window looks and behaves. Last updated: 2026-11-03.

Mockups (private claude.ai artifacts; links in [map/accounts.md](../map/accounts.md#mockups-and-tools)): the theater window, the window beside a stream, the neighbor card, the landing page, and the oshi mark lab.

"Krischan" marks what he decided. "Proposed" marks agent suggestions he has not confirmed.

## The window

- A separate window beside the stream, never drawn inside YouTube's page. (Krischan)
- Two screens stacked like a DS, each 256×192 art pixels, shown at a whole-number scale (2× = 512×384 per screen). (Krischan agreed to the real DS resolution, "just scale up", 2026-10-29)
- On desktop Chrome and Edge it opens as an always-on-top Document Picture-in-Picture window, so it stays visible when the stream is fullscreen. Other browsers get a normal popup window. (proposed 2026-10-29)

## Top screen: the theater

- Header: LIVE badge, stream time, seats filled out of the total.
- Stage across the full width of the screen, in the oshi's color. (Krischan, 2026-10-29)
- No exit signs. (Krischan, 2026-10-29)
- Seating: 6 rows (A to F), each row two blocks of 6 seats with an aisle between them, so 72 seats per theater. Rounded squares in straight rows. (Krischan, 2026-10-29)
- Dropped, do not bring back without asking: circle seats, curved rows, staggered rows. Krischan: "too many things at a time". An optional "depth" variant (front rows slightly bigger) exists in the mockup as a switch, off by default, undecided. ([decision 0007](../decisions/0007-two-screens-and-seating.md))
- Seat colors: you (gold), your party (mint), other viewers (soft pastels), empty (white). Same shape, different color and border, so the legend reads at a glance.
- Typing bubbles appear above seats. Krischan loved these. (2026-10-29)
- Rooms are per stream; your party sits together and strangers watching the same stream fill the other seats. A full theater opens another one ("screening 2"). (proposed 2026-10-29)
- The original handoff's single global 100-seat theater and waitlist are replaced by this. (see [research](../research/2026-10-29-original-handoff-review.md))

## Bottom screen: your party

- Header: party code, how many are here and away.
- Your party up close: avatar, name, oshi mark badge, and state above the head.
- Presence states: typing, here, away, and you. Krischan liked how these read. (2026-10-29)
- "Nearby" panel: someone a few seats away waves at you; you can wave back. (proposed 2026-10-29)
- Buttons: Leave party, Copy invite.

## Chat flying up (extension only)

When someone in your party sends a chat message on YouTube, it rises from their seat on the bottom screen, goes behind the DS frame at the hinge, and comes out on the top screen. It moves straight up, holds a moment, then fades over a random amount of time. (Krischan, 2026-10-29)

Proposed details (2026-10-29):

- The sender's own extension announces the message (it already sees them hit send). Nobody's extension scans the whole live chat.
- Only the first ~40 characters travel. Members-only emotes are images, so they show as a placeholder or are skipped.
- One flying message per person at a time, queued, so a fast chatter can't flood the top screen.
- Steps at 12 frames per second while moving; nothing runs when nothing moves.

## Oshi marks

Fans already put their oshi's emoji at the end of their display names. The mark shows on your seat.

- No hand-made emoji pack to maintain. Krischan wants as little upkeep as possible. (2026-10-29)
- Option A: the device's own emoji, shown as is.
- Option B: the device's own emoji, shrunk to pixels on the device by a fixed algorithm (block average, alpha threshold, color quantization to steps of 32, 1px outline). No AI. Explained in the [lab research note](../research/2026-10-29-oshi-mark-pixelation.md).
- Krischan doesn't fully trust B yet and is testing it across devices in the oshi mark lab. Undecided. ([open questions](../project/open-questions.md))
- Later: fandoms submit hand-drawn pixel marks, credited to the artist, free, reviewed before going live. (Krischan liked the idea, 2026-10-29)
- The extension could pre-fill the mark from the emoji at the end of your YouTube display name. (proposed 2026-10-29)

## Connections and waving

- A connections tab like a Discord profile: links people paste in, so people watching alone can make friends. (Krischan, 2026-10-29)
- Poke or wave someone nearby, then take the conversation somewhere else. (Krischan, 2026-10-29)
- Proposed safety rules (2026-10-29): your card shows only to your party automatically, and to a stranger only after you both wave; links limited to known platforms (X, Bluesky, Twitch, YouTube, Discord, Pixiv and similar), never any URL; a "Hide my card" button. See [safety.md](safety.md).

## Reactions

- Superchats and akasupa (red superchats) are a big part of YouTube streams and need to show up somehow, maybe as a square literally throwing money at the oshi. (Krischan, 2026-10-29)
- Throwing tomatoes when a streamer's joke bombs would be funny. (Krischan, 2026-10-29)
- Proposed (2026-10-29): superchats are detected locally from the chat each viewer already sees, so they cost no server work; tinted by tier; memberships could be confetti. Penlights in the oshi's color as the default fan reaction (idol and VTuber concert culture). Tomatoes only where the streamer turns them on, because on stream a raid could abuse them. Bursts of the same reaction merge into one effect.
- Proposed for v0 (2026-11-02): a few reaction buttons (草, 👏, penlight, 😭) that pop above your seat. Without the extension the site can't see chat, so this is what makes the room feel alive.

## Avatars

- v0 has no illustrated avatars: seats are colored squares, the party shows marks and names. (proposed 2026-11-02)
- Custom avatars in v2 or v3, possibly editable so artists can take part. (Krischan, 2026-10-29) A 16×16 editor in the spirit of PictoChat was suggested.
- The chibi sprites, stage star and curtains in the mockups are AI placeholders and must not ship ([decision 0004](../decisions/0004-no-ai-art.md)).

## Dropped ideas

- **Silhouette row over the video** (party as silhouettes along the bottom of the player): dropped 2026-10-29 because it needs drawing inside YouTube's page. Krischan prefers his own window.
- **2.5D CSS tilt** (`rotateX`) from the original handoff: dropped 2026-10-29; it blurs pixel art. Krischan: "the vision is blurry" on that one.
- **Bird's-eye and close-up views with zoom**: replaced by the two screens.
- **Curved, staggered, circular seating**: tried and rejected 2026-10-29.
