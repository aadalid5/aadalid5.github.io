---
parent: Guides
title: Code Style
layout: home
---

# Code Style

## Linters

This project uses [ESLint](https://eslint.org/) and
[Stylelint](https://stylelint.io/) to encourage consistent code style in
the code base. Several plugins and configs have been pulled in with
little or no additional configuration on our end.

Do not disable the linter through the use of code comments. In almost all cases,
you should rewrite your code to comply with the linter. If you absolutely need to
disable the linter for a **valid reason**, it should be done only for that line of
code and for the specific rule(s). Code reviewers must agree that disabling the
linter is necessary. An example of a **valid** reason for disabling a linting rule
might be that a JSX library **requires** you to spread props when interacting with it.
An example of an **invalid** reason for disabling a linting rule might be that you
**prefer** to spread props instead of explicitly writing each one.
