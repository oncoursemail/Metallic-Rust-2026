# Roadmap — one-week sprint

Target: a **self-hosted, playable** 2026 Rec Room client on our own Rust backend within ~1 week,
plus the foundation for the from-scratch Rust client (ongoing).

Each item below maps to a GitHub issue under a milestone.

## Milestone 1 — Backend: logged-in & settled (Days 1–2)
Status: **in progress** (client already logs in and reaches the menu)
- Fix post-login re-auth loop — correct JWT claims / `account/me` shape so the session sticks
- `account/me`, `account/{id}`, `/home/me`, `/me/config/v3`, privileges/restrictions
- `player/login`, `player/heartbeat`, `player/qos`, connection-info
- econ: balance, `avatar/v4/items`, `defaultunlocked`, outfits
- rooms REST: `publishState/configs`, room lists, room details
- notify hub negotiate (SignalR handshake) returns something the client accepts
- **Done = client sits stably in the menu, no loop, no "create account"**

## Milestone 2 — Realtime: join a room (Days 2–4)
Status: not started — the big one
- Reverse the realtime transport (`live`/`tachyon`): protocol, framing, auth
- `tachyon` Rust server: accept connection, auth with our JWT, room session create/join
- Minimal room: spawn the local player into an empty room (Dorm)
- **Done = client loads into a room served by us**

## Milestone 3 — Standalone deploy (Day 4)
- hosts redirect of `*.nodeline.net` → local, with Defender exclusion handled
- trusted leaf cert served by `rrserver` (no mitmproxy middleman)
- one-command launch script
- **Done = launch NodeNet → straight into our stack, no proxy**

## Milestone 4 — Decomp/analysis foundation (Days 3–5, parallel)
- type/method inventory for the gameplay/networking subsystems (local only)
- document the room/realtime message types and the economy/account models
- **Done = we can look up any system's types without re-dumping**

## Ongoing / stretch (not on the week's critical path)
- Full realtime simulation parity (physics, voice, avatars, interactions)
- From-scratch Rust client (engine choice: Bevy or custom) — the long pole
- Gameplay improvements & modding hooks

---

### Reality check
The server + a playable self-hosted client this week is realistic (we're already most of the way).
A *complete* from-scratch Rust client is not a one-week thing — it's tracked as the ongoing track so
it never blocks shipping the playable stack.
