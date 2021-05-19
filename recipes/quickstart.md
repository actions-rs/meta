# Quickstart CI workflow

This workflow installs latest stable Rust version
and invokes these commands in parallel:

 * `cargo check`
 * `cargo test`
 * [`cargo fmt`](https://github.com/rust-lang/rustfmt)
 * [`cargo clippy`](https://github.com/rust-lang/rust-clippy)

## When it can be used?

1. You have a simple Rust project
2. There is no OS-specific code
3. It can be compiled with the `stable` Rust compiler
4. You want a quick start with Rust CI

```yaml
on: [push, pull_request]

name: Continuous integration

jobs:
  check:
    name: Check
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions-rs/toolchain@v1
        with:
          profile: minimal
          toolchain: stable
          override: true
      - uses: actions-rs/cargo@v1
        with:
          command: check

  test:
    name: Test Suite
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions-rs/toolchain@v1
        with:
          profile: minimal
          toolchain: stable
          override: true
      - uses: actions-rs/cargo@v1
        with:
          command: test

  fmt:
    name: Rustfmt
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions-rs/toolchain@v1
        with:
          profile: minimal
          toolchain: stable
          components: rustfmt
          override: true
      - uses: actions-rs/cargo@v1
        with:
          command: fmt
          args: --all -- --check

  clippy:
    name: Clippy
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions-rs/toolchain@v1
        with:
          profile: minimal
          toolchain: stable
          components: clippy
          override: true
      - uses: actions-rs/cargo@v1
        with:
          command: clippy
          args: -- -D warnings
```

## Can I tune it?

Sure!

This workflow is using following Actions to execute the pipeline,
see their pages for the available options:

1. [`actions-rs/toolchain`](https://github.com/actions-rs/toolchain)
2. [`actions-rs/cargo`](https://github.com/actions-rs/cargo)
