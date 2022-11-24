---
parent: Guides
title: Node Package Manager (NPM)
layout: home
---

# Node Package Manager (NPM)
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

This project uses [Node Package Manager](https://npmjs.com) to manage its
dependencies. Moving forward Node Package Manager will be referred to as NPM.

## Configuration

This project makes one configuration change to NPM. That change is to save exact
version numbers in `package.json`.

## Installing Dependencies

In general, use `npm ci` to install your dependencies. `npm ci` will install
dependencies using the version numbers from `package-lock.json`. This will
ensure you're using the same dependencies that have been tested and known to work
with the application. It will also prevent you from unintentionally upgrading
transitive dependencies.

If you want to upgrade direct or transitive dependencies, use `npm install` or
`npm i`.

## Scripts

### `build`

This script generates a production build of the application.

### `clean`

This script deletes all temporary artifacts like NPM dependencies, build files,
files generated when running tests, etc.

### `clean:all`

This script runs the `clean` script and also deletes the `node_module` directory.

### `clean:build`

This script deletes all build files.

### `lint`

This script executes all linting.

### `lint:fix`

This script executes all linting and automatically addresses any fixable
errors.

### `lint:js`,

This script executes all JavaScript related linting.

### `lint:js:fix`

This script executes all JavaScript related linting and automatically addresses
any fixable errors.

### `lint:scss`

This script executes linting on all SCSS and CSS files.

### `lint:scss:fix`

This script executes linting on all SCSS and CSS files. It also automatically
addresses any fixable errors.

### `prepare`

This lifecycle script runs automatically with local npm install to have Git hooks enabled.

### `release`

This script runs `build` and then publishes the `dist/` directory to our Nexus
registry.

### `release:local`

This script runs `build` and uses [yalc](https://www.npmjs.com/package/yalc) to
publish the `dist/` directory to a local registry, so it can be consumed by another
local MFE. Useful to test the library in your local environment without the need
to push and publish all changes.

### `release:notes`

Generates release notes in the GitHub repository using
[release-it](https://www.npmjs.com/package/release-it). The release notes will
contain a list of commit messages since the last git tag.


### `sb`

This script starts the Storybook development server on port 6006.

### `sb:a11y`

This script runs an accesibility testing using [axe-playwright](https://www.npmjs.com/package/axe-playwright), 
it needs the Storybook to be running.

### `sb:build`

This script generates a static web application with the stories in the
current project and outputs it to a `.tmp/storybook` directory.

### `sb:test`

This script conducts visual testing of the components using the created
stories for each of them.

### `test`

Runs both `sb:test` and `unit:test`.

### `unit:test`

This script executes unit tests.
