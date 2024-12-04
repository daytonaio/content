---
title: 'Daytona Community Hours #7'
description:
  ' A detailed summary of the new releases, patches, and updates that were
  mentioned during the Daytona Community Hours #7 YouTube video.'
date: 2024-08-09
author: 'Team Daytona'
tags: ['News', 'Update', 'Project Configs']
---
# Daytona Office Hours #7

As always, in our recent community hours, we reviewed the latest developments
and improvements at Daytona. We're excited to walk you through our latest
release and give you a sneak peek at what's coming next. Let's dive right in!

## TL;DR

- Project Configs: Let users create multiple projects seamlessly.
- API Route: Get the URL from any instance of a repository.
- Workspace Status Checks: Status checks are added to the code and SSH commands.

## What's New in This Release

### Project Configs feature

This release introduced a major feature, Project Configs feature that allows you
to streamline the project creation process. This new feature will enable users
to save project details like repository information, build settings, and
environment variables. Also, lets users pre-configure your projects and quickly
create new workspaces. Project Configs are a stepping stone towards prebuilds, a
feature that will let you set up ready-to-use development environments even
faster.

#### How It Works

- Create Configs: Use the `daytona project-config` command to define your
  project configurations.
- Reuse Configs: When creating a new workspace, simply specify the desired
  project config.
- Customize: If needed, override preconfigured settings using the `--blank`
  flag.

### Recent Fixes

- Note on loginctl Linux server daemon: Added a note to users on Linux to run
  `loginctl enable-linger $USER` to enable the server daemon to continue running
  after logging out of the machine. This is specifically useful for servers
  running on remote machines.
- Fatal error handling on `ctrl-c`: Now, if you `control-c` out of Daytona, it
  won't throw a fatal error. It will catch the signal and exit.
- Inform users about prerequisites when opening a project with VS Code: When
  setting up VS Code as a default IDE, Daytona now informs the user if VS Code
  is not installed locally.
- A root user check on serve: Added a root user check when starting the server
  and a recommendation on running as a non-root user.

## Coming Soon: Builds Runner

We're thrilled to announce Builds Runner as a key feature in our next release.
This substantial progress in our build process will introduce a dedicated
service that actively handles pending builds. This will also act as an important
prerequisite for the upcoming features in Daytona.

We're excited to see how these updates impact your workflow. Try them out and
let us know what you think! Your feedback helps us continue to improve.

Have questions? Need more details? Don't hesitate to reach out. Join our Slack
[community](https://go.daytona.io/slack).

## References

- To learn more about the `Project Configs` refer to our recent release
  [notes](https://github.com/daytonaio/daytona/releases/tag/v0.24.0)
- Watch our office hours video on YouTube:
  [Daytona Office Hours #7](https://www.youtube.com/watch?v=nVQWa4jmwLc)
