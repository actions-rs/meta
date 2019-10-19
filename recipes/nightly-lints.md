# Nightly lints CI workflow

This workflow installs latest nightly Rust version
and invokes these commands in parallel:

 * [`cargo fmt`](https://github.com/rust-lang/rustfmt)
 * [`cargo clippy`](https://github.com/rust-lang/rust-clippy)

## When it can be used?

1. You are living on an edge
2. You prefer to use `nightly` versions of `clippy` and `rustfmt`,
as they has more options available

## Workflow

```yaml
on: [push, pull_request]

name: Lints

jobs:
  clippy:
    name: Clippy
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v1
      - id: component
        uses: actions-rs/components-nightly@v1
        with:
          target: x86_64-unknown-linux-gnu
          component: clippy
      - uses: actions-rs/toolchain@v1
        with:
          profile: minimal
          toolchain: nightly
          override: true
          components: rustfmt, clippy
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

