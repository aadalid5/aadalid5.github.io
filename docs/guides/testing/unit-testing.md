---
grand_parent: Guides
parent: Testing
title: Unit Testing
layout: home
---

# Unit Testing
{: .no_toc }

<details markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

## Overview

This project uses [Jest](https://jestjs.io/docs/getting-started) and
[React Testing Library](https://testing-library.com/docs/react-testing-library/intro/)
for unit testing.

## Why do we Write Unit Tests?

We write unit tests to ensure our code behaves as intended and build
confidence in the changes we're releasing.

## Code Coverage

**Thresholds**

| Branch | Function | Line | Statement |
| :---: | :---: | :---: | :---: |
| 90% | 90% | 90% | 90% |

These thresholds are an enforced minimum level of coverage. There's no
reason we can't strive to maintain higher coverage.

## Strategies

These are some common strategies used in our testing.

### Test Queries

React Testing Library has a great
[guide](https://testing-library.com/docs/queries/about#priority) that lists their
queries in the order they should be prioritized for use. Please review this at
least once.

In general, avoid using `getByTestId`. More often than not, it's not necessary to
use. That being said, there are rare occasions where it may be necessary to use
the `getByTestId` query. If you find yourself using this query often, you may want
to ask someone for feedback.
