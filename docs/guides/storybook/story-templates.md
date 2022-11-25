---
grand_parent: Guides
parent: Storybook
title: Templates
layout: home
---

# Story Templates
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

Here you can find templates for the _Overview_, _Playground_ and _Feature_ stories, 
so that they can be reused when required.

### Overview Story

This template aligns with the [Overview Structure](/pages/HBRG/mfe-core/guides/storybook/structure.html#overview-story) guidelines.
You can see the mdx template <a href="/docs/guides/storybook/templates/overview.stories.mdx" target="_blank" rel="noopener noreferrer">here</a>.

````md
import { Meta } from '@storybook/addon-docs';
import MyComponent from '../Component';
import PropsTable from '../../../story-helpers/PropsTableHelper.mdx';
import Table from '../../../story-helpers/TableHelper.mdx';

<Meta title="Components/MyComponent/Overview" component={MyComponent} />

# MyComponent

Short description for component MyComponent.

## Props

export const propsList = [
    { name: 'children', type: 'node', description: 'Prop description' },
    {
        name: 'variant',
        type: 'string',
        description: 'Prop description',
        defaultValue: MyComponent.variant.PRIMARY,
    },
];

<PropsTable propsList={propsList} />

## Variants

If applies, short description for the variants of MyComponent.

<Table
    headings={['Property', 'Description']}
    body={[
        ['<code>MyComponent.variants.ALT</code>', 'Variant Description'],
        ['<code>MyComponent.variants.PRIMARY</code>', 'Variant Description.'],
    ]}
/>

## Use example

```jsx
import MyComponent from 'mfe-core/ui/MyComponent';

return (
    <MyComponent variant={MyComponent.variant.ALT}>
        <div>Some text</div>
    </MyComponent>
);
```
````

### Playground Story

This template aligns with the [Playground](/pages/HBRG/mfe-core/guides/storybook/structure.html#playground-story) guidelines.
You can see the mdx template <a href="/docs/guides/storybook/templates/playground.stories.mdx" target="_blank" rel="noopener noreferrer">here</a>.

```md
import { Meta, Canvas, Story } from '@storybook/addon-docs';
import MyComponent from '../Component';

<Meta
    title="Components/MyComponent/Playground"
    component={MyComponent}
    argTypes={% raw %} {{}} {% endraw %}
/>

# Playground

export function Template(args) {
    const { children, variant } = args;
    return (
        <div>
            <MyComponent variant={variant}>{children}</MyComponent>
        </div>
    );
}

<Canvas>
    <Story
        name="Playground"
        args={% raw %} {{ {% endraw %}
            children: 'Some text',
            variant: MyComponent.variant.PRIMARY,
        {% raw %} }} {% endraw %}
    >
        {Template.bind({})}
    </Story>
</Canvas>

```

### Feature Story

This template aligns with the [Feature Stories](/pages/HBRG/mfe-core/guides/storybook/structure.html#features-stories) guidelines.
You can see the mdx template <a href="/docs/guides/storybook/templates/features/someFeature.stories.mdx" target="_blank" rel="noopener noreferrer">here</a>.

```md
<Meta
    title="Components/MyComponent/Features"
    component={MyComponent}
    argTypes={% raw %} {{ {% endraw %}
        children: {
            table: { disable: true },
        },
        variant: {
            table: { disable: true },
        },
    {% raw %} }} {% endraw %}
/>

# Default Story

<Story
    name="Feature Variant"
    args={% raw %} {{ {% endraw %}
        children: 'Some text',
        variant: MyComponent.variant.ALT,
    {% raw %} }} {% endraw %}
>
    {Template.bind({})}
</Story>
```

**Note**

When using the the templates, please remove the eslint comment in the first line.
That was added only for demo purposes.