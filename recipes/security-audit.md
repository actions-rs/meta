# Security audit workflow

This workflow is executed on schedule and performs an audit
for crates with security vulnerabilities.

## When it can be used?

When you agree that it is important to have no dependencies with security vulnerabilities.

```yaml
name: Security audit
on:
  schedule:
    - cron: '0 0 * * *'
jobs:
  audit:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v1
      - uses: actions-rs/audit-check@v1
        with:
          token: ${{ secrets.GITHUB_TOKEN }}```
```

This Action will be executed periodically at midnight of each day
and check if there any new advisories appear for crate dependencies.\
For each new advisory (including informal) an issue will be created.

Alternatively, you can use it to audit changes (commits or pull requests),
see an example [here](https://github.com/actions-rs/audit-check#audit-changes).

## Can I tune it?

Sure!

This workflow is using following Actions to execute the pipeline,
see their pages for the available options:

1. [`actions-rs/audit-check`](https://github.com/actions-rs/audit-check)
