---
grand_parent: Guides
parent: Testing
title: Visual Regression Testing
layout: home
---

# Visual Regression Testing
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

This project uses the [Storyshots](https://github.com/storybookjs/storybook) 
addon for Storybook for visual regression testing.

## Testing

### What is Visual Regression Testing?

Visual regression testing is a type of regression testing where we
validate that recent changes to the code have not caused the visual
aspect of our components to change. This type of testing is not intended
to validate the internal functionality of the components but rather
that the component stays _visually_ the same.

In many cases we want to apply visually test components
that first must be interacted with. For instance, modals and alerts
might require that you first click on a button. In these cases what we
are interested in is how a component looks after some interaction
with it has taken place. With Storyshots (the Storybook addon that enables
us to visually test components) we can provide a `beforeScreenshot` handler
to take a snapshot of a component only when it is in the desired state.

In more general terms, this handler serves as a way to delay the screenshot,
so we may find it necessary to use it to avoid taking snapshots of things
like mounting animations.
More information can be found [here](https://storybook.js.org/addons/@storybook/addon-storyshots-puppeteer).

### How is this achieved?

Storyshots allows us to generate images of components when they
are rendered by the Storybook stories, and these images are then saved and
used as a baseline for future comparisons for that component. These images
can be found in the `snapshots` folder inside each component directory, and
Storyshots will look for this directory when trying to compare newly generated 
images with the baseline. If this folder is not found when the tests run, 
Storyshots will use the generated images as the new baseline and create the 
folder for us.

### Considerations

Care should be taken to ensure consistency when making component comparison,
for instance:

-   **Do not use global CSS**. Avoid using global styles as this will affect 
    components that you may not be working on, which will cause them to fail 
    visual testing unless new snapshots are generated for all of the affected 
    components.

-   **Be careful when testing components that depend on some external API**. APIs 
    whose response is not reliable should not be used for stories as this can 
    cause different results to load when a component's baseline is generated
    and when new images are created and compared.
