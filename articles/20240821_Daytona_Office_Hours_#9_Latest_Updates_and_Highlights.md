---
title: "Daytona Office Hours #9: Latest Updates and Highlights"
description: "This article covers the recent updates and highlights from the Daytona Office Hours #9 YouTube video."
date: 2024-08-21
author: "Ivan Dagelić"
tags: ["pre-builds", "project-configs", "latest", "update", "highlights"]
---

# Latest Updates and Highlights

*Hello, Daytona community! welcome back to another episode of Daytona Office Hours.* 

*In this "office hours", we deep dive into a detailed demo of our new pre-builds feature. Updates on project configurations and how they speed up development. Recent fixes and improvements on the repo.*

### TL;DR

- **New features**
     - **[project-config](https://github.com/daytonaio/daytona/pull/789)**: Users can now define and manage project configurations.
     - **[pre-builds](https://github.com/daytonaio/daytona/pull/912)**: Allows users to speed up development and run builds.

- **Fixes**
     - **[.devcontainer.json detection](https://github.com/daytonaio/daytona/pull/943)**: Fixed the `devcontainer.json` file detection.
     - **[Binary Download Interruptions](https://github.com/daytonaio/daytona/pull/942)**: binary download interruptions are now fixed by use `wget` instead of `curl` to download the binary.
     - **[Version mismatch](https://github.com/daytonaio/daytona/pull/941)**: We have fixed version mismatch warning displaying wrong versions.


## New features

### 1. Project-configs
*As we introduced in the last release. The introduction of **project-configs** allows users to create reusable templates, streamlining the project setup process. Project configurations ease the definition of key parameters such as repository settings, environment variables, and build configurations, making it easier for new and existing users to initialize their projects efficiently.*


### 2. Pre-builds

*This new release introduces prebuilds. The project configurations are **pre-builds**, which are designed to enhance efficiency further. This feature enables users to set up automatic builds that are triggered by specific Git events, such as commits or pushes. The caching of builds significantly reduces setup time and helps maintain consistency across development environments.*

*[Watch](https://youtu.be/7WZdv0ccGOU?si=ijcsn7pFrLMK7DFd&t=163) me demonstrate the process of setting up prebuilds, showcasing the intuitive interface and the customization options available for users.*


> [!NOTE] NOTE: GitHub is currently the only git provider that supports prebuilds.

*Using `daytona prebuilds add` opens a view that lets asks the user to select a project configuration and the Git branch they plan to work on. The user can then decide on a commit interval after which a build should be triggered as well as any specific trigger files whose changes should immediately start the build process.*

![pre-builds demo](/articles/assets/20240821_Daytona_Office_Hour_%209_Latest_Updates_and_Highlights_img1.png)

*[Consequent `daytona create` calls will automatically detect the most recent existing build and use it to create the project much faster.]*

![pre-builds demo](/articles/assets/20240821_Daytona_Office_Hour_Latest_Updates_and_Highlights_img2.png)

*`daytona build list` and `daytona build logs` allow the user to view the builds and their information or debug the process. `daytona build rm --all` lets the user delete the builds to clear up space.*

![pre-builds demo](/articles/assets/20240821_Daytona_Office_Hour_Latest_Updates_and_Highlights_img3.png)

*The prebuilds work by registering a listener to webhook event from the Git provider by sending a public API endpoint that the Git provider will send requests to. Currently only GitHub is supported, but more options are coming soon.*

![pre-builds demo](/articles/assets/20240821_Daytona_Office_Hour_Latest_Updates_and_Highlights_img4.png)

## Major milestones

*The launch of project configurations and prebuilds marks significant steps toward streamlined development practices.*

## community announcements

- If you are using Daytona and encounter any bugs please feel free to open an issue.
- We are happy to welcome new contributors.
- We will help you solve the issue, so feel free to ask questions inside of the issue or PRs.
- Also, don't forget to star the repo and follow social handles.
- Currently, there are [19 open bounties](https://github.com/daytonaio/daytona/issues?q=is%3Aissue+is%3Aopen+label%3A%22%F0%9F%92%8E+Bounty%22).    
- Few of them are assigned to someone already but most of them open to anyone.
- Some of the priority issues we really love to be solved immeditely are 
    - [charm.sh integration](https://github.com/daytonaio/daytona/issues/513)
    - [the TUI breaking under pressure](https://github.com/daytonaio/daytona/issues/668)
    - [TUI breaks on Daytona create](https://github.com/daytonaio/daytona/issues/665)
- We hope to see you around Daytona.

## Conclusion

*The recent developments related project configurations, prebuilds, and bug resolutions all contribute to creating a more efficient user experience. As the project continues to evolve, user engagement and contribution will remain crucial. We Ensure that the Daytona project will always strive to meets the diverse needs of its community.*

## References

*For more information, users can access the resources associated with these updates provided below. Engage with the community to stay informed about further developments. Help us with your expertise to make Daytona better.*

- [Daytona Office Hours #9 YouTube Video](https://www.youtube.com/watch?v=7WZdv0ccGOU)
- [Daytona Documentation](https://daytona.io/docs)
- [Daytona Dotfiles](https://daytona.io/dotfiles)
- [Daytona GitHub Repository](https://github.com/daytonaio/daytona/)
- [Daytona Community Slack](https://go.daytona.io/slack)

