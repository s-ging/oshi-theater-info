**Welcome back!** Here's the full context and a handoff document for Claude.

---

## 📋 PROJECT CONTEXT: "Pixel Theater"

### The Core Idea
A **Chrome/Firefox/Edge browser extension** that displays a cute, minimal, **2D pixel-art theater** where VTuber viewers can "watch together." Think Nintendo DS Settings screen aesthetic meets a cinema. Viewers appear as pixel chips in seats, and the streamer (or anyone) can see their audience spatially.

### Key Constraints (Non-Negotiable)
- **100 user cap** (not 10k — waitlist for overflow)
- **Zero memory leaks** — target **<15MB RAM** client-side, **<10MB** server
- **12fps** render loop (intentional aesthetic + performance)
- **$0 hosting** (self-hosted initially, then free tiers like Oracle Cloud)
- **No persistence** — fresh session every time, no localStorage/disk
- **Canvas rendering only** (no DOM thrashing)
- **Livestreams only** (YouTube `/live` pages)
- **Cross-browser Day 1** (Chrome, Firefox, Edge)

---

## 🎯 THE VISION

### Visual Style
- **Pixel art** reminiscent of Nintendo DS settings screen
- **2.5D tilt** (CSS `rotateX(5deg)`) — theater seating perspective
- **Two views:**
  1. **Bird's Eye:** Everyone as 4x4px colored dots, "You" = golden marker
  2. **Close-Up:** 5x5 grid around you, 32x32px chips with avatars + names
- **View switching:** Zoom out/in effect via CSS transforms (NOT 3D renderer)
- **Regions:** Seats grouped (e.g., "Blue Region", "Red Region") instead of numbers

### The "Scale Down + Pixelate" Technique (NEW)
- Render at **480x270 internal resolution**
- Scale up to viewport via CSS `image-rendering: pixelated`
- **Memory drops to ~0.5MB for canvas** (vs 8MB at 1080p)
- **CPU <1%** at 12fps
- **Total client memory: <10MB**

---

## 🔧 TECHNICAL ARCHITECTURE

### Client (Browser Extension)
```
manifest.json (Manifest V3, cross-browser)
background.js (persistent WebSocket)
content.js (detects YouTube /live pages)
popup.html/js (mini-window widget)
theater.html/js (canvas renderer)
```

**Memory budget:**
| Component | Size |
|-----------|------|
| Canvas (480x270) | 0.5MB |
| Avatar cache (16x16, LRU 20) | 0.5MB |
| Seat data (100 seats) | 4KB |
| WebSocket buffer | 1MB |
| JS heap | 5-8MB |
| **Total** | **<10MB** |

### Server (Node.js + uWebSockets)
```javascript
// No Express, no Socket.io — raw uWebSockets
// Memory: <10MB for 100 concurrent users
const seats = new Map(); // seatId -> { channelId, displayName, avatarUrl, joinedAt }
const waitlist = [];     // emails for overflow
```

**Connection flow:**
1. Client connects → auto-assign seat
2. Server sends full state (100 seats)
3. Broadcast join/leave/typing events
4. **Heartbeat:** 15s ping, 60s timeout, 3 retries
5. **Stream end detection:** Client reads YouTube DOM → closes WS → no reconnect

---

## 🎨 INTERACTION (V1)

### What's In
- ✅ Auto-assign seat on join
- ✅ Hover shows viewer name
- ✅ **Typing indicator:** Speech bubble above seat when user chats
- ✅ View switching (button + mouse wheel zoom)
- ✅ Bird's eye + close-up views
- ✅ Region labels ("Blue Region")

### What's Deferred to V2
- ❌ "Sit beside" feature (mutual consent)
- ❌ Wave animations
- ❌ Seat selection (click to pick)
- ❌ Streamer spotlight
- ❌ Group seating
- ❌ Akasupa/superchat integration

