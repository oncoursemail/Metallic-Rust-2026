# Contributing

Thanks for helping preserve the 2026 build. This project is an independent, from-scratch Rust
reimplementation — everything we ship is our own original code. A few rules keep it that way.

## Picking up an issue

1. Browse the [open issues](../../issues) and milestones. Pick one that's unassigned.
2. Comment on the issue to claim it, then open a branch and work there.
3. Open a pull request referencing the issue. Keep PRs focused — one issue per PR where you can.

New here? Issues tagged for early work and the [Progress Board](README.md#progress-board) are the
best starting points.

## Clean-room rule

- Write **original Rust**. Do not copy, paste, fork, or transpile code from Rec Room, from
  **RecFlare**, or from any other revival project.
- You may decompile the owned 2026 build **locally** to understand how a system works, and you may
  consult RecFlare's open-source server **only** to learn the *shape* of an endpoint or response
  (what routes exist, what fields come back). Understand it, then reimplement it in your own words
  and your own code. Never paste decompiled or third-party source into this repo.
- If you're unsure whether something is clean-room, ask in the issue before writing it.

## No copyrighted artifacts

Never commit any of the following — they stay on your own machine only:

- Rec Room code or decompiled source
- IL2CPP metadata (e.g. `global-metadata.dat`)
- Game assets (models, textures, audio, etc.)
- Captured request/response bodies or network captures
- Any binaries from the game (`.dll`, `.exe`, `.dat`, …)

The [`.gitignore`](.gitignore) is set up to exclude these — don't override it. The loader (client
circumvention tooling) is also kept out of this public repo by design.

If you accidentally commit a copyrighted artifact, flag it immediately so it can be scrubbed from
history.
