---
title: "Running Omni Engineer in Daytona: A Step-by-Step Guide for AI Engineers"
description: "Learn to run Omni Engineer in Daytona, create a devcontainer.json, and contribute to repositories with this comprehensive guide."
date: 2024-08-21
author: "Dheeraj Singh"
tags: ["Omni Engineer", "Daytona", "Devcontainer", "Docker"]
---


# Running Omni Engineer in Daytona: A Step-by-Step Guide for AI Engineers

In this guide, we'll demonstrate how to run Omni Engineer inside Daytona and effectively use it. We'll also walk through creating a `devcontainer.json` file, contributing it to existing repositories, and making a pull request to the Groq repository. By the end, you'll know how to set up a development environment that streamlines your AI engineering workflows.

## Prerequisites

- Basic understanding of Docker and VS Code.
- Familiarity with Git and GitHub.
- Access to the Omni Engineer and Claude Engineer repositories.

## Step 1: Setting Up Your Development Environment

### 1.1. Install VS Code and Docker

Ensure you have [Visual Studio Code (VS Code)](https://code.visualstudio.com/) and [Docker](https://www.docker.com/products/docker-desktop) installed on your machine. These tools are essential for creating and managing development containers.

### 1.2. Install the Remote - Containers Extension

Install the "Remote - Containers" extension for VS Code from the Extensions Marketplace. This will allow you to open and work inside Docker containers.

## Step 2: Creating the `devcontainer.json` File

### 2.1. Create a New Directory for Your Dev Container Configuration

Open a terminal and navigate to the root directory of your local clone of the Omni Engineer repository:

```bash
git clone https://github.com/Doriandarko/omni-engineer.git
cd omni-engineer
```

Create a .devcontainer directory and navigate into it:

```bash
mkdir .devcontainer
cd .devcontainer
```
### 2.2. Create the devcontainer.json File
Inside the .devcontainer directory, create a file named devcontainer.json with the following content:

```json
{
  "name": "Omni Engineer Dev Container",
  "dockerFile": "Dockerfile",
  "extensions": [
    "ms-python.python",
    "ms-vscode.cpptools",
    "esbenp.prettier-vscode",
    "github.copilot"
  ],
  "settings": {
    "python.pythonPath": "/usr/local/bin/python"
  },
  "runArgs": [
    "--gpus",
    "all"
  ],
  "postCreateCommand": "pip install -r requirements.txt",
  "remoteUser": "vscode"
}
```
### 2.3. Create a Dockerfile
In the same .devcontainer directory, create a file named Dockerfile with the following content:

```bash
# Use an official Python runtime as a parent image
FROM python:3.9-slim

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Set the working directory
WORKDIR /workspace

# Install dependencies
COPY requirements.txt /workspace/
RUN pip install --no-cache-dir -r requirements.txt

# Install additional system packages
RUN apt-get update && apt-get install -y \
    build-essential \
    curl \
    git \
    && rm -rf /var/lib/apt/lists/*

# Copy the rest of the application code
COPY . /workspace/
```

## Step 3: Contributing devcontainer.json to the Repositories

### 3.1. Fork and Clone the Repositories
If you haven't already, fork the [Omni Engineer repository](https://github.com/Doriandarko/omni-engineer) and [Claude Engineer repository](https://github.com/Doriandarko/claude-engineer) to your GitHub account. Clone the repositories to your local machine:

```bash
git clone https://github.com/YOUR_USERNAME/omni-engineer.git
cd omni-engineer
```

### 3.2. Add the .devcontainer Directory
Copy the .devcontainer directory created earlier into the root of both repositories.

### 3.3. Commit and Push Changes
Add the changes to the staging area, commit them, and push them to your forked repository:

```bash
git add .devcontainer
git commit -m "Add devcontainer configuration"
git push origin main
```

### 3.4. Create a Pull Request
Go to your forked repository on GitHub and create a pull request (PR) from your fork's main branch to the original repository's main branch. Describe the changes and submit the PR.

## Step 4: Creating a Pull Request for the Groq Repository


### 4.1. Fork and Clone the Groq Repository
Fork the Groq repository and clone it to your local machine:
```bash
git clone https://github.com/YOUR_USERNAME/groq.git
cd groq
```

### 4.2. Add the .devcontainer Directory
Copy the .devcontainer directory from your Omni Engineer setup into this repository.

### 4.3. Commit and Push Changes

Add, commit, and push the changes:
```bash
git add .devcontainer
git commit -m "Add devcontainer configuration"
git push origin main

```
### 4.4. Create a Pull Request
Go to your forked Groq repository on GitHub and create a PR to merge the changes into the original repository.

## Step 5: Using Omni Engineer Inside Daytona
### 5.1. Open the Dev Container
In VS Code, open the Omni Engineer repository. Click on the green "><" icon in the bottom-left corner of the window and select "Reopen in Container."

### 5.2. Access and Use Omni Engineer
Once inside the dev container, you can access and use Omni Engineer. For example, if you're working on an AI model, you might want to run the following command to start the Omni Engineer service:

```bash
omni-engineer --start
```

You can now develop and test your AI models within this environment.

## Conclusion
You've successfully set up a development container for Omni Engineer, contributed it to the repositories, and created a pull request for the Groq repository. With these steps, you can streamline your AI engineering workflows and ensure a consistent development environment.
