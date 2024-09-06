---
title: "Daytona Office Hours #8 Summary"
description: "A comprehensive summary of the key points discussed during the Daytona Office Hours #8 session on youtube."
date: 2024-08-21
author: "Varun Seenivasan"
tags: ["updates", "new releases", "patches", "news"]
---

# Daytona Office Hours #8 Summary

## Introduction

The Daytona Office Hours #8 video covered releases v0.25.0 and v0.25.1 which presented a variety of bug fixes, new features, as well as chores and tests.


### TL;DR

* v0.25.0
  * Features:
    * PR #812: Users are notified if server ports are taken
    * PR #781: Builds runner added
  * Fixes:
    * PR #856: Users can submit TUI form prematurely with Ctrl + S
    * PR #900: Repo API now returns URL in a JSON object
    * PR #901: Moved registry port check to after removal
    * PR #902: Check for docker requirements in Local Container Registry Start
    * PR #908: Directory creation logic moved to the server
    * PR #899: Fatal error when ctrl-c-ing out of project config selection removed
    * PR #898: Allows Daytona creation logs
    * PR #903: Allows Daytona server start in daemon mode if another daemon server exists
    * PR #916: Resolved websocket log-reader todos
    * PR #905: All request objects coming to the API are properly validated
  * Chores and tests:
    * PR #893: Readme update
    * PR #896 Reverted Swagger version update
    * PR #883 Use different config directiory in development mode
    * PR #909 Bumped github.com/docker/docker from 26.1.4+incompatible to 26.1.5+incompatible
    * PR #897 Refactored purge command
    * PR #887 Created unit tests for various packages
  * v0.25.1 - PR #921: Docker installation check 

## v0.25.0

Full changelog: https://github.com/daytonaio/daytona/compare/v0.24.0...v0.25.0

### Features

#### #812: Users are notified if server ports are taken
In this feature, if server ports of the API server, Headscale server, or local registry are already occupied, the user will be notified.

by @ezhil56

https://github.com/daytonaio/daytona/pull/812


#### #781: Builds runner added 
This feature refactors and updates the existing build logic to work with a new build runner. The build runner now includes functionality to automatically retry builds that are in a pending state. 

by @lbrecic

https://github.com/daytonaio/daytona/pull/781


### Bug Fixes

#### #856: Users can submit TUI form prematurely with Ctrl + S
This fix enables users to save the lengthy TUI form early using the [Ctrl + S] shortcut key.

by @harkiratsm

https://github.com/daytonaio/daytona/pull/856

#### #900: Repo API now returns URL in a JSON object
Instead of the Repo API response being a URL as a string, the response is now wrapped in a JSON object.

by @Tpuljak

https://github.com/daytonaio/daytona/pull/900

#### #901: Moved registry port check to after removal
This PR fixed a bug that occured when checking the registry by moving the check to after the port removal.

by @lbrecic

https://github.com/daytonaio/daytona/pull/901

#### #902: Check for docker requirements in Local Container Registry Start
This PR added a check for Docker requirements in Local Container Registry Start.

by @tarunrajput

https://github.com/daytonaio/daytona/pull/902

#### #908: Directory creation logic moved to the server
The command "daytona server configure" originally would fail because it attempts to create a directory on the CLI. This PR moved the creation logic to the server.

by @tarunrajput

https://github.com/daytonaio/daytona/pull/908

#### #899: Fatal error when ctrl-c-ing out of project config selection removed

by @idagelic

https://github.com/daytonaio/daytona/pull/899

#### #898: Allows Daytona creation logs
This PR fixed a bug that prevented the user from getting creation logs while running Daytona in Daytona.

by @Tpuljak

https://github.com/daytonaio/daytona/pull/898

#### #903: Allows Daytona server start in daemon mode if another daemon server exists
This fix allows Daytona server start in daemon mode even if another daemon server already exists.

by @lbrecic 

https://github.com/daytonaio/daytona/pull/903

#### #916: Resolved websocket log-reader todos
This PR introduced trace logs into the websocket log-reader.

by @lbrecic

https://github.com/daytonaio/daytona/pull/916

#### #905: All request objects coming to the API are properly validated
This PR significantly updated API validation, ensuring all incoming request objects are properly checked for required properties. These changes also affect the generated Swagger files and API client libraries.

by @Tpuljak

https://github.com/daytonaio/daytona/pull/905


### Chores and Tests

#### #893: Readme update
This PR added the documentation badge and link to the readme. Additionally, horizontal scroll was removed from the one-line install command.

by @idagelic

https://github.com/daytonaio/daytona/pull/893

#### #896 Reverted Swagger version update
The Swagger version will be kept at `v0.0.0-dev`.

by @Tpuljak

https://github.com/daytonaio/daytona/pull/896

#### #883 Use different config directiory in development mode
A minor fix to use a separate config directory when inside a devcontainer, making it easier to run Daytona within Daytona.

by @Tpuljak

https://github.com/daytonaio/daytona/pull/883

#### #909 Bumped github.com/docker/docker from 26.1.4+incompatible to 26.1.5+incompatible

by @dependabot

https://github.com/daytonaio/daytona/pull/909

#### #897 Refactored purge command
Servers will now be stopped when purging. Additionally, this PR added seperate purge processes for the tailscale server, provider manager, and local container registry.

by @Tpuljak

https://github.com/daytonaio/daytona/pull/897

#### #887 Created unit tests for various packages
This PR created unit tests for various packages: `cmd`, `apikey`, `constants`, `jetbrains`. This is embedded in the internal packages.  

by @Philip-21

https://github.com/daytonaio/daytona/pull/887

## v0.25.1

Full changelog: https://github.com/daytonaio/daytona/compare/v0.25.0...v0.25.1

### Fixes

#### #921: Installation guide added to docker info error message 
`LookPath` was not working on darwin so this PR added an installation guide to the docker info error message.

by @Tpuljak

https://github.com/daytonaio/daytona/pull/921

## References
v0.25.0 changelog - https://github.com/daytonaio/daytona/compare/v0.24.0...v0.25.0

v0.25.1 changelog - https://github.com/daytonaio/daytona/compare/v0.25.0...v0.25.1

"Daytona Office Hours #8 - Latest Updates, Fixes & Future Plans!" - 
https://www.youtube.com/watch?v=M0dndoz5UpQ
