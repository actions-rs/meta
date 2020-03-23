# Contributing to `actions-rs`

The following is a set of guidelines for contributing to `actions-rs` GitHub Actions.

## Requesting new Actions

Use this [issues list](https://github.com/actions-rs/meta/issues) to talk about things you want to see in `actions-rs`.

## Reporting bugs

Before creating bug reports, please check the GitHub issues list for Action you are using
as you might find out that you don't need to create one.
When you are creating a bug report, please include as many details as possible.

    Note: If you find a closed issue that seems like it is the same thing that you're experiencing,
    open a new issue and include a link to the original issue in the body of your new one.

### How do I submit a bug report?

Bugs are tracked as a GitHub issues in the corresponding Action repositories.

Explain the problem and include additional details to help maintainers reproduce the problem:

 1. Use a clear and descriptive title for the issue to identify the problem.
 2. Describe the exact steps which reproduce the problem in as many details as possible.
 3. Provide specific examples to demonstrate the steps.
    Include links to the workflow files (pointing to the specific commit, and not to the `master` branch) and
    attach step logs to the issue (consider enabling [debug logs](https://github.com/actions/toolkit/blob/master/docs/action-debugging.md) first)
 4. Describe the behavior you observed after following the steps and point out what exactly is the problem with that behavior.
 5. Explain which behavior you expected to see instead and why.

## Pull Requests

If your change introduces any new functionality or breaks the backwards compatibility in any matter -
do not rush to create a Pull Request at all.\
Maintaining backwards compatibility is highly important, therefore your change might be declined.
Do not waste your time on that and create an issue first,
explain why do you want to make this change and let the discussion happen.

Code you are contributing should pass the following checks:

1. Should change only one specific thing
2. Not raising any compiler errors or warnings
3. Conforms to formatting rules (use `npm run format` command)
4. Not raisiing any lint warnings (use `npm run lint` command)
5. Should pass the CI tests

Now create a GitHub Pull Request with patch:

1. Ensure the Pull Request description clearly describes the problem and solution
2. Include the relevant issue number if applicable
3. Ensure that all the checks from above are passing
