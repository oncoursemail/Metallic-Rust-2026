# Metallic-Rust-2026

A clean-room **Rust** reimplementation of Rec Room's **2026** build (`20260323.14`) — backend first,
client next — for **preservation and open gameplay development** after the official shutdown.

The goal: a self-hostable stack we fully control, so we can run the game, fix it, and change the
gameplay.

> **Status (updated live):** the backend is up and the official 2026 client **logs in and reaches
> the menu against our Rust server**. See the [Progress Board](#progress-board).

---

## Legal / clean-room

This repository contains **only our own original code and documentation.** It does **not** contain
Rec Room's game code, decompiled source, IL2CPP metadata, assets, or captured response payloads —
those are copyrighted, stay local/private, and are excluded via `.gitignore`. Reverse-engineering is
done against a legally-owned copy for interoperability and preservation; the Rust code here is an
independent reimplementation of the observed protocol, not a copy of Rec Room's code.

---

## Architecture

```
            ┌────────────────────────┐        ┌──────────────────────────────┐
  Client ──▶│  rrserver (Rust)       │        │  tachyon (Rust)              │
  (2026)    │  HTTPS REST backend    │        │  realtime room server        │
            │  NameServer, OAuth2,   │        │  (room sim + networking)     │
            │  account, econ, rooms  │        │                              │
            └────────────────────────┘        └──────────────────────────────┘
```

- **Phase 1 client:** the official 2026 client, patched to talk to our backend (via the existing
  NodeNet/`nodeline` loader during bring-up).
- **Phase 2 client (stretch):** a from-scratch Rust client. This is the long pole — tracked but not
  on the one-week critical path.

## Repo layout (planned)

| Path | What |
|------|------|
| `server/`  | `rrserver` — the Rust REST backend |
| `tachyon/` | the Rust realtime server |
| `docs/`    | protocol notes, roadmap, our own RE write-ups (no copyrighted content) |
| `tools/`   | local-only helpers (metadata reader, capture scripts) — gitignored where they carry game data |

---

## Progress Board

**Sprint target: ≤ 1 week to a self-hosted, playable 2026 client on our Rust backend.**

### ✅ Done
- [x] Cracked the 2026 IL2CPP metadata (v31) — normalized, tool-loadable
- [x] Captured + decoded the live backend API (NameServer map + boot sequence)
- [x] Rust `rrserver` serving the boot sequence over TLS
- [x] Real client runs the full boot sequence against our server
- [x] OAuth2 `connect/token` login with a JWT session — client **reaches the menu**

### 🔜 This week
- [ ] Fix the post-login re-auth loop (JWT/account shape) → stable logged-in session
- [ ] Flesh out account / player / econ / rooms REST so the client settles in the menu
- [ ] Join a room: implement the realtime (`tachyon`) handshake → load into a room
- [ ] Standalone deployment (hosts redirect + trusted cert, no mitmproxy middleman)
- [ ] Decompile/analysis foundation: generate type/method inventory for gameplay systems

### 🧭 Ongoing / stretch
- [ ] Full realtime room simulation parity
- [ ] From-scratch Rust client
- [ ] Gameplay improvements & open modding

See [`docs/ROADMAP.md`](docs/ROADMAP.md) for detail. Issues/milestones track each task.
