---
title: "Creating a Development Container: A Step-by-Step Guide"
description: "A comprehensive guide on setting up a standardized development environment inside a container using Docker and VSCode, including basic concepts, benefits, and common pitfalls."
date: 2023-08-20
author: "Vikash Prem Sharma"
---

# Creating a Development Container: A Step-by-Step Guide

## Introduction

Creating a development container involves setting up a standardized and reproducible development environment that can run consistently across different workstations or CI/CD environments. This guide will walk you through the process of creating a basic development container using Docker and Visual Studio Code (VSCode).

## What Are Dev Containers?

Dev containers are isolated, lightweight environments that allow developers to work inside a containerized version of a build environment. Essentially, dev containers provide a pre-configured development environment right inside your editor or IDE.

Some of the main benefits of using dev containers include:

- **Pre-configured Build Environments**: Dev containers come with a base image that has all the software, tools, and dependencies pre-installed, so you can get started coding right away.
- **Isolated Environments**: Each dev container has its own isolated filesystem, networking, memory, and CPU, so there are no conflicts with other projects or software on your local machine.
- **Reproducible Builds**: Dev containers provide the exact same environment every time they're launched, ensuring consistent build results. No more "it works on my machine!" issues.
- **Less Setup Time**: Starting a new project with dev containers means you can skip the lengthy setup and configuration process. Just open your project in the container and everything is ready to go.
- **Flexibility**: You can choose a base image with the software and tools you want or build your own custom base image, meeting your specific needs.

Dev containers revolutionize the developer experience by providing pre-configured, isolated environments that can supercharge your productivity. If you haven't tried them yet, you owe it to yourself as a developer to give dev containers a shot. They may just change the way you work! The future is containerized!

## Prerequisites

Before you begin, ensure you have the following:

- **Docker**: Installed and running on your machine.
- **VSCode**: Installed with the Remote - Containers extension.
- **Basic Familiarity**: With Docker and VSCode.

## Step 1: Create a `Dockerfile`

A Dockerfile specifies the instructions to create the image for your development environment. Follow these steps:

1. **Create a Directory**: For your project and navigate into it.

   ```sh
   mkdir my-dev-container && cd my-dev-container

   ```

2. **Create a Dockerfile**: Inside the directory, create a file named Dockerfile with the following content:

   ```sh
   FROM ubuntu:20.04

   # Avoid warnings by switching to noninteractive
   ENV DEBIAN_FRONTEND=noninteractive

   # Use the default user 'developer'
   ARG USERNAME=developer
   ARG USER_UID=1001
   ARG USER_GID=$USER_UID

   # Create the user 'developer' with sudo access
   RUN groupadd --gid $USER_GID $USERNAME \
       && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
       && apt-get update \
       && apt-get install -y sudo \
       && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
       && chmod 0440 /etc/sudoers.d/$USERNAME

   # Install development tools
   RUN apt-get install -y git build-essential

   # Switch back to the dialog frontend for any additional apt-get installations
   ENV DEBIAN_FRONTEND=dialog
   ```

## Step 1: Create a `devcontainer.json` File

The devcontainer.json file describes how VSCode should interact with the development container. In the same directory, create a file named devcontainer.json with the following content:

    ```sh
    {
    "name": "My Development Container",
    "build": {
        "dockerfile": "Dockerfile",
        "args": {
        "USER_UID": "1001",
        "USER_GID": "1001"
        }
    },
    "remoteUser": "developer"
    }

This file tells VSCode to build the development container image using the Dockerfile in the current directory and set the remote user to `developer`.

### Step 3: Open the Project in VSCode

1. **Open the Directory**: You created in VSCode.
2. **Reopen in Container**: Press `F1` to open the command palette and select `Remote-Containers: Reopen in Container`. This will build the Docker image if it's not already built and start a container with your development environment, attaching VSCode to it.

### Step 4: Develop Inside the Container

Now you are inside a containerized development environment. You can open a terminal in VSCode, and you'll be interacting with the shell inside the container. Install your project's dependencies, develop your code, and run your applications all within the container. You can add more tools and dependencies you need for your project by modifying the Dockerfile and rebuilding the container.

### Conclusion

By following these steps, you can create a consistent and isolated development environment using Docker and VSCode. This setup ensures that your development environment is reproducible and portable, making it easier to collaborate with other developers and deploy your applications.

Feel free to ask if you have any questions or need further assistance!

### References

- [Ultimate Guide to Dev Containers](https://www.daytona.io/dotfiles/ultimate-guide-to-dev-containers)
- [Creating a Development Container](https://www.daytona.io/dotfiles/creating-a-development-container)
- [Demo | Run the server in VS-Code](https://www.youtube.com/watch?v=uL-TaEhvVwk)
