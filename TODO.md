# TODO

## Repository review (2026-11-12)

- [ ] **P2 — Exercise a released Rust container action and assert its artifact (small).**
  `.github/workflows/main.yaml` uses `actions/checkout@v4` and `john-cd/rust_github_action@master`. Coordinate with the upstream action upgrade. Pin reviewed action revisions compatible with the hosted runner, set explicit Rust toolchain expectations, and fail unless the action returns a readable zip containing an image that loads and starts.
