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

Containerization has transformed how developers build and deploy software, ensuring applications run consistently across different environments. For those new to this approach, VSCode offers a user-friendly way to dive in. This guide will walk you through setting up a containerized development environment in VSCode, covering key concepts, common pitfalls, and how tools like Daytona can simplify and enhance the process by automating and standardizing your container setup.

### What is Containerization?

**[Containerization](https://www.daytona.io/definitions/c/containerization)** lets you bundle your application and its dependencies into a single, portable container. This container can run consistently in any environment, from local development to production.

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

### How Daytona Simplifies Containerized Development

Daytona provides a streamlined approach to containerized development, making it easier for teams to work in consistent, reliable environments. Here’s how Daytona’s tools can enhance your workflow:

1. **Standardized Environments:** Daytona uses a `devcontainer.json` file for every project to ensure that all developers work in the same environment, regardless of their local machine setup. This standardization reduces configuration issues and speeds up onboarding.

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

2. **Custom Docker Images:** Daytona allows teams to create custom Docker images tailored to their project needs. By including all necessary tools, libraries, and configurations in these images, developers can avoid the common "works on my machine" problems.

   **Steps to Create:**
   - Build the image:

     ```bash
     docker build -t mcr.microsoft.com/devcontainers/base:alpine-3.18
     ```

   - Push to a registry:

     ```bash
     docker push mcr.microsoft.com/devcontainers/base:alpine-3.18
     ```

3. **Automated Setup:** Daytona's `devcontainer.json` configurations are designed to automate much of the setup process. This includes commands that run automatically after the container is built, such as installing dependencies, so developers can start coding immediately.

   **Example:**

   ```json
   "postCreateCommand": "npm ci && npm run setup"
   ```

4. **Consistency Across Platforms:** Daytona’s approach ensures a consistent development experience across different operating systems, making it easier for teams to collaborate without worrying about environment discrepancies.

By incorporating Daytona’s tools into your workflow, you can achieve a more efficient and reliable containerized development process, enabling your team to focus on writing code rather than managing environments.

### Conclusion

Containerization is essential for modern development, ensuring your app runs consistently across different environments. It simplifies your workflow by isolating dependencies and configurations, making your development process smoother and more reliable.

VSCode, with its Remote - Containers extension, makes it easy to set up a containerized environment that mirrors production. This approach minimizes the "works on my machine" issue and streamlines development, testing, and deployment.

Daytona enhances this process by standardizing environments and automating setups, so your team can focus more on coding and less on environment management. By using tools like Daytona, you're embracing a more efficient and consistent way to develop, ultimately making your work easier and more productive.
---
