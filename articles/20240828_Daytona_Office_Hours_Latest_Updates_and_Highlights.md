---
title:
  'Daytona Ecosystem: Server Port Notifications, Latest Developments And
  Improvements'
description:
  'The latest updates, major fixes, upcoming developments, and highlights
  discussed during Daytona Office Hours 8 YouTube video.'
date: 2024-08-21
author: 'Team Daytona'
tags: ['Update', 'News', 'Release', 'DOH']
---

At Daytona, we're excited to announce that this week's release includes progress
on _server port notifications_ and _builds runner_ features. Quality-of-life
fixes we have been working on and much more. Let's dive in and see what's new,
and get a glimpse of what's ahead.

# TL;DR

- **Server Port Notification:** Notify users if server ports are busy.
- **Server Configuration Form Submission:** Early form submission with `Ctrl+S`
  for easier server configuration.
- **API JSON validation:** Introduction of proper required properties in the
  Swagger documentation and API validation.

## What's New in This Release

We have two significant features to hightlight this week: server port
notifications and builds runner.

### Server Port Notifications

**Server port notifications**, a subtle addition, automatically checks for port
conflicts with the API server, SQL server, and local registry. If any of the
ports are occupied, Daytona will alert you, allowing you to either free up the
port or adjust the corresponding service settings.

### Builds Runner

We have also introduced a new feature **builds runner**, that will eventually
enable pre-builds. While currently in stealth mode and not yet integrated into
Daytona, this build runner feature is a crucial component of our pre-builds
functionality. We anticipate releasing it within the next few weeks.

## Major Fixes And Progress

- **Allow users to submit the form earlier:** This fix allows users to save the
  server configuration form more efficiently. Instead of repeatedly clicking the
  submit button after each change, you can now press `Ctrl+S` to save the form
  at any time.
- **Docker Requirement Check:** Now, when you start the local container
  registry, Daytona will verify that Docker is installed and running correctly.
  This ensures a smoother startup process.
- **Server Configuration Directory Fix:** Corrects directory creation for remote
  profiles. Previously, when you modified a directory path in the server
  configuration for a remote profile, Daytona would automatically attempt to
  create the directory on your local machine. This update now prevents
  unnecessary directory creation on the host machine when using remote profiles.
- **Daytona Creation Logs:** We've fixed an issue that affected Daytona creation
  logs. Now, when you create a new Daytona project, the logs will display
  correctly, ensuring a smoother development experience while working on Daytona
  inside Daytona.
- **Proper API JSON validation:** We've implemented a significant change to our
  API's Swagger specification. This update ensures strict JSON validation,
  requiring all API requests to adhere to a precise structure.

## Breaking Changes

_We've significantly improved our API's Swagger specification to include strict
validation for required properties. This change ensures that API clients
generated from our Swagger definition adhere to the correct structure,
preventing potential errors and inconsistencies. While this is the only breaking
change in this release, it's essential for maintaining API consistency and
reliability._

## Patches

- **Different Config Directory:** To avoid conflicts when working on Daytona
  within a Daytona project, we now use a different configuration directory in
  development mode. This allows you to have distinct settings for development
  and production environments.
- **Purge Command Enhancement:** We've simplified the purge command. Now,
  instead of manually stopping and starting the Daytona server, the command
  automatically handles these steps and efficiently deletes all workspaces.
  Additionally, we've fixed an issue that prevented the local container registry
  volume from being wiped clean.

## Coming Soon: Pre-Builds and Multiple IDs Support For Git Providers

We're not slowing down! Here's what we're working on for the near future:

1. **Pre-Builds Feature:** Ability to configure pre-builds for quicker startup
   times. Accelerates project startup with pre-built images or dev containers.
   This feature eliminates the need for lengthy build processes, allowing you to
   dive into your projects more quickly.
2. **Multiple Identities Support for Git Providers:** Support users with
   multiple GitHub accounts. This will provide greater flexibility and
   convenience for users working with multiple accounts.
3. **Commit URL Clone Fix:** Ensures successful cloning of repositories from
   non-main branches.

## Conclusion

We hope these updates excite you as much as they do us. Excited to see how
you'll use them to streamline your work. We are commited to offer the best
possible experience for Daytona users and developers. Stay tuned for more
updates as we continue to innovate.

Want to learn more or have questions? Join our Slack community:
[Daytona Community Slack](https://go.daytona.io/slack).

## References

- Watch our office hours on YouTube:
  [Daytona Office Hours #8 YouTube Video](https://youtu.be/M0dndoz5UpQ)
- Checkout the latest release that we discussed during the session:
  [Daytona Releases Page](https://github.com/daytonaio/daytona/releases/tag/v0.25.0)