### Edge Cases
| Scenario | Solution |
|----------|----------|
| No YouTube cookie | Guest mode (generic avatar), retry |
| YouTube API change | Graceful error: "YouTube is being fussy" |
| Network issues | Exponential backoff (1s, 2s, 4s, 8s, max 30s) |
| Stream ended | Detect via DOM → close WS → no reconnect |
| Tab inactive | Throttle to 6fps |
| Multiple streams | Handle both tabs independently |
| Rapid reconnect | Recall seat if available |

---

## 📋 WAITLIST STRATEGY

- **100 users cap** (not a queue — hard cap)
- When full → "Theater Full" screen
- **Collect email** for notifications (Resend integration, user handles)
- **No in-app queue** (would wreck UX)
- **Public link** for first 100
- **Organic discovery** (no streamer outreach initially)

---

## 🚀 DEPLOYMENT

- **Self-hosted** initially (user's machine, 10 users: user + GF + friends)
- **Cloudflare Worker** as proxy (SSL, DDoS)
- **`wss://`** required (Chrome extension needs HTTPS)
- **No domain yet** — IP or ngrok
- **Git** for rollback
- **No monitoring/logging** except: user count, watch hours, most-used channel
- **Update toast:** "AppName updated to v1.26.9! Patch notes" (DOM toast, not new tab)

---

## 📅 DEVELOPMENT PHASES

### Phase 1: Core (Week 1)
- [ ] Extension skeleton (Manifest V3, cross-browser)
- [ ] YouTube cookie reader (channel ID, name, avatar)
- [ ] Canvas renderer (480x270 → pixelated scale up, 12fps)
- [ ] Bird's eye view (dots)
- [ ] WebSocket client (uWebSockets)

### Phase 2: Interaction (Week 2)
- [ ] Server (Node + uWebSockets + seat management)
- [ ] Close-up view (5x5 grid)
- [ ] View switching (button + mouse wheel)
- [ ] Typing indicator (speech bubbles)
- [ ] Heartbeat + reconnection
- [ ] Stream detection

### Phase 3: Polish (Week 3)
- [ ] Waitlist (email collection)
- [ ] 100-user cap
- [ ] Cross-browser testing
- [ ] Memory profiling + leak hunting
- [ ] Soft launch (user + GF + friends)
- [ ] Twitter launch

---

## 🎯 THE CHALLENGE

**Build this with:**
- **Client:** <10MB RAM (target 8MB)
- **Server:** <10MB RAM
- **100 users** (capped)
- **$0** hosting
- **12fps** pixel art
- **Zero leaks** (heap snapshots verified)
- **Cross-browser** Day 1

**No over-engineering. No bloat. Just a tight, pixel-perfect theater.**

---

## 🤝 HANDOFF TO CLAUDE

**Claude, here's what you're inheriting:**

1. **A fully-specified project** with clear constraints
2. **A working mental model** of the architecture (extension + uWebSockets server + canvas pixel art)
3. **A performance-first philosophy** (pixelation for zero-cost rendering, <10MB everything)
4. **A phased roadmap** (3 weeks, core → interaction → polish)
5. **A "challenge accepted" mentality** — the user wants you to push back if something is over-engineered

**Your first task:** Start with Phase 1, Step 1 — the cross-browser `manifest.json` and extension skeleton. Ask clarifying questions if anything is ambiguous, but **do not iterate on the spec** — the user explicitly said "front load the thinking" and wants execution now.

**Key files to create first:**
```
pixel-theater/
├── manifest.json          # Cross-browser V3 manifest
├── src/
│   ├── background.js      # WebSocket service worker
│   ├── content.js         # YouTube /live detection
│   ├── popup/
│   │   ├── popup.html
│   │   └── popup.js
│   └── theater/
│       ├── theater.html
│       ├── theater.js     # Canvas renderer
│       └── theater.css
├── server/
│   ├── server.js          # uWebSockets server
│   └── package.json
└── README.md
```

**Claude — the user is ready to build. Go.** 🎭