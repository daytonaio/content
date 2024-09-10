---
title: "Introducing Daytona Project Config: Simplify and Streamline Workspace Setup"
description: "Learn how Daytona’s new Project Configs simplify project creation and management with predefined configurations."
date: 2024-09-10
author: "Daytona"
tags: ["Project Config", "Daytona", "Development", "Prebuilds"]
---

# Introducing Daytona Project Config: Simplify and Streamline Workspace Setup

## Introduction

For modern developers, creating and maintaining consistent [development environments](/definitions/20240819_definition_development%20environment.md) can often feel repetitive and time-consuming. Every time you start a new project or set up a new [workspace](/definitions/20240819_definition_daytona%20workspace.md), you may find yourself manually configuring [repositories](/definitions/20240819_definition_repository.md), environment variables, and build settings from scratch. As project complexity increases, so do these overhead tasks, potentially slowing down your **developer velocity**.

What if there was a way to automate these processes and maintain consistency across all your workspaces? Enter **Daytona’s Project Configs**, a powerful new feature introduced in **v0.24.0** ([see release notes](https://github.com/daytonaio/daytona/releases/tag/v0.24.0)) designed to simplify workspace setup by allowing you to predefine project settings that can be reused across multiple environments. Whether you’re managing multiple repositories or frequently spinning up new development environments, Project Configs can save you hours of configuration time.

> **“The idea behind Project Configs is to give developers a quick, efficient way to set up their projects without having to constantly reconfigure everything. It’s a time-saver and a consistency booster.”** – Daytona Dev Team

### TL;DR
- **What are Project Configs?** A feature introduced in [Daytona v0.24.0](https://github.com/daytonaio/daytona/releases/tag/v0.24.0) for predefining workspace settings to reduce setup time.
- **Why use them?** Save setup time, ensure consistency across environments, and streamline workflows.
- **Key Features:** Automatically configure Git repository URLs, build settings (e.g., `devcontainer.json`), and environment variables in `KEY=VALUE` format.
- **Future Development:** Project Configs will soon integrate with [Prebuilds](https://www.daytona.io/docs/usage/prebuilds), enhancing workspace readiness.

---

## What Is Daytona Project Config?

At its core, **Daytona Project Config** is an entity that contains all the essential information necessary to create a **development project** within a [workspace](/definitions/20240819_definition_daytona%20workspace.md). A Project Config stores critical details like the [Repository URL](/definitions/20240819_definition_repository.md), **build configurations**, and environment variables, making it easy to reuse these settings whenever you need to create a new workspace. For a deeper understanding of how it works, check out the official [Daytona Project Configuration Usage guide](https://www.daytona.io/docs/usage/projects/#project-configuration).

**Why is this important?**

For developers working in teams or managing multiple projects, it’s essential to maintain a uniform [development environment](/definitions/20240819_definition_development%20environment.md) to avoid issues like version mismatches, missing dependencies, or inconsistent build processes. Project Configs not only save time but also ensure that the environments are consistent and reproducible.

### Key Features of Project Configs

- **Repository URL**: Specifies the Git repository linked to your project.
- **Build Configuration**: Choose between automatic detection, using a `devcontainer.json` file, custom image builds, or the default Daytona base image.
- **Environment Variables**: Set essential environment variables for the build and runtime environments in `KEY=VALUE` format.
- **Configuration Name**: Each Project Config has a unique identifier that distinguishes it from other configurations.

According to recent surveys, up to **40% of a developer’s time** can be spent on environment setup and configuration, especially in larger organizations. By using Daytona’s Project Configs, developers can significantly cut down on this overhead and focus more on coding.

---

## Benefits of Project Configs for Developers

### Consistency Across Environments

One of the primary advantages of using Project Configs is that they ensure a consistent [development environment](/definitions/20240819_definition_development%20environment.md) across multiple workspaces. Whether you’re switching between projects or collaborating with other developers, the environment will always be identical, reducing the likelihood of "[works on my machine](/definitions/20240819_definition_works%20on%20my%20machine%20syndrome.md)" issues.

### Reusability and Automation

With Project Configs, you don’t have to reinvent the wheel every time you create a new workspace. By storing repository and environment settings in a Project Config, you can easily reuse them across projects. This level of automation not only saves time but also helps avoid human errors that can occur during manual setup.

### Faster Onboarding

New developers joining a project or team can benefit from Project Configs by having a predefined, ready-to-use [development environment](/definitions/20240819_definition_development%20environment.md). This eliminates the learning curve of setting up an environment from scratch and ensures that new team members are productive from day one.

---

## Step-by-Step Guide: Creating a New Project Config

Let’s dive into the actual process of creating a Project Config in Daytona. Here’s how you can get started:

### 1. Add a New Project Config

Open your terminal and run the following command:

```bash
daytona project-config add
```

You’ll be prompted to enter key information for the configuration, such as the [repository URL](/definitions/20240819_definition_repository.md), build configuration, and environment variables.

For example:

```bash
daytona project-config add
> Enter repository URL: https://github.com/user/repo
> Select build configuration: Devcontainer
> Enter environment variables: ENV_VAR=production
> Name your project config: MyProjectConfig
```

This simple set of inputs ensures that the next time you create a workspace, Daytona will automatically load these settings, significantly reducing setup time.

### 2. Sample Repository for Project Config

Let’s set up a Project Config for the [Daytona Sample TypeScript Node Project](https://github.com/daytonaio/sample-typescript-node), which includes a basic Node.js app and a `devcontainer.json` for an easy development setup.

Here’s how to create the Project Config:

```bash
daytona project-config add
> Enter repository URL: https://github.com/daytonaio/sample-typescript-node
> Select build configuration: Devcontainer
> Enter environment variables: NODE_ENV=development
> Name your project config: SampleTypeScriptNodeConfig
```

Once saved, you can apply this configuration to multiple workspaces, ensuring that each workspace has the same repository and environment setup. To create a new workspace with this setup, use:

```bash
daytona create
> Select project config: SampleTypeScriptNodeConfig
```

This process will quickly set up your workspace with the same configuration, making it easy to get started.

---


## Managing Your Project Configs

Once you’ve created a Project Config, Daytona provides several commands to manage and view these configurations. You can explore these commands in more detail in the [Daytona CLI Reference for Project Config](https://www.daytona.io/docs/reference/cli/#daytona-project-config). Here are some key operations:

### Listing All Project Configs

To list all your existing Project Configs, use the command:

```bash
daytona project-config list
```

This will display a table with the Project Config name, associated repository, build configuration, and whether it's set as the default.

```bash
Name                       Repository                                           Build         Default
──────────────────────────────────────────────────────────────────────────────────────────────────────
SampleTypeScriptNodeConfig https://github.com/daytonaio/sample-typescript-node  Devcontainer    Yes
```

### Viewing Details of a Project Config

To see the details of a specific Project Config, run:

```bash
daytona project-config info
```

Select the configuration you want to view, and Daytona will display details such as the repository URL, build configuration, and any environment variables associated with it. For example, you might see information like this:

```bash
Project Config Info:
---------------------
Name: sample-typescript-node
Repository: https://github.com/daytonaio/sample-typescript-node.git
Default: Yes
Build: Devcontainer
Devcontainer path: .devcontainer/devcontainer.json
```

This output provides a structured view of the Project Config, showing key details such as the repository URL, build configuration, and the path to the development container configuration.


---

## Updating or Deleting Project Configs

### Updating a Project Config

If you need to change settings within an existing Project Config, Daytona makes it easy. Simply run:

```bash
daytona project-config update
```

You’ll be prompted to select the Project Config you want to update and then modify any of the settings, such as changing the repository URL or adding new environment variables.

### Deleting a Project Config

If a configuration is no longer needed, you can remove it using the following command:

```bash
daytona project-config delete
```

This will remove the configuration from Daytona, ensuring your workspace remains clean and organized.

---

## What's Next: Project Configs and Prebuilds

The introduction of Project Configs is part of Daytona’s broader initiative to improve developer efficiency by automating repetitive tasks. One upcoming feature that will further streamline the development process is **Prebuilds**.

### How Prebuilds Will Enhance Project Configs

Prebuilds allow for even faster workspace setup by listening for changes in the underlying repository and automatically running builds in the background. This ensures that when a developer creates a new workspace, all necessary builds have already been completed, significantly reducing wait times.

> **"Prebuilds are designed to take Daytona’s automation to the next level, allowing for 'ready-to-go' environments. Coupled with Project Configs, they’ll make workspace creation nearly instantaneous."** – Daytona Engineering Team

---

## Conclusion

Daytona’s **Project Configs** bring a significant improvement to workspace setup by reducing the time and effort needed to configure repositories, environment variables, and build settings. Whether you’re a solo developer or part of a larger team, the ability to define and reuse configurations can dramatically enhance your productivity.

As Daytona continues to roll out features like **Prebuilds**, the development experience will only get faster and more efficient, allowing developers to spend less time on setup and more time coding.

```bash
# Commands Recap
daytona project-config add
daytona project-config list
daytona project-config info
daytona project-config update
daytona project-config delete
```

For more detailed documentation, visit the official [Daytona CLI Reference](https://www.daytona.io/docs/reference/cli/#daytona-project-config) or explore the comprehensive [Project Configuration Usage Guide](https://www.daytona.io/docs/usage/projects/#project-configuration).
