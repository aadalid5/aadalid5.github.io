---
parent: Guides
title: Git Workflow
layout: home
---

# Git Workflow
{: .no_toc }

<details markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

## Git Hooks

### Pre-commit

During the pre-commit hook, the linters will be executed. Specifically, the
[lint](/pages/HBRG/crimson-dark/guides/npm.html#lint) script will be executed.
This script does not use the fix option. This is intentional so that no
unexpected changes are introduced during the commit process. If linting fails,
your commit will also fail. For this reason, it is encouraged that you execute
the linters prior to committing. If your commit does fail due to linting errors,
simply resolve the errors and try committing again.

### Pre-push

During the pre-push hook, the unit tests will be executed using the
[test](/pages/HBRG/crimson-dark/guides/npm.html#test) script. If any tests fail
or the coverage threshold is not met, the tests will fail and your push will also
fail. If your push does fail for this reason, you'll need to check the results,
address the reason for failure, and push your changes again.

## Creating a Branch

When you're ready to start work on a new feature or bug, you'll want to create a
new branch off of `main`. Name your branch by the ticket number and,
optionally, a description of the Jira ticket you're working on. An
example of a good branch name for
[this Jira ticket](https://jira.hbsp.harvard.edu/browse/HBRMODRN-218) would be
`HBRMODRN-218-app-documentation`, or simply `HBRMODRN-218`. Including the Jira
ticket number is important because our Jira integration will list associated
branches, commits, and pull requests in the ticket.

## Commit Messages

This project doesn't enforce a format for commit messages. However, commit
messages will be used in the release notes, so there is an expectation that we
write good commit messages. A good commit message is one that is descriptive
enough that someone would generally understand the purpose and scope of the
commit when reading the message.

### Examples

```text
# Bad
update nav

# Good
HBROPS-215: update navigation to include "Diversity" link
```

```text
# Bad
fix safari bug

# Good
HBROPS-581: fix article heading margin in safari
```

## Squash

Squashing entails combining several commits into one with a new commit message.
This is essentially rewriting the history of your branch. Squashing is preferred
when you have multiple commits which as a whole makeup a unit of code, but
separately would result in errors or an incomplete feature. If you've never
worked with `squash` before, you should read
[the documentation](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)
prior to attempting it.

## Rebase vs Merge

This project prefers rebasing over merging. While merging is often easier, it
leaves much to be desired in the commit history. Rebasing, on the other hand, will
preserve the commit history and make it easier to read when a need arises.

### Important Notes

- If you're rebasing a branch that has already been pushed to the remote
repository, you'll need to force push after rebasing.
- Once complete, rebasing is permanent. If you're not completely comfortable, you
may want to create a copy of your branch prior to attempting a rebase.
- If you need help rebasing, just ask someone.
