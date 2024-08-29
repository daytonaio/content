---
title: "A Beginner's Guide to Developing Inside Containers with VSCode"
description: "Step-by-step guide on setting up a development environment inside a container using VSCode. Learn the basics of containerization, common pitfalls, and how Daytona does it."
author: "Johnnie Oduro Jnr."
date: "2024-08-20"
tags: ["Containerization", "VSCode", "Development Environment", "Docker", "Daytona"] 
---

## TL;DR

Containerization packages your app and its dependencies into a single, portable unit that runs consistently across different environments. This guide walks you through setting up a development environment inside a container using VSCode, covering basics, pitfalls to avoid, and Daytona's approach.

## A Beginner's Guide to Developing Inside Containers with VSCode

### Introduction

Containerization is a game-changer for development, ensuring your app runs the same everywhere. If you're new to this, don't worry—VSCode makes it simple. In this guide, we'll cover setting up a containerized development environment in VSCode, highlight common pitfalls, and share how Daytona does it.

### What is Containerization?

**Containerization** lets you bundle your application and its dependencies into a single, portable container. This container can run consistently in any environment, from local development to production. Read more about [containerizatoin here](https://www.daytona.io/definitions/c/containerization)

**Why use it?**
1. **Consistency:** Your app behaves the same in every environment.
2. **Isolation:** Each app runs in its own space, avoiding conflicts.
3. **Portability:** Containers can be easily moved across different environments.

### Setting Up Your Development Environment in a Container with VSCode

Let's dive into setting up a development environment inside a container using VSCode.

#### Step 1: Install Docker

[Docker](https://www.daytona.io/definitions/d/docker) is essential for creating and managing containers. Install it from the [Docker website](https://www.docker.com/products/docker-desktop).

After installation, confirm it's working by running:

```bash
docker --version
```

#### Step 2: Install VSCode

If you haven't already, grab Visual Studio Code from the [official site](https://code.visualstudio.com/).

#### Step 3: Install the Remote - Containers Extension

This VSCode extension allows you to work inside containers seamlessly.

- Open VSCode, go to Extensions (`Ctrl+Shift+X`), search for "Remote - Containers," and install it.

#### Step 4: Create a Dev Container Configuration

1. **Open your project in VSCode:** Start by opening your project folder.
2. **Create a `.devcontainer` folder:** In your project root, create a `.devcontainer` folder.
3. **Add a `devcontainer.json` file:** This file defines your container's setup.

**Example for a Node.js project:**

```json
{
  "name": "My Dev Container",
  "image": "node:14",
  "extensions": [
    "dbaeumer.vscode-eslint"
 ],
  "postCreateCommand": "npm install",
  "forwardPorts": [3000],
  "remoteUser": "node"
}
```

**Explanation:**
- **`image`:** The base image for your environment (Node.js 14 here).
- **`extensions`:** VSCode extensions to install inside the container.
- **`postCreateCommand`:** Commands to run after the container is set up (e.g., installing dependencies).
- **`forwardPorts`:** Ports to expose from the container to your local machine.
- **`remoteUser`:** The user to run commands inside the container.

4. **Reopen in Container:** VSCode will prompt you to reopen the folder in the container. Click "Reopen in Container," and VSCode will build and configure the environment automatically.

#### Step 5: Start Coding

Once the container is set up, you can code as usual, but your environment is now consistent and isolated. For example, if you're working on a Node.js app, you can run:

```bash
npm start
```

Your app will be accessible via `http://localhost:3000`.

### Common Pitfalls and How to Avoid Them

1. **Large Image Sizes:** Some images are big, slowing builds. Opt for lightweight images like `alpine` versions.

   **Example:**
 Replace `node:14` with `node:14-alpine`:

 ```json
   "image": "node:14-alpine"
 ```

2. **File Permissions:** Containers may cause permission issues. Use the `remoteUser` setting to match your desired permissions.

 ```json
   "remoteUser": "root"
 ```

   **Note:** Use `root` carefully due to security risks.

3. **Dependency Management:** Keep your `devcontainer.json` well-documented to make future updates easier.

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

4. **Performance Issues:** Containers might slow down your workflow, especially with large projects. Optimize by reducing Dockerfile layers.

   **Example:**

   **Before:**

 ```Dockerfile
   RUN apt-get update
   RUN apt-get install -y git
 ```

   **After:**

 ```Dockerfile
   RUN apt-get update && apt-get install -y git
 ```

### How Daytona Does It

At Daytona, we've streamlined our development with VSCode containers.

1. **Standardized Environments:** We use a `devcontainer.json` to ensure every developer works in the same environment.

   **Example:**

 ```json
   {
     "name": "Daytona Dev Container",
     "image": "daytona/base-image:latest",
     "extensions": [
       "dbaeumer.vscode-eslint",
       "ms-python.python"
     ],
     "postCreateCommand": "npm ci"
   }
 ```

2. **Custom Docker Images:** We build custom images with all the tools our projects need, avoiding "works on my machine" issues.

   **Steps to Create:**
   - Build the image:

 ```bash
     docker build -t daytona/base-image:latest .
 ```

   - Push to a registry:

 ```bash
     docker push daytona/base-image:latest
 ```

3. **Automated Setup:** Our `devcontainer.json` automates setup, so developers can start coding immediately.

   **Example:**

 ```json
   "postCreateCommand": "npm ci && npm run setup"
 ```

 This ensures dependencies are installed, and the environment is configured.

4. **Consistency Across Platforms:** VSCode’s Remote - Containers extension keeps our development experience the same, whether on Windows, macOS, or Linux.

### Conclusion

Setting up a containerized development environment in VSCode is a great way to ensure consistency, portability, and isolation in your workflow. With these steps, you'll be up and running quickly, and you can take inspiration from Daytona's approach to streamline your process. Happy coding!

---
