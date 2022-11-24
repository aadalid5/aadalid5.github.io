---
parent: Guides
title: Data Attributes
layout: home
---

# Data Attributes
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

Some systems, such as UI tests and tag managers, require unique selectors
to do their job. In these cases we use data attributes to provide those
unique selectors.

## Attributes in Use

### Analytics Attributes

The analytics team sometimes requires unique selectors to target elements
or for data to be exposed and associated with a specific elements on the
page. In these cases, we use `data-analytics` to provide unique targets
and `data-analytics-*` to expose data.

Example
```html
<button
    type="button"
    onClick={someMethod}
    data-analytics="some-button"
    data-analytics-subscriber-status={user.subStatus}
>
    Save Article
</button>
```

### QA Testing Attributes

QA needs unique selectors for their automated UI tests. For example, if
they need to click on a button during test execution, they need a
unique selector to target that button. To do this we use the `data-qa`
attribute.

Example
```html
<button
    type="button"
    onclick={someMethod}
    data-qa="save-article-button"
>
    Save Article
</button>
```

To aid QA with their testing efforts, we should add `data-qa` attributes
to any elements that can be interacted with by a user. If we fail to do
so, QA will request them as needed. We should only add attributes to
interactive elements. If a request is made to add an attribute to
something like a paragraph element, we should question the reason.