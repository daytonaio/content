---
title: "A Beginner's Guide to Developing Inside Containers with VSCode"
description: "Step-by-step guide on setting up a development environment inside a container using VSCode. Learn the basics of containerization, common pitfalls, and how Daytona does it."
author: "Johnnie Oduro Jnr."
date: "2024-08-20"
tags: ["Containerization", "VSCode", "Development Environment", "Docker", "Daytona"] 
---

## TL;DR

Containerization allows you to package your application and its dependencies into a single, portable unit that runs consistently across different environments. This guide shows you how to set up a development environment inside a container using VSCode. It covers the basics of containerization, how to avoid common pitfalls, and how Daytona optimizes their containerized workflows.

---

## A Beginner's Guide to Developing Inside Containers with VSCode

### Introduction

Containerization has revolutionized the way developers build, ship, and run applications. If you're new to the concept, the idea of working inside a container might sound intimidating. However, with tools like Visual Studio Code (VSCode), setting up and developing inside containers has never been easier. This guide will walk you through the basics of containerization, how to set up a development environment inside a container using VSCode, common pitfalls to avoid, and how the Daytona team does it.

### What is Containerization?

Before diving into the setup, let's cover some basic concepts:

**Containerization** is a lightweight form of virtualization that allows you to package an application and its dependencies into a single, portable unit called a container. Containers can run consistently across different environments, from your local machine to production servers. Read more about [containerizatoin here](https://www.daytona.io/definitions/c/containerization).

**Benefits of Containerization:**
1. **Consistency:** Containers ensure that your application behaves the same way in every environment, reducing the "it works on my machine" problem.
2. **Isolation:** Each container runs in its own isolated environment, preventing conflicts between different applications or services.
3. **Portability:** Containers can be easily moved between different environments, making deployment simpler and more reliable.

### Setting Up Your Development Environment in a Container with VSCode

Now that you understand the basics, let's get hands-on with setting up a development environment inside a container using VSCode. Follow these steps:

#### Step 1: Install Docker

[Docker](https://www.daytona.io/definitions/d/docker) is the platform that allows you to create and manage containers. Start by installing Docker on your machine:

- **For Windows:** Download Docker Desktop from the [official website](https://www.docker.com/products/docker-desktop) and follow the installation instructions.
- **For macOS:** Download Docker Desktop from the [official website](https://www.docker.com/products/docker-desktop) and follow the installation instructions.
- **For Linux:** Follow the [official Docker documentation](https://docs.docker.com/engine/install/) for your distribution.

Ensure Docker is running by opening a terminal and typing:

```bash
docker --version
```

You should see the Docker version information.

**Example:**

```bash
Docker version 20.10.7, build f0df350
```

#### Step 2: Install VSCode

If you haven't already, install Visual Studio Code from the [official website](https://code.visualstudio.com/). VSCode is a powerful, lightweight code editor with an extensive ecosystem of extensions.

#### Step 3: Install the Remote - Containers Extension

To develop inside containers, you'll need to install the "Remote - Containers" extension in VSCode. This extension allows you to open any folder inside a container, leveraging Docker to provide a consistent development environment.

- Open VSCode.
- Go to the Extensions view by clicking on the Extensions icon in the Activity Bar or by pressing `Ctrl+Shift+X`.
- Search for "Remote - Containers" and click "Install."

**Example:**

![Remote - Containers Extension](https://code.visualstudio.com/assets/docs/remote/containers/remote-containers-extension.png)

#### Step 4: Create a Dev Container Configuration

With the extension installed, you're ready to set up your containerized development environment.

1. **Open your project in VSCode:** Open the folder or repository you want to develop inside a container.
2. **Create a `.devcontainer` folder:** In the root of your project, create a new folder named `.devcontainer`.
3. **Add a `devcontainer.json` file:** Inside the `.devcontainer` folder, create a file named `devcontainer.json`. This file defines the configuration for your dev container.

Here’s a basic example for a Node.js project:

```json
{
  "name": "My Dev Container",
  "image": "node:14", // Use a Node.js 14 image as the base
  "extensions": [
    "dbaeumer.vscode-eslint" // Install ESLint extension inside the container
  ],
  "settings": {
    "terminal.integrated.shell.linux": "/bin/bash"
  },
  "postCreateCommand": "npm install", // Run npm install after the container is created
  "forwardPorts": [3000], // Forward port 3000 from the container to your local machine
  "remoteUser": "node" // Use the 'node' user inside the container
}
```

**Special Instructions:**

- **Choosing the Right Base Image:** The `"image": "node:14"` line specifies the base image for your development environment. If you're working with Python, for example, you might use `"image": "python:3.9"` instead. Be sure to choose an image that matches your project's requirements.

- **Custom Dockerfile:** If you need more control over the environment, you can create a `Dockerfile` in the `.devcontainer` folder instead of using an existing image. Reference it in your `devcontainer.json` like this:

  ```json
  {
    "name": "My Dev Container",
    "build": {
      "dockerfile": "Dockerfile"
    },
    ...
  }
  ```

**Example Dockerfile for a Python Project:**

```Dockerfile
# Use an official Python runtime as a parent image
FROM python:3.9-slim

# Set the working directory in the container
WORKDIR /usr/src/app

# Copy the current directory contents into the container at /usr/src/app
COPY . .

# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Run app.py when the container launches
CMD ["python", "app.py"]
```

4. **Reopen in Container:** Once the `devcontainer.json` file is set up, VSCode will prompt you to reopen the folder inside the container. Click "Reopen in Container" to start the process. VSCode will build the container, install the specified extensions, and set up your development environment.

**Example of Reopening in Container:**

![Reopen in Container](https://code.visualstudio.com/assets/docs/remote/containers/reopen-in-container.png)

#### Step 5: Develop as Usual

After your container is up and running, you can develop just as you would on your local machine. The main difference is that your code is running inside a container, which ensures consistency across different environments.

**Example:**

Let's say you're working on a Node.js project. After setting up the container, you might run your application using:

```bash
npm start
```

VSCode will handle the port forwarding, allowing you to view your application in the browser at `http://localhost:3000`.

### Common Pitfalls and How to Avoid Them

Working with containers introduces a few potential pitfalls. Here’s how to avoid them:

1. **Large Image Sizes:** Some base images can be quite large, leading to slow build times. To avoid this, choose lightweight images (like Alpine-based images) when possible.

   **Example:**

   Instead of using `node:14`, you can use `node:14-alpine` to reduce the image size:

   ```json
   "image": "node:14-alpine"
   ```

2. **File Permissions:** Containers run with their own user and group settings, which might cause file permission issues. Set the `remoteUser` in your `devcontainer.json` to align with your container's user configuration.

   **Special Instruction:**

   If you're running into file permission issues, double-check the user your container is running as. You can use the `remoteUser` setting in `devcontainer.json` to specify a user that matches the permissions you need.

   ```json
   "remoteUser": "root"
   ```

   However, be cautious when using `root`, as it can introduce security risks.

3. **Dependency Management:** Ensure that your `devcontainer.json` is well-documented and maintained. This will make it easier for others (or yourself) to understand and modify the container setup later.

   **Example:**

   Include comments in your `devcontainer.json` file to explain why certain settings or commands are used:

   ```json
   {
     "name": "My Dev Container",
     "image": "node:14",
     "extensions": [
       // ESLint helps in identifying and fixing common JavaScript issues
       "dbaeumer.vscode-eslint"
     ],
     ...
   }
   ```

4. **Performance Issues:** Containers can sometimes be slower than developing directly on your host machine, especially if you're working with heavy applications or large codebases. Consider optimizing your container setup by minimizing the number of layers in your Dockerfile or using bind mounts wisely.

   **Example:**

   If you notice slow performance, review your Dockerfile and consider merging RUN commands to reduce the number of layers:

   **Before:**

   ```Docker

file
   RUN apt-get update
   RUN apt-get install -y git
   ```

   **After:**

   ```Dockerfile
   RUN apt-get update && apt-get install -y git
   ```

### How Daytona Does It

At Daytona, developing inside containers using VSCode’s Remote - Containers extension has been a game-changer for our workflow. Here’s how we do it:

1. **Standardized Environments:** We use a `devcontainer.json` in every project to define the development environment. This ensures that all developers are working in the same environment, regardless of their local machine setup.

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

2. **Custom Docker Images:** We create custom Docker images tailored to our project’s needs, including all necessary tools, libraries, and configurations. This helps us avoid "works on my machine" scenarios.

   **Special Instruction:**

   To create a custom Docker image, start with a base image, install your project's dependencies, and then push it to a container registry (like Docker Hub or a private registry).

   **Example:**

   ```Dockerfile
   FROM node:14

   WORKDIR /usr/src/app

   COPY package*.json ./

   RUN npm ci

   COPY . .

   CMD ["npm", "start"]
   ```

   Build and push the image:

   ```bash
   docker build -t daytona/base-image:latest .
   docker push daytona/base-image:latest
   ```

3. **Automated Setup:** Our `devcontainer.json` files are designed to automate as much of the setup process as possible. For instance, we use the `postCreateCommand` to install dependencies automatically, ensuring that developers can start coding immediately after the container is built.

   **Example:**

   ```json
   "postCreateCommand": "npm ci && npm run setup"
   ```

   This command not only installs dependencies but also runs a setup script that configures the environment according to project-specific needs.

4. **Consistent Development Experience:** By using VSCode’s Remote - Containers extension, we ensure that our development experience is consistent across different platforms, making it easier for new developers to onboard and start contributing to projects.

### Conclusion

Developing inside containers with VSCode is a powerful way to ensure consistency and portability in your development workflow. By following the steps outlined in this guide, you can set up a containerized development environment that suits your needs, avoid common pitfalls, and take inspiration from how Daytona does it to streamline your process. Happy coding!

---

This article should provide a comprehensive, beginner-friendly guide to developing inside containers with VSCode, complete with examples and special instructions to help new developers avoid common issues.