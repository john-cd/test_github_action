<!-- TODO Reviewed ??-??-2026. -->

# test_github_action

This repository exercises the Rust container action on a GitHub-hosted Linux runner. The workflow pins both the checkout action and the upstream container action to reviewed commit SHAs, then validates the returned ZIP, loads its Docker image, and runs the test binary.

The sample Rust toolchain is pinned in `rust-toolchain.toml`. Update the upstream action SHA only after reviewing its change and confirming the hosted workflow still builds and runs the exported image.

## Local Rust checks

Install the toolchain from `rust-toolchain.toml` with `rustup show` in the checkout. From the repository root, run `cargo check --locked --workspace --all-targets` and `cargo test --locked --workspace`. The GitHub workflow separately checks the pinned Docker action.
