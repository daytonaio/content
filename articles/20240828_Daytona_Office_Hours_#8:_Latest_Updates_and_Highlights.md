---
title: "Daytona Office Hours #8: Latest Updates and Highlights"
description: "This article covers the recent updates and highlights from the Daytona Office Hours #8 YouTube video."
date: 2024-08-21
author: "Toma Puljak"
tags: ["Server", "Port", "Notification", "update", "highlights"]
--- 

# Daytona Office Hours #8: Latest Updates, Fixes & Future Plans!

*Hello everyone! Welcome back to yet another Daytona Office Hours. Where, as always we discuss what we released in the last week and what we plan on releasing next week. Also, where we answer any questions around Daytona and discuss open issues and much more. Come join us in the next Daytona Office Hours.*

*In this iteration of Daytona Office Hours we discussed, the latest release v0.25.0. Quality-of-life improvements and new features.Upcoming plans for the next release.*

## Features

*The release we had since last week was realease 025.0. If you remember the week before we had a big release regarding the introduction of `project-configs`. While the new release 0.25.0 does have a lot of notes. Its mostly quality-life fixes and improvements with two more subtle features.*

1. Server Port Notification

*Let's dive in, the first feature is to notify users, if server ports are taken. This feature is essentially a quality of life change.This feature essentially makes Daytona, check ports by the API server, SQL server and local registry. If the ports are busy this features notifies the users to either stop using the port or to change the port of the corresponding service.* 

2. Builds Runner (Stealth Mode)

*We have a feature by our Luca which is about adding the build runner. This feature is currently in stealth mode not used by Daytona currently but its a big part of what will make a prebuilds feature. We hope release it in the next few weeks.*

## Fixes

1. *Allow users to submit the form earlier, this fix was proposed by me. It's a quality of life change regarding the server. The server configure form has a lot of inputs in groups. If you want to change the first input then you have to click the submit button a lot of times. With this fix you can just `ctrl + s` and it will save the form prematurely.*

2. *Change URL for repo API response object. This is minor fix where we changed up the json structure of the return response.*

3. *Check registry ports after removal, nothing really worth mentioning here.*

4. *Add check for Docker requirements in local container registry start by Tarun. This is again a quality of life change. This fix adds checking docker requirements while starting the local container registry server. Which basically checks if the binary Docker is installed and if its up and running. Then, it prints the appropriate message.* 

5. *Server configuration fails to make directory by Tarun again. This change is again regarding to server configuration.*

6. *Removed fatal on the project config select ctrl-c. This fixes the display of error and exits.*

7. *Daytona creation logs in Daytona is again a fix by me. This fixes the Daytona creation logs when you run Daytona create but while working on Daytona inside. When you spin up the Daytona server in development, while working in a Daytona project everything should work smoothly as earlier.*

8. *Server start fails if systemd file exists again a small quality of life change. This fix improves the error message if the systemd file exists while trying to start the server in demon mode.*

9. *Resolve websocket long-reader todos again minor change. This introduces some trace logs into the web socket.*

10.* Proper API JSON validation again a fix by me. This is a huge change in the swagger specification. This is the only breaking change of this release. With this change we introduced proper required properties in swagger documentation and the API validation as well. Now the entire object that goes into our API needs to be structured accordingly.*


## breaking changes

*The breaking change is regarding to services that rely on our Swagger files and any tools that generate API clients from the definition.*

## Chores

1. *Swagger version revert update*

2. *Chose to use different config directory in development mode. This is again a fix for working with Daytona inside Daytona. Now when you start up Daytona in a dev container it will use Daytona-dev directory not Daytona so that we can have seperate configs with when running Daytona in development mode and production productions mode.* 

3. *Refactoring the purge cmd. Now the purge command requires user to stop the Daytona server before starting it before the user required to start the server. Now the purge command handles starting the server automaitcally and deletes all the workspaces. Also, this fixes the wiping the volume of the local container registry.*

4. *Added some unit tests for the internal package.* 




### TL;DR

## new releases
## patches
## general news
- *We really apprecciate the contributors, especially those who are willing to write tests for our packages.*
- 
