# 2026-10-29 — Oshi mark pixelation

**Method:** built the [Oshi Mark Lab](https://claude.ai/artifact/JMSpwBgLRE8UdYtxCirwnq) page so Krischan can compare emoji marks before and after pixelation on any device. Explained the algorithm when he asked to be sure it isn't AI-generated.

## Findings

### The algorithm (no AI)

A fixed recipe of standard image-processing steps. No model, no server call, no randomness: the same emoji on the same device gives the same pixels every time. For a 12×12 mark:

1. Draw the emoji with the device's normal emoji font on a hidden 48×48 canvas (ordinary text rendering).
2. Read back the 2,304 pixels.
3. Cut them into a 12×12 grid of 4×4 blocks (16 source pixels each).
4. A source pixel counts if it is more than half opaque. A block with fewer than 7 counted pixels becomes transparent. This gives hard edges.
5. A filled block takes the average color of its counted pixels.
6. Round each red, green and blue value to the nearest multiple of 32 (a small palette, chunky color steps).
7. Paint every empty pixel that touches a filled pixel (up, down, left, right) dark gray: a 1px outline.
8. Show the 14×14 result enlarged with nearest-neighbor scaling (`image-rendering: pixelated`).

In image-processing terms: block-average downscaling, alpha thresholding, uniform color quantization, and a one-pixel outline. 8×8 and 16×16 use the same steps with a different grid.

How to check it yourself: view the page source (the recipe is about 40 lines; the page loads only two Google Fonts); go offline and type a new emoji in the lab (still works, nothing leaves the device); reload (identical pixels).

The art underneath is the emoji itself, drawn by Apple's, Google's, Microsoft's or Samsung's designers. The code was written by an AI; see [decision 0004](../decisions/0004-no-ai-art.md#code).

### What the lab shows (expected, not yet confirmed by Krischan's tests)

- Simple shapes hold up: ⭐ 🌙 💎 🍓 🔥.
- Detailed ones (faces like 🐻 🐱, and 🐙) get muddy at 8×8 and 12×12. 16×16 is clearer but barely pixel art.
- Newer emoji (🫧) may not exist on older systems such as Windows 10; the lab flags "Not in color here".
- Friends on different systems see different source art (glossy Apple vs flat Microsoft).

### How the server handles marks (proposed)

The server only passes the emoji character itself. Every viewer's device draws it, so we never make, store or redistribute emoji images.

## What this means for the project

- Plain or pixelated marks is still Krischan's call, pending his device tests.
- If pixelation doesn't hold up, fan-drawn marks become the main look, with plain emoji as the fallback.

## Next steps

- Krischan tests the lab across devices and browsers (turn on link sharing to open it on devices not signed in).
- Record the result in [experience.md](../product/experience.md#oshi-marks) and close the question in [open-questions.md](../project/open-questions.md).
