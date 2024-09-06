---
title: "A Beginner's Guide to Developing Inside Containers with VSCode"
description: "Step-by-step guide on setting up a development environment inside a container using VSCode. Learn the basics of containerization, common pitfalls, and how Daytona does it"
author: "Johnnie Oduro Jnr"
date: "2024-08-20"
tags: ["Containerization", "VSCode", "Development Environment", "Docker", "Daytona"] 
---

TL;DR
--------

Containerization packages your app for consistent use. This guide covers VSCode setup and Daytona’s approach.

A Beginner's Guide to Developing Inside Containers with VSCode
---------------------------------------------------------------

Introduction
---------------

Containerization ensures consistency. This guide covers VSCode setup, concepts, and Daytona tools.

What is Containerizattion
--------------------------

**[Containerization](https://www.daytona.io/definitions/c/containerization)** It bundles your app and its dependencies into a portable container that runs consistently anywhere, from local development to production.

**Why use it?**

1. **Consistency:** Your app behaves the same in every environment.
2. **Isolation:** Each app runs in its own space, avoiding conflicts.
3. **Portability:** Containers can be easily moved across different environments.

Setting Up Your Development Environment in a Container with VSCode
--------------------------------------------------------------------

Let's dive into setting up a development environment inside a container using VSCode.

Step 1: Install Docker
-----------------------

[Docker](https://www.daytona.io/definitions/d/docker) It's essential for creating and managing containers. Install it from the [Docker website](https://www.docker.com/products/docker-desktop).

After installation, confirm it's working by running:

```bash
docker --version
```

Step 2: Install VSCode
-----------------------

If you haven't already, grab Visual Studio Code from the [official site](https://code.visualstudio.com/).

Step 3: Install the Remote - Containers Extension
--------------------------------------------------

This VSCode extension allows you to work inside containers seamlessly.

- Open VSCode, go to Extensions (`Ctrl+Shift+X`), search for "Remote - Containers," and install it.

Step 4: Create a Dev Container Configuration
---------------------------------------------

1. **Open your project in VSCode:** Start by opening your project folder.
2. **Create a `.devcontainer` folder:** In your project root, create a `.devcontainer` folder.
3. **Add a `devcontainer.json` file:** This file defines your container's setup.
4. **Reopen in Container:** Click "Reopen in Container" to have VSCode automatically build and configure the environment.

Step 5: Start Coding
---------------------

Once the container is set up, you can code in a consistent, isolated environment. For example, if you're working on a Node.js app, you can run:

```bash
npm start
```

Your app will be accessible via `http://localhost:3000`.

Common Pitfalls and How to Avoid Them
--------------------------------------

1. **Large Image Sizes:** Big images can slow builds. Use lightweight images like `alpine`.

   **Example:**
    Replace `node:14` with `node:14-alpine`:

    ```json
      "image": "node:14-alpine"
    ```

2. **File Permissions:** Containers may cause permission issues. Use `remoteUser` to set correct permissions.

    ```json
      "remoteUser": "root"
    ```

   **Note:** Use `root` carefully due to security risks.

3. **Dependency Management:** Document your `devcontainer.json` to simplify future updates.

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

4. **Performance Issues:** Containers can slow large projects; minimize Dockerfile layers to optimize.

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

How Daytona Simplifies Containerized Development
-------------------------------------------------

Daytona streamlines containerized development, ensuring consistent, reliable environments. Here’s how it enhances your workflow:

1. **Standardized Environments:** Daytona’s `devcontainer.json` ensures consistent setups for all developers, reducing configuration issues and speeding up onboarding.

   **Example:**

   ```json
   {
     "name": "Daytona Dev Container",
     "image": "mcr.microsoft.com/devcontainers/base:alpine-3.18",
     "extensions": [
       "dbaeumer.vscode-eslint",
       "ms-python.python"
     ],
     "postCreateCommand": "npm ci" //Installs a package and all its dependencies.
   }
   ```

2. **Custom Docker Images:** Daytona allows teams to create tailored Docker images with essential tools, libraries, and configurations, avoiding "works on my machine" issues.

   **Steps to Create:**
   - Build the image:

     ```bash
     docker build -t mcr.microsoft.com/devcontainers/base:alpine-3.18
     ```

   - Push to a registry:

     ```bash
     docker push mcr.microsoft.com/devcontainers/base:alpine-3.18
     ```

3. **Automated Setup:** Daytona’s `devcontainer.json` automates setup and dependency installation, so developers can start coding immediately.

   **Example:**

   ```json
   "postCreateCommand": "npm ci && npm run setup"
   ```

4. **Consistency Across Platforms:** Daytona provides a uniform development experience across OSs, simplifying collaboration and avoiding discrepancies.

Incorporating Daytona’s tools boosts efficiency and reliability in containerized development, letting your team focus on coding rather than managing environments

Conclusion
----------

Containerization is vital for modern development, ensuring consistent app performance and streamlining workflows by isolating dependencies and configurations.

VSCode's Remote - Containers extension sets up a production-like environment, reducing "works on my machine" issues and streamlining development.

Daytona standardizes environments and automates setups, letting your team focus on coding, making development more efficient and productive
---
