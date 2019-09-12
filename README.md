# GitHub Actions for Rust language

Repositories in [this organization](https://github.com/actions-rs) are [GitHub Actions](https://github.com/features/actions), which can be used to do the full CI circle for Rust projects.

All Actions here are using the same defaults and support almost all options, which `cargo` subcommands has.

## Basic workflow

This workflow example creates three jobs:
 1. Run `cargo fmt` & `cargo clippy`
 2. Run `cargo build` & `cargo test`
 3. Install specific Rust version and run tests against it

```yaml
on: [push, pull_request]

name: commit checks

jobs:

  lints:
    name: Lints
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@master
      - uses: actions-rs/fmt@master
      - uses: actions-rs/clippy@master

  checks:
    name: Checks
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@master
      - uses: actions-rs/toolchain@master
        with:
          toolchain: stable
          override: true
      - uses: actions-rs/build@master
      - uses: actions-rs/test@master

  min_version:
    name: Minimal supported Rust version
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@master
      - uses: actions-rs/toolchain@master
        with:
          toolchain: 1.31.0
          override: true
      - uses: actions-rs/test@master
```
