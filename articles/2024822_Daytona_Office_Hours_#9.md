---
title: "Daytona Office Hours #9 - Pre-Builds Demo & Latest Fixes!"
description: "The recent updates and highlights shared during the Daytona Office Hours #9 and a special demo for Pre-Builds."
date: 2024-8-22
author: "Daytona"
tags: ["Office Hours", "Prebuilds"]
---
Daytona-Office-Hours-%239
# Daytona Office Hours #9 - Pre-Builds Demo & Latest Fixes!

## Introduction

In our recent office hours, we discussed the latest development news on Daytona. Even though we haven't had a new release yet, there are some interesting features and fixes we are working on, and looking forward to merging them.

### TL;DR

- **Pre-Builds demo**
- **Recent fixes and future releases**
- **Contributions and bounties**

## Pre-Builds

A couple of weeks back we introduced a major feature called [Project Configs](https://github.com/daytonaio/daytona/pull/789). They allow users to define project configurations in advance and use them when creating workspaces in the future. They contain the relevant repository and build information, environment variables which are then used by default whenever a project with the specified repository is created. They are part of a bigger effort to incorporate [pre-builds](https://github.com/daytonaio/daytona/pull/912) which will let users set up "ready-to-go" builds and spend less time waiting for their development environments to be ready. The documentation for the project config can be found [here](https://www.daytona.io/docs/reference/cli/#daytona-project-config).

Prebuilds are a way to speed up development by setting a project configuration to listen to changes in the underlying repository and run a build whenever necessary to ensure that once the user wants to create a project and start working, the creation process is much quicker. The user can then decide on a commit interval after which a build should be triggered and any specific trigger files whose changes should immediately start the build process. Prebuilds is still under development, but it is almost ready to be merged. In the office hours video, we presented a demo of creating and managing pre-builds.

## Recent Fixes

We discussed some of the recent bug fixes:
- **[Fix .devcontainer.json Detection](https://github.com/daytonaio/daytona/pull/943)**: *Checks if .devcontainer.json is located at the root for auto-detection. It used to check the file at .devcontainer/devcontainer.json only.*
- **[Handle Binary Download Interruptions](https://github.com/daytonaio/daytona/pull/942)**: *Prefers to use wget instead of curl to download the binary because it automatically handles interruptions. Additionally, add a retry policy if the download fails.*
- **[Fix Version Mismatch Warning](https://github.com/daytonaio/daytona/pull/941)**: *Fixes the version mismatch warning message.*

Furthermore, there are various minor fixes and optimizations that are going to be in the next release. There are some other open pull requests that we are not sure if they are going to be merged right away.

## Contribute and Win Bounties

We finalized this episode by motivating users to submit issues if they encountered any and to contribute to Daytona open-source to win bounties. If you have any questions, ask us at our [community slack](https://go.daytona.io/slack).

Watch our office hours video on YouTube: [Daytona Office Hours #9 - Pre-Builds Demo & Latest Fixes
](https://www.youtube.com/watch?v=7WZdv0ccGOU).
