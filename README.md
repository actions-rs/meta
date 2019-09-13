# GitHub Actions for Rust language

Repositories in [this organization](https://github.com/actions-rs) are [GitHub Actions](https://github.com/features/actions), which can be used to do the full CI circle for Rust projects.

All Actions here are using the same defaults and support almost all options, which `cargo` subcommands has.

## Basic workflow

This workflow example creates three jobs:
 1. Run `cargo build` on stable
 2. Run `cargo test` on nightly
 3. Install specific Rust version and run check it too

```yaml
on: [push, pull_request]

name: commit checks

jobs:
  build:
    name: Stable build
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@master
      - uses: actions-rs/toolchain@master
        with:
          toolchain: stable
          override: true
      - uses: actions-rs/cargo@master
        with:
          command: build
          args: --release

  test:
    name: Nightly test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@master
      - uses: actions-rs/toolchain@master
        with:
          toolchain: nightly
          override: true
      - uses: actions-rs/cargo@master
        with:
          command: test
          args: --all-targets

  min_version:
    name: Minimal supported Rust version
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@master
      - uses: actions-rs/toolchain@master
        with:
          toolchain: 1.31.0
          override: true
      - uses: actions-rs/cargo@master
        with:
          command: check
          args: --all-targets
```
