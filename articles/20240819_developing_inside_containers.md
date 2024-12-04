---
title: "A Beginner's Guide to Developing Inside Containers with VSCode"
description:
  'Step-by-step guide on setting up a development environment inside a container
  using VSCode. Learn the basics of containerization, common pitfalls, and how
  Daytona does it'
author: 'Johnnie Oduro Jnr'
date: '2024-08-20'
tags:
  ['Containerization', 'VSCode', 'Development Environment', 'Docker', 'Daytona']
---

# TL;DR

Containerization packages your app and its dependencies into a single, portable
unit that runs consistently across different environments. This guide walks you
through setting up a development environment inside a container using VSCode,
covering basics, pitfalls to avoid, and Daytona's approach.

## A Beginner's Guide to Developing Inside Containers with VSCode

# Introduction

Containerization has transformed how developers build and deploy software,
ensuring applications run consistently across different environments. For those
new to this approach, VSCode offers a user-friendly way to dive in. This guide
will walk you through setting up a containerized development environment in
VSCode, covering key concepts, common pitfalls, and how tools like Daytona can
simplify and enhance the process by automating and standardizing your container
setup.

## What is Containerizattion

**[Containerization](https://www.daytona.io/definitions/c/containerization)** It
bundles your app and its dependencies into a portable container that runs
consistently anywhere, from local development to production.

**Why use it?**

1. **Consistency:** Your app behaves the same in every environment.
2. **Isolation:** Each app runs in its own space, avoiding conflicts.
3. **Portability:** Containers can be easily moved across different
   environments.

## Setting Up Your Development Environment in a Container with VSCode

Let's dive into setting up a development environment inside a container using
VSCode.

## Step 1: Install Docker

[Docker](https://www.daytona.io/definitions/d/docker) It's essential for
creating and managing containers. Install it from the
[Docker website](https://www.docker.com/products/docker-desktop).

After installation, confirm it's working by running:

```bash
docker --version
```

## Step 2: Install VSCode

If you haven't already, grab Visual Studio Code from the
[official site](https://code.visualstudio.com/).

## Step 3: Install the Remote - Containers Extension

This VSCode extension allows you to work inside containers seamlessly.

- Open VSCode, go to Extensions (`Ctrl+Shift+X`), search for "Remote -
  Containers," and install it.

## Step 4: Create a Dev Container Configuration

1. **Open your project in VSCode:** Start by opening your project folder.
2. **Create a `.devcontainer` folder:** In your project root, create a
   `.devcontainer` folder.
3. **Add a `devcontainer.json` file:** This file defines your container's setup.
4. **Reopen in Container:** Click "Reopen in Container" to have VSCode
   automatically build and configure the environment.

## Step 5: Start Coding

Once the container is set up, you can code in a consistent, isolated
environment. For example, if you're working on a Node.js app, you can run:

```bash
npm start
```

Your app will be accessible via `http://localhost:3000`.

## Common Pitfalls and How to Avoid Them

1. **Large Image Sizes:** Big images can slow builds. Use lightweight images
   like `alpine`.

   **Example:** Replace `node:14` with `node:14-alpine`:

   ```json
     "image": "node:14-alpine"
   ```

2. **File Permissions:** Containers may cause permission issues. Use
   `remoteUser` to set correct permissions.

   ```json
     "remoteUser": "root"
   ```

   **Note:** Use `root` carefully due to security risks.

3. **Dependency Management:** Document your `devcontainer.json` to simplify
   future updates.

   **Tip:** Add comments to your `devcontainer.json`:

   ```json
   {
     "name": "My Dev Container",
     "image": "node:14",
     "extensions": [
       "dbaeumer.vscode-eslint" // ESLint helps catch JavaScript issues
     ]
   }
   ```

4. **Performance Issues:** Containers can slow large projects; minimize
   Dockerfile layers to optimize.

   **Example:**

   1. **Before:**

      ```Dockerfile
        RUN apt-get update
        RUN apt-get install -y git
      ```

   2. **After:**

      ```Dockerfile
        RUN apt-get update && apt-get install -y git
      ```

## How Daytona Simplifies Containerized Development

Daytona provides a streamlined approach to containerized development, making it
easier for teams to work in consistent, reliable environments. Here’s how
Daytona’s tools can enhance your workflow:

1. **Standardized Environments:** Daytona’s `devcontainer.json` file for every
   project to ensure that all developers work in the same environment,
   regardless of their local machine setup. This standardization reduces
   configuration issues and speeds up onboarding.

   **Example:**

   ```json
   {
     "name": "Daytona Dev Container",
     "image": "mcr.microsoft.com/devcontainers/base:alpine-3.18",
     "extensions": ["dbaeumer.vscode-eslint", "ms-python.python"],
     "postCreateCommand": "npm ci" //Installs a package and all its dependencies.
   }
   ```

2. **Custom Docker Images:** Daytona allows teams to create custom Docker images
   tailored to their project needs. By including all necessary tools, libraries,
   and configurations in these images, developers can avoid the common "works on
   my machine" problems.

   **Steps to Create:**

   - Build the image:

     ```bash
     docker build -t mcr.microsoft.com/devcontainers/base:alpine-3.18
     ```

   - Push to a registry:

     ```bash
     docker push mcr.microsoft.com/devcontainers/base:alpine-3.18
     ```

3. **Automated Setup:** Daytona’s `devcontainer.json` configurations are
   designed to automate much of the setup process. This includes commands that
   run automatically after the container is built, such as installing
   dependencies, so developers can start coding immediately.

   **Example:**

   ```json
   "postCreateCommand": "npm ci && npm run setup"
   ```

4. **Consistency Across Platforms:** Daytona’s approach ensures a consistent
   development experience across different operating systems, making it easier
   for teams to collaborate without worrying about environment discrepancies.

Incorporating Daytona’s tools boosts efficiency and reliability in containerized
development, letting your team focus on coding rather than managing environments

## Conclusion

Containerization is essential for modern development, ensuring your app runs
consistently across different environments. It simplifies your workflow by
isolating dependencies and configurations, making your development process
smoother and more reliable.

VSCode, with its Remote - Containers extension, makes it easy to set up a
containerized environment that mirrors production. This approach minimizes the
"works on my machine" issue and streamlines development, testing, and
deployment.

## Daytona enhances this process by standardizing environments and automating setups, so your team can focus more on coding and less on environment management. By using tools like Daytona, you're embracing a more efficient and consistent way to develop, ultimately making your work easier and more productive
