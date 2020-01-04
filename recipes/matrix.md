# Matrix CI workflow

This workflow installs multiple different Rust versions in parallel
and invokes these commands for each installed version:

 * `cargo build`
 * `cargo test`
 * [`cargo fmt`](https://github.com/rust-lang/rustfmt)
 * [`cargo clippy`](https://github.com/rust-lang/rust-clippy)

## When it can be used?

1. You want to guarantee that your crate is compiled on `stable`
2. You also want to provide the MSRV (Minimal Supported Rust Version) policy
3. You also want to check if your crate compiles on `beta` and `nightly`

## Workflow

```yaml
on: push

name: Continuous integration

jobs:
  ci:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        rust:
          - stable
          - beta
          - nightly
          - 1.31.0  # MSRV

    steps:
      - uses: actions/checkout@v2

      - uses: actions-rs/toolchain@v1
        with:
          profile: minimal
          toolchain: ${{ matrix.rust }}
          override: true
          components: rustfmt, clippy

      - uses: actions-rs/cargo@v1
        with:
          command: build

      - uses: actions-rs/cargo@v1
        with:
          command: test

      - uses: actions-rs/cargo@v1
        with:
          command: fmt
          args: --all -- --check

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

