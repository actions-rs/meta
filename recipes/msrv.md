# Quickstart + MSRV CI workflow

This workflow is doing almost the same what [Quickstart workflow](../quickstart.md) does,
except all jobs are invoked twice: for latest stable Rust and
for MSRV (Minimal Supported Rust Version) toolchain.

## When it can be used?

1. You have a simple Rust project
2. It can be compiled with the `stable` Rust compiler
3. You also have a policy about minimal supported Rust version (ex. "*this crate can be compiled with Rust 1.31.0 and higher*")
    and you want to guarantee that

## Workflow

```yaml
on: [push, pull_request]

name: Continuous integration

jobs:
  check:
    name: Check
    runs-on: ubuntu-latest
    strategy:
      matrix:
        rust:
          - stable
          - 1.31.0
    steps:
      - uses: actions/checkout@master
      - uses: actions-rs/toolchain@v1
        with:
          toolchain: ${{ matrix.rust }}
          override: true
      - uses: actions-rs/cargo@v1
        with:
          command: check

  test:
    name: Test Suite
    runs-on: ubuntu-latest
    strategy:
      matrix:
        rust:
          - stable
          - 1.31.0
    steps:
      - uses: actions/checkout@master
      - uses: actions-rs/toolchain@v1
        with:
          toolchain: ${{ matrix.rust }}
          override: true
      - uses: actions-rs/cargo@v1
        with:
          command: test

  fmt:
    name: Rustfmt
    runs-on: ubuntu-latest
    strategy:
      matrix:
        rust:
          - stable
          - 1.31.0
    steps:
      - uses: actions/checkout@master
      - uses: actions-rs/toolchain@v1
        with:
          toolchain: ${{ matrix.rust }}
          override: true
      - run: rustup component add rustfmt
      - uses: actions-rs/cargo@v1
        with:
          command: fmt
          args: --all -- --check

  clippy:
    name: Clippy
    runs-on: ubuntu-latest
    strategy:
      matrix:
        rust:
          - stable
          - 1.31.0
    steps:
      - uses: actions/checkout@master
      - uses: actions-rs/toolchain@v1
        with:
          toolchain: ${{ matrix.rust }}
          override: true
      - run: rustup component add clippy
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

