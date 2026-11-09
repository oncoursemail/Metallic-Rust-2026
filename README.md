# Metallic-Rust-2026

A fully independent, **from-scratch Rust reimplementation** of Rec Room's **2026** build
(`20260323.14`) — our own backend server, our own game client, and our own client loader, all
written in original Rust — for **preservation and open gameplay development** after the official
shutdown.

The goal is a self-hostable stack we **fully own and can change any way we want**: run it, fix it,
and rework the gameplay. Every component here is our own original code. Nothing in this repo is
copied from Rec Room or from any third-party revival project.

> **Status:** the Rust backend serves the boot sequence and OAuth2 login, and a client reaches the
> menu against it. See the [Progress Board](#progress-board).

---

## Goals

- **Preserve the 2026 build.** Keep a self-hosted stack playable after the official servers go dark.
- **Own the whole stack.** A backend, a client, and a loader we can modify freely — no dependence on
  anyone else's servers, revivals, or hosting.
- **Open gameplay development.** A clean base for modding, experimentation, and new gameplay once the
  core is up.

---

## Architecture

All three components are original Rust, built and maintained in this project. (The loader is
circumvention-adjacent tooling and is developed separately — it is **not** part of this public repo.)

```
   ┌──────────────┐        ┌────────────────────────┐        ┌──────────────────────────┐
   │  loader      │        │  server (Rust)         │        │  realtime server (Rust)  │
   │  (our Rust,  │  ───▶  │  HTTPS REST backend     │        │  room sim + networking   │
   │   local-only)│        │  name/boot, OAuth2,     │        │  (planned)               │
   │              │        │  account, econ, rooms   │        │                          │
   └──────────────┘        └────────────────────────┘        └──────────────────────────┘
```

| Component | What it is | In this repo? |
|-----------|------------|---------------|
| `server`  | our Rust REST backend (name/boot, OAuth2, account, economy, rooms) | yes — `server/` |
| realtime  | our Rust realtime room server (room sim + networking) | planned |
| client    | our from-scratch Rust game client (the long pole) | planned |
| loader    | our Rust client loader — local-only circumvention tooling | **no, kept local** |

### Repo layout

| Path | What |
|------|------|
| `server/` | our Rust REST backend |
| `docs/`   | roadmap and our own original write-ups (no copyrighted content) |

---

## Principles

- **Fully independent.** This is a from-scratch reimplementation. We do **not** use, fork, or
  incorporate **RecFlare** or any other revival's server or client code. Our stack is entirely our
  own. RecFlare's open-source server is consulted **only** as a reference for the *shape* of Rec
  Room's endpoints and responses (what routes exist, what fields a response carries) — its code is
  **never** copied into this project.
- **Decompile locally to understand, then reimplement in original Rust.** We decompile the owned
  2026 build **on our own machines** to understand how each system works, then write **original
  Rust** that reimplements that behavior. The reimplementation is ours to modify freely; a verbatim
  transpile of Rec Room's code would not be, so we never do that.
- **Copyrighted artifacts stay local.** Rec Room's code, decompiled source, IL2CPP metadata, assets,
  and captured payloads are **never** committed (see `.gitignore`). The public repo holds only our
  own original code and docs. Our client ships original/replacement assets or loads the user's own
  copy — it never redistributes Rec Room's assets.

---

## Progress Board

**Target: a self-hosted, playable 2026 client on our own Rust backend.**

### ✅ Done
- [x] Normalized the owned 2026 build locally into a tool-loadable form for study
- [x] Mapped the backend API surface (name/boot sequence and login flow)
- [x] Rust `server` serving the boot sequence over TLS
- [x] Client runs the full boot sequence against our server
- [x] OAuth2 `connect/token` login with a JWT session — client **reaches the menu**

### 🔜 This week
- [ ] Fix the post-login re-auth loop (JWT/account shape) → stable logged-in session
- [ ] Flesh out account / player / econ / rooms REST so the client settles in the menu
- [ ] Join a room: implement the realtime handshake → load into a room
- [ ] Standalone deployment: our loader + trusted cert, no third-party proxy in the path
- [ ] Analysis foundation: generate a local type/method inventory for gameplay systems

### 🧭 Ongoing / stretch
- [ ] Full realtime room simulation parity
- [ ] From-scratch Rust client
- [ ] Gameplay improvements & open modding

See [`docs/ROADMAP.md`](docs/ROADMAP.md) for detail, and [`CONTRIBUTING.md`](CONTRIBUTING.md) to pick
up an issue. Issues and milestones track each task.
