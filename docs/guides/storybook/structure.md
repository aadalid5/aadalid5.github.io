---
grand_parent: Guides
parent: Storybook
title: Style & Structure
layout: home
---

# Storybook guidelines
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

This page documents the standards used in this project for creating and
documenting Storybook stories. The intended audience for this project's
Storybook documentation are library consumers.

## Structure

The proposed structure is similar to the one described
[here](https://storybook.js.org/blog/structuring-your-storybook/). All files
related to documenting a component in particular must be inside a `stories`
directory and include [overview](#overview-story), [playground](#playground-story),
and [feature stories](#features-stories).

The resulting directory layout should resemble the following template:

    Component
    ├── ...
    ├── stories
    │   ├── overview
    │   └── playground
    │   ├── features
    |       ├── foo
    |       ├── bar

### Overview Story

Any and all information that may be useful to a consumer should be included here.
Although this exact information can change depending on the component, the
following minimum information must be provided for all components:

- A small introduction to the component and what it does.
- A table detailing the component's props.
- If applicable, a table detailing the component's variants.
- A usage example.

### Playground Story

This is a story where all the props are connected to the story's controls. The
purpose of this story is to provide an interface through which we can test the
component's behavior for prop variations that are not covered by feature stories.

### Features Stories

Feature stories are a set of stories that cover different visual states of
a component. There are different types of features stories that should be created
as well as criteria for when these types should be created.

#### Default Feature Story

A default feature story contains all the required props for a component and none
of the optional props or no props if the component doesn't have any. This is the
components default state. The story should be named `Default` and will be sorted
to the top of the `Features` directory in the Storybook navigation. Default
feature stories should be created for every component except when a component has
a `variant` prop. Variants are handled differently. This will be covered below.

#### Variant Feature Stories

Variants are required props that impact how a component is styled or rendered. For
example, which icon to render or to style a button as text. Whenever a component
has variants, a feature story should be created for each variant. These stories
should be named `variant - {variant name}` For example, `variant - primary`.

#### Optional Prop Feature Stories

A feature story should always be created for each optional prop that causes a
visual change in the component. For example, if an optional `disabled` prop
causes a component to appear greyed out, it should have a feature story. These
feature stories should be named after the prop. In the case of our previous
example, the story would be named `disabled`.

The only exception is for props that pass in class names to alter the component's
styles. Do not create feature stories for these props.

## Stories

The guidelines for the creation of stories are as follows:

-   **Do not create stories that only extend/overwrite styles.** Some
    components provide a `className` prop that allow a consumer to overwrite
    the styling. For visual testing purposes this should not be done as it is
    pointless to test for arbitrary styling instead of predefined prop behavior.

-   Components with open/active props should have those props set to true in
    their feature story.

-   **Don't create containers that restrict components from expanding their width or height.**
    It is preferable if we do not provide a container for the component and let
    it resize on its own so as to not test for arbitrary responsive values.


## Dos and Don'ts

### Do provide only the necessary controls for the story.

Feature stories should not provide controls to props that are out of scope for
the feature story.

Let's say we are working on a feature story for a Checkbox component that has
the following props:

```js
const { isChecked, showLabel, label } = props;
```

Ideally, we want to create a feature story to test the `isChecked` prop and
another to test the `showLabel` prop. The appropriate way to go about providing
controls for both of these stories is as follows:

**isChecked Story**

```js
export const Checked = Template.bind({});
Checked.args = {
    isChecked: true,
};
```

**showLabel Story**

```js
export const WithLabel = Template.bind({});
WithLabel.args = {
    showLabel: true,
    label: 'Label Here',
};
```

Because each story focuses on showcasing one aspect of the component, it
wouldn't make sense to provide a `showLabel` prop in the `isChecked` story.

While a label might render due to default props (this depends on how the
component is written), the concern lies in the Storybook _controls_ and what a
user can change in the rendered story. Keeping the provided controls relevant to
the feature that is being tested makes for easier exploration of the components
in the library.

---

###  Don't spread props when rendering components.

Template story functions will always receive an `args` parameter, which is
an object with the props for that story. The object should be destructed
and its keys passed individually to the component.

```js
//DON'T do this
function Template(args) {
    return <SomeComponent {...args} />;
}

// DO this
function Template(args) {
    const { foo, bar } = args;
    return <SomeComponent foo={foo} bar={bar} />;
}
```

---

### Provide [actions](https://storybook.js.org/docs/react/essentials/actions) as function handlers by default.

In many cases, components can take in a handler to reflect interactions with the
component. Let's say we have a Button component with an `onClick` prop.

```js
function Template(args) {
    const { onClick } = props;
    return <Button onClick={onClick} />;
}
```

In this case, this `onClick` prop would not cause a visual change for the Button
component and so it is unnecessary to provide a control for this story. However,
we may still want to have some feedback for the handler's functionality and so
we provide a dummy handler in the form of a Storybook _action_.

```js
Button.args = {
    onClick: action('Clicked Button!'),
};
```

In some cases this generic handler is not sufficient and so we must provide real
logic. For instance, a modal may require that we give it some logic when it
dismounts.

```js
function Template(args) {
    const { onClose } = props;
    return <Modal onClose={onClose} />;
}
```

---

### Notes

-   Should you find it absolutely necessary to provide a `className` prop
    to the component, consider modifying the component. A component variation
    that cannot be tested unless the styling is overwritten may indicate that
    extra props are needed.
