---
title: 'Daytona container-registry feature explained'
description:
  'Learn how Daytona’s container registry enables reusable project
  configurations across multiple workspaces, using Docker to ensure consistency
  and speed up development environments.'
date: 2024-09-12
author: 'Oreoluwa Ajayi'
tags:
  ['Dev Containers', 'Container registry', 'Daytona', 'Docker', 'Development']
---

# Daytona container-registry feature explained

# Introduction

In modern development workflows, maintaining consistency across various
environments is critical to ensure seamless integration and collaboration.
[Daytona](https://www.daytona.io)’s container registry tackles this challenge by
allowing developers to store and reuse project configurations across multiple
workspaces. Powered by Docker, Daytona simplifies setup, reduces onboarding
time, and ensures consistency in development environments.

Docker plays a pivotal role here by packaging the development environment into
containers, ensuring that all dependencies, tools, and configurations are
bundled together. With Daytona’s integration, developers can quickly launch
these environments across different systems, avoiding the "works on my machine"
problem.

In addition to storing custom container images in Daytona’s registry, the
platform speeds up workspace creation by reusing images rather than rebuilding
them from scratch, allowing consistent environments across workspaces.

## TL;DR

- **Reusable Configurations**: Daytona’s container registry stores Docker-based
  project configurations for reuse across workspaces.
- **Easy Setup**: Simplifies setting up and managing Docker containers, reducing
  onboarding time.
- **Speed and Consistency**: Docker ensures that development environments remain
  consistent across different machines and platforms, while Daytona speeds up
  workspace creation by reusing container images.

## Adding a Project Configuration

Daytona allows developers to create reusable configurations, including Docker
containers, to maintain project consistency. This reduces the need for
repetitive setup, allowing you to define build configurations, environment
variables, and Docker-based setups.

**Steps to Create a Docker-Backed Project Configuration**:

- [x] Run the following command to start creating a project configuration:

  ```bash
  daytona project-config add
  ```

- [x] Enter the repository URL
      `e.g https://github.com/oreoluwa212/srcbooks-devcontainer` in the provided
      space.

- [x] Choose the **Docker-backed build configuration**. Daytona integrates with
      Docker to provide options such as:

  - **Automatic**: Daytona detects and sets up the container automatically based
    on project files.
  - **Devcontainer**: Use a predefined
    [Devcontainer](https://code.visualstudio.com/docs/remote/containers) file to
    define the Docker environment.
  - **Custom image**: You can also provide a custom Docker image for the
    project, stored and managed in Daytona's container registry.

- [x] Define the devcontainer path `.devcontainer/devcontainer.json`

- [x] Define environment variables in the format `KEY=VALUE`. To reference
      machine variables, use `$VALUE`.

- [x] Name the configuration, e.g., `new-book`. Daytona will store this
      configuration, allowing you to reuse the Docker-based setup across various
      workspaces. Reuse of pre-built container images from Daytona's registry
      ensures faster setup and avoids redundant builds.

- [x] Project configuration is successfully added

## Managing Docker-Based Project Configurations

Once created, Daytona provides intuitive commands to manage project
configurations stored in Docker containers. With Docker's containerization,
developers can ensure the same environment is used across different machines or
team members.

**View a Project Configuration**:

```bash
daytona project-config info
```

## Using Daytona's Container Registry to Launch a Workspace

Daytona’s standout container-registry feature is the ability to quickly select
and launch a workspace from its container registry. After creating and storing
Docker-backed project configurations, developers can instantly access these
workspaces without repeating the setup process.

Here’s how you can launch a containerized workspace using the `daytona code`
command:

1. Type the following command to start the process:

   ```bash
   daytona code
   ```

2. You'll be prompted to select a workspace from the available container
   configurations. These workspaces are based on pre-built Docker images stored
   in Daytona’s container registry, ensuring consistency and fast setup times.

3. Once selected, Daytona will pull the associated container image from the
   registry (if not already cached) and spin up the development environment in
   seconds, complete with all the dependencies and configurations.
   ![Select Workspace](/articles/assets/20240912_daytona_container_registry_img12.png)

    By leveraging this feature, you can instantly launch any containerized
    workspace, reducing the time it takes to set up and manage environments, which is particularly useful for teams working across multiple projects.

 4. Type the following command to view registry:

   ```bash
   daytona list
   ```

   ![Registry](/articles/assets/20240912_daytona_container_registry_img13.png)

## Setting a Custom Build Registry

Daytona allows developers to set a custom build registry for images built by the
Daytona builder. Once an image is built, it can be uploaded to a custom
container registry, speeding up the creation of future workspaces for the same
project.

## Prerequisites

Before setting a custom build registry, ensure you have an account on a
container registry with permission to push and pull images
`(e.g., Docker Desktop)`.

### Steps to Configure a Custom Build Registry

1. Open a terminal window and execute the following command:

   ```bash
   daytona container-registry set
   ```

   This command will prompt you to enter the necessary details.

2. Set the required options:

   - **Server URL**: Enter the full URL to your custom container registry.
   - **Username**: Provide the username Daytona should use to log in to the
     container registry.
   - **Password**: Enter the password for your registry account.

   After entering these details, press Enter to complete the configuration.

3. Configure the server by executing the following command:

   ```bash
   daytona server configure
   ```

   Press Enter repeatedly until the “Builder Registry” section is highlighted.

4. The interface will display a list of options for the builder registry. Select
   the custom registry you just configured using the Up/Down arrow keys. Press
   Enter until the command exits to save the configuration.

By setting up a custom build registry, you can store your Docker images securely
in a registry of your choice, speeding up workspace creation by reusing images
instead of building them from scratch.

## Conclusion

Daytona’s container registry, integrated with Docker, offers an efficient way to
manage and reuse project configurations. Docker’s ability to package
environments ensures consistency, while Daytona simplifies the process of
deploying and managing these containers across multiple workspaces. By
leveraging Daytona’s container registry, developers can not only ensure
consistency but also reduce setup times and enhance team collaboration.

Whether working with a devcontainer or a custom Docker image, Daytona’s project
configuration feature ensures that development remains smooth, efficient, and
adaptable to changes.

## References

- [Daytona Documentation](https://www.daytona.io)
- [Docker Overview](https://www.docker.com/get-started)
- [Dev Containers vs. Traditional Development Environments](https://www.daytona.io/dotfiles/dev-containers-vs-traditional-development-environments)
- [Daytona Projects Configuration documentation](https://www.daytona.io/docs/usage/projects)

---
