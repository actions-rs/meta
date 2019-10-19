# GitHub Actions for Rust language

![CC0 licensed](https://img.shields.io/github/license/actions-rs/meta)
[![Gitter](https://badges.gitter.im/actions-rs/community.svg)](https://gitter.im/actions-rs/community)

Repositories in [this organization](https://github.com/actions-rs) are [GitHub Actions](https://github.com/features/actions), which can be used to do the full CI circle for Rust projects.

## Recipes

See the [@actions-rs/example](https://github.com/actions-rs/example) repository
with the live workflows described here.

### Quickstart ⚡

[Quickstart](./recipes/quickstart.md) recipe can be useful
if you are not familiar with GitHub Actions, never used CI thingies before
or just want to copy-n-paste some scripts into your project for an instant result.

### MSRV (Minimal Supported Rust Version) 🔒

[MSRV](./recipes/msrv.md) recipe does almost the same what "[Quickstart](#quickstart)" do,
but also helps to guarantee the MSRV policy if you have any.

### Nightly clippy and rustfmt 📎

Ever had this problem when your CI build is broken,
because today's `nightly` is missing `clippy` or `rustfmt`?\
Yeah, I know, everyone hates that.

[Nightly lints](./recipes/nightly-lints.md) recipe is utilizing `rustup` ability
to find the most recent `nightly` toolchain with the components requested;
no more broken builds for you!

### Stable + beta + nightly + MSRV

[Matrix](./recipes/matrix.md) recipe combines three previous recipes together
in order to make an ultimate quickstart workflow.

### Perform security audit for your dependencies 🛡️

[Security Audit](./recipes/security-audit.md) recipe is using [RustSec](https://rustsec.org/)
advisories database to audit crate for security vulnerabilities.

## License

All recipes in this repository are published with the [CC0](./LICENSE) license.
