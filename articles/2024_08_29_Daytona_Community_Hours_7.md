---
title: "Daytona Office Hours #7 - Major Updates & Exciting New Features!"
description: "This article covers the recent updates and news shared during the Daytona Community Hours YouTube video. Provides a detailed summary of the main points discussed in the video, focusing on any new releases, patches, or updates. Daytona's latest developments and improvements and how they can benefit users."
date: 2024-08-29
author: "Toma Puljak"
tags: ["DOH", "News", "Update"]
---

# Daytona Office Hours #7 - Major Updates & Exciting New Features!

## Introduction

Hello everyone, and welcome to the seventh edition of Daytona Office Hours! Today, we are excited to share the latest updates and features from our newly released version 0.24.0. As well as some important news about Daytona. This release was significant as we had a lot of fixes, chores, and most importantly features. Let's dive right in.

## Features

1. New API Route Implementation: We have implemented a get URL from the repository API route. This API route is meant to support clients that integrate with Daytona. This feature makes it easier to create a workspace if you don't have access to a concrete repo URL. This allows you to create a repo URL from a commit hash, a branch, and a PR.
2. Work Space Status Checks: This is an useful user experience improvement feature. This checks the state of the project before executing code and SSH into it. It makes it easier and more clear to the user if the workspace or project is stopped while attempting to connect to it.
3. AWS CodeCommit Support: Implemented AWS CodeCommit as a git provider, as it was requested by one of the community members. If not all but this gives us most of the git providers covered in Daytona. Makes it more complete and accessible to those using AWS CodeCommit.
4. Project Configs: This is the biggest feature of this release. This feature is a huge UX improvement. It allows the spinning up multiple projects and workspaces with the existing configuration. To know more about the Project Configs please refer to [this](https://github.com/daytonaio/daytona/releases/tag/v0.24.0) page.

## Breaking Changes

Because of the provider interface change. This release requires users to update their providers with `daytona provider update`.

## Fixes

1. Control-C Error Handling: Now Daytona handles the error that was being thrown on `ctrl+c`. We have fixed the error that should be reserved for when things actually go wrong. Now, if you `control+c` out of `Daytona help` it won't throw a fatal error. It will catch the signal and exit.
2. VS Code CLI Installation Info: Prompts the users to install VS Code CLI, if it's not installed locally. This comes in handy if the user-chosen ide 'vscode' for the project is not installed.
3. Loginctl Note for Linux Server Daemon: When the user runs Daytona as a daemon on a remote machine and logs out of it. The Daytona server stops and prompts the user to enable `loginctl` and allows the Linux server daemon to persist through log out.
4. Error-Handling on wrong token: Handles the 500 internal server error, if the user enters the wrong API token.
5. Root User Check: Added a root user check when starting the server. We recommend running the server as a non-root user. Since Daytona remaps ownership of repository files when you create a project. It's important note that the server is not run by the root user as Daytona cannot remap ownership in this case.
6. Devcontainer Local Environment Override: Now the host environment variables can override the `localEnv`. This fixes a bug when running Daytona in a non-Linux non-daytona-user environment.
7. ProviderConfig Authentication: Authenticates the `providerConfig` before adding them to the database.
8. Git Provider For URL interface: Minor fix to `GitProviderForUrl` interface return value for AWS CodeCommit conflict.

## Chores And Tests

1. Server yes flag description: Fixes "yes" flag description that was leftover from the `daytona purge` command.
2. Swagger Version Update: The Swagger version is now updated to 0.24.0. This will be automated in the future.
3. Docker Bump: We bumped [github.com/docker/docker](https://github.com/docker/docker) from 26.0.2+incompatible to 26.1.4+incompatible.
4. Docker Package Readme: Added a README to the `docker` pkg. It explains its purpose and testing procedure. Outlines how to test the package.
5. Duplicate Repo Validation Removal: Removed duplicate repo validation and appended occurrence number to keep duplicate entries unique.

## New Contributors
Daytona loves to see new contributors around. This week we have two new contributors. We welcome all the new contributors.
1. [@titanventura](https://github.com/titanventura) made their first contribution in [#822](https://github.com/daytonaio/daytona/pull/822)
2. [@the-johnwick](https://github.com/the-johnwick) made their first contribution in [#797](https://github.com/daytonaio/daytona/pull/797)

## Updates

In the next release, we are developing a few updates around users submitting a form early, reverting swagger version update, and changing to a different config directory in development mode. As we come up with a new release this Friday, Don't forget to [watch](https://youtu.be/nVQWa4jmwLc?si=t51TVWIdfLaxy7uD&t=635) the demonstration of changing to different config directory in development mode, Stay tuned!

## References/Resources

- [Daytona Community Hours YouTube Video](https://www.youtube.com/watch?v=nVQWa4jmwLc)
- [Daytona Releases Page](https://github.com/daytonaio/daytona/releases/)