---
title: "CS50 DevBox: A Local Development Environment for CS50"
description: "How to set up a local development environment for CS50 using devcontainers as an alternative to Codespaces."
date: 2024-09-10
author: "Oreoluwa Ajayi"
tags: ["CS50", "devcontainer", "local development", "Docker", "VS Code"]
---

# CS50 DevBox: A Local Development Environment for CS50

## Introduction

The CS50 course, famous for its introduction to computer science and programming, requires specific tools such as `clang`, `make`, and `gdb`. Setting up a local environment for CS50 can be challenging due to platform-specific issues and dependency management. By using a devcontainer, we can streamline the setup process, ensuring all necessary tools are readily available in a consistent, isolated environment.

This guide will help you create a local development environment for CS50 using VS Code's devcontainer feature as an alternative to Codespaces.

### TL;DR

- **Use Docker and VS Code**: Set up a portable, isolated environment with devcontainers.
- **Automated Setup**: No need to install tools manually—everything is pre-configured.
- **Effortless Configuration**: Devcontainer simplifies handling dependencies like `clang`, `make`, and CS50 tools.

## Problems with Local Development Setup

Software Engineers often face issues when setting up a local environment for CS50, such as:

- **Dependency Conflicts**: Installing necessary tools can cause issues, especially on Windows.
- **Cross-Platform Inconsistencies**: Getting CS50 tools like `check50` and `submit50` to work can be challenging on different operating systems.
- **Time-Consuming Setup**: Installing compilers, debugging environments, and dependencies can slow down the learning process.

**Key Point:** By containerizing the development environment using a devcontainer, you can ensure consistent behavior across machines and avoid setup headaches.

## How to Create Your CS50 DevBox

### Step 1: Install Prerequisites

To begin, make sure you have the following installed on your machine:

- **[VS Code](https://code.visualstudio.com/)**: The IDE we'll use.
- **[Docker Desktop](https://www.docker.com/products/docker-desktop)**: To run the devcontainer.
- **[Remote - Containers Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)**: An extension for working with devcontainers in VS Code.

### Step 2: Set Up the Project Directory

1. **Create a project folder**:
   ```bash
   mkdir cs50-devbox
   cd cs50-devbox
   ```

2. **Initialize a Git repository**:
   ```bash
   git init
   ```

### Step 3: Create the `devcontainer.json` File

1. **Create a `.devcontainer` directory**:
   ```bash
   mkdir .devcontainer
   ```

2. **Create and edit `devcontainer.json`** in the `.devcontainer` directory:
   ```json
   {
     "name": "CS50 DevBox",
     "image": "ubuntu:latest",
     "customizations": {
       "vscode": {
         "extensions": [
           "ms-vscode.cpptools",
           "ms-python.python"
         ]
       }
     },
     "postCreateCommand": "sudo apt-get update && sudo apt-get install -y clang make gdb python3 python3-pip",
     "settings": {
       "terminal.integrated.defaultProfile.linux": "bash"
     }
   }
   ```

This configuration ensures:
- **Ubuntu base image** for consistency.
- **Automatic installation** of VS Code extensions for C++ and Python development.
- **Post-creation commands** to install essential tools: `clang`, `make`, `gdb`, and `python3`.

### Step 4: Add Sample Code

1. **Create a sample C program**:
   Create a file named `hello.c` in the root of the project with this code:

   ```c
   #include <stdio.h>

   int main(void) {
       printf("Hello, CS50!\n");
       return 0;
   }
   ```

2. **Create a sample Python script (optional)**:
   Create a file named `hello.py`:

   ```python
   print("Hello, CS50 in Python!")
   ```

### Step 5: Test the Setup

1. **Open the project in VS Code**:
   Open VS Code and navigate to the project folder. VS Code will prompt you to reopen the project in the container. Accept this prompt.

2. **Run the code**:
   - **For C code**: Open the integrated terminal and run:
     ```bash
     clang hello.c -o hello
     ./hello
     ```
   - **For Python code**: Run the Python script:
     ```bash
     python3 hello.py
     ```

---

## Conclusion

By following this guide, you have set up a **DevBox** for working on the CS50 course using devcontainers. This approach ensures that all necessary tools and dependencies are available in an isolated environment, making it easier to focus on coding without worrying about system configuration issues.

This setup can serve as a reliable alternative to Codespaces, allowing you to customize your own environment and share it with others.

---

## References

- [CS50 Documentation on Development Environment](https://cs50.readthedocs.io/cs50.dev/)
- [Docker Documentation](https://docs.docker.com/)
- [VS Code DevContainer Documentation](https://code.visualstudio.com/docs/remote/containers)

```