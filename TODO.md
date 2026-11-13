# TODO

## Repository review (2026-11-12)

No open GitHub issues were found, so repository work is tracked here.

- [x] **P2 — Exercise a pinned Rust container action and assert its artifact (2026-11-12).**
  Pinned `actions/checkout` to the verified v7.0.1 commit and the upstream action to its current `develop` commit `90676192279197c6d8d5802d2531af644e117a25`. Added an explicit Rust 1.100.0 toolchain. The workflow now fails unless the action returns an existing, readable ZIP containing a Docker image, the image loads, and the test binary starts with the expected output.

- [ ] **P2 — Capture hosted workflow evidence after the change is pushed.**
  The repository's workflow uses GitHub-hosted Linux Docker, which is unavailable for local execution here. A successful hosted run is still needed to verify the pinned upstream action's archive and container behavior end to end.
