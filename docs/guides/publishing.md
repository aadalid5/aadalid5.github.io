---
parent: Guides
title: Publish / Release
layout: home
---

# Publishing the Package
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

This guide aims to cover the CI/CD workflows that are responsible for publishing
the `mfe-core` package. Aside from publishing a "production ready" version of the
package, we also publish versions for change requests and changes that will be
in the next release. The rest of this guide will go over the details on how and
when packages are published as well as how a release can be performed.

## Publishing Events

There are 3 events that will trigger publishing. Those events are:

* [Updating a pull request targeting `main`](#updating-a-pull-request-targeting-main)
* [Merging a pull request into `main`](#merging-a-pull-request-into-main)
* [Manually triggering a release](#manually-triggering-a-release)

### Updating a Pull Request Targeting `main`

#### Trigger

Whenever a pull request targeting `main` is created or updated, the Jenkins
pipeline will publish a new version of the package. The only exception is for pull
requests with a base branch matching the pattern `release-*`.

#### Build Contents

This build is based on the resulting source code after the target and base branches
are merged.

#### Version Number

The version number will be a combination of the current semantic version of the
package and the short commit hash. For example, `1.2.3-pr.asf7d86`.

#### NPM Tag

This version of the package will be tagged for easy installation. The tag will
be the pull request number prefixed by `pr-`. For example, `pr-234`.

To install the package using the tag:
```bash
npm i mfe-core@pr-234
```

### Merging a Pull Request into `main`

#### Trigger

Whenever there is a push event to the `main` branch, a new version of the package
will be published. This should only happen when a pull request is merged into
`main`. On rare occasions an administrator may need to push to `main` directly. This
will also trigger publishing.

#### Build Contents

This build is based on the `main` branch after the pull request is merged.

#### Version Number

The version number will be a combination of the current semantic version of the
package and the short commit hash. For example, `1.2.3-next.asf7d86`.

#### NPM Tag

This version of the package will be tagged `next` for easy installation.

To install the package using the tag:
```bash
npm i mfe-core@next
```

### Manually Triggering a Release

This version is intended to be a "production ready" version. It can be manually
triggered whenever the `main` branch is ready using the `mfe-core-release` job in
Jenkins. The job will prompt the initiator for the release type (patch, minor,
major), build the package, deploy it, create and merge a pull request for the
version bump, and generate release notes in GitHub.

#### Trigger

Someone needs to manually click the "Build Now" button in the `mfe-core-release`
Jenkins job.

#### Build Contents

This build is based on the `main` branch.

#### Version Number

The version number will be the semantic version generated from the release type
the initiator chooses. If the current version is `1.2.3` and during release the
initiator chooses:

* `patch` then the new version will be `1.2.4`
* `minor` then the new version will be `1.3.0`
* `major` then the new version will be `2.0.0`

#### NPM Tag

This version uses the `latest` tag. This is the tag NPM assumes when installing
a package without one specified.

To install a package using the tag:
```bash
npm i mfe-core
```
