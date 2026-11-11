# Changelog

All notable changes to LocalBrain are documented here. Format follows
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/); versions match
`server/package.json` and Git tags (`vX.Y.Z`).

## [Unreleased]

## [0.1.0] - 2026-11-11

### Added

- Packaged `localbrain` binaries for macOS, Linux and Windows that embed
  the server, frontend and runtime — no Node.js install required.
  Unix assets use a `.bin` extension and Windows uses `.exe`.
- Packaged binaries open the web UI automatically; use `--daemon` for
  API-only or `--no-browser` to keep the server headless.
- Build-time environment lock: binaries are built for `dev` or `prod`
  (`make bin ENV=prod`) and reject `--env` switches that would mix data
  directories.
- `--help` and broader CLI configuration flags (`--env`, `--data-dir`,
  `--models-dir`, `--api-token`, `--remote-url`, worker TLS options, …).
- Resilient watched-folder handling: unavailable folders are marked
  unavailable, syncing pauses safely, indexed documents stay searchable,
  and queued per-file jobs are pruned instead of flooding the queue.
- Automatic additive schema repair for existing `app.db` files.

### Fixed

- `no such column: meta` errors on databases created before newer
  document columns existed.
- Folder syncs could treat an unmounted volume as empty and remove
  indexed locations; scans now defer until the folder is readable again.
