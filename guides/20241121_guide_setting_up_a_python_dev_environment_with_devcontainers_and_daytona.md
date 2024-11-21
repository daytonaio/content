---
title: "Setting Up a Python Dev Environment with DevContainers and Daytona"
description: "A step-by-step guide to setting up a Python dev environment with DevContainers and Daytona"
date: 2024-11-21
author: "Kiran Naragund"
tags: ["python", "devcontainers", "daytona"]
---

# Setting Up a Python Dev Environment with DevContainers and Daytona

## Introduction

In modern Python development, managing dependencies, Python versions, and conflicting libraries can often be cumbersome and time-consuming. Traditional tools like venv, virtualenv, and pipenv have helped manage these issues, but there's a better way to simplify and streamline your workflow: using DevContainers with Daytona.

This guide walks you through setting up a Python development environment using Daytona's containerized workspaces and the DevContainer. You'll learn how to skip the hassle of traditional environment managers and achieve consistency across team members, projects, and machines.

### TL;DR

- What is needed to get started in this hands-on learning
- Overviews of both DevContainer and Daytona
- Using Python project template
- Setup python project workspace in Daytona
- Conclusion

## Prerequisites
To follow this guide, you'll need to have the following:
- Basic understanding of[Python](definitions/20240820_defintion_python.md) and [Development Environment](definitions/20240819_definition_development environment.md)
- An IDE (like [VS Code](https://code.visualstudio.com/))
- Docker (download from [here](https://www.docker.com/))
- Daytona latest version [install from [here](https://www.daytona.io/docs/installation/installation/)]

**Note:** *[In this guide, Daytona v0.45.0 is used]*

## Overview of Daytona
Daytona is an open-source development environment manager that uses configuration files from a project's repository to build and provision workspaces. It simplifies the process of setting up consistent development environments across teams or for individual developers.

**Key Features of Daytona:**

- **Containerized Environments**: Keep your laptop clean by using clearly separated and containerized dev environments.
- **Portability**: Move your environments with you or host them on a remote server.
- **Consistency**: Ensure all team members work in identical environments, eliminating "it works on my machine" issues.
- **Easy Setup**: Create a fully configured development environment with a single command.
- **IDE Integration**: Seamlessly works with popular IDEs like VS Code and JetBrains products.
- **Git Provider Integration**: Easily connect with GitHub, GitLab, Bitbucket, and more for smooth workflow integration.
- **GPU Support**: Leverage GPU acceleration directly within your Daytona workspaces, ideal for machine learning and data science projects.

For more info about Daytona and it's features, check [here](https://daytona.io)

## Overview of DevContainers

DevContainers, short for Development Containers, are a way to configure portable and reproducible development environments using Docker containers. Dev containers are isolated, lightweight environments that allow developers to work inside a containerized version of a build environment. 

**Key Features of DevContainers:**

- **Pre-configured Build Environments**: Dev containers come with a base image that has all the software, tools, and dependencies pre-installed, so you can get started coding right away.
- **Isolated Environments**: Each dev container has its own isolated filesystem, networking, memory, and CPU, so there are no conflicts with other projects or software on your local machine.
- **Reproducible Builds**: Dev containers provide the exact same environment every time they're launched, ensuring consistent build results. No more "it works on my machine!" issues.
- **Less Setup Time**: Starting a new project with dev containers means you can skip the lengthy setup and configuration process. Just open your project in the container and everything is ready to go.
- **Flexibility**: You can choose a base image with the software and tools you want or build your own custom base image, meeting your specific needs.

For more info about DevContainers and it's features, check [here](https://containers.dev/)

## Step 1: Preparations

### Fork the Template Repository

For this guide we will be using this [pthon-project-template](https://github.com/pamelafox/python-project-template). 

This repository starts with a very simple `main.py` and a test for it at `tests/main_test.py`. Read the README file for better understanding of the file structure.

Click on the "Fork" button at the top right of the repository page to create a local copy under your GitHub account.

**Note:** *[The `.devcontainer/devcontainer.json` file content defines a configuration for a python development container environment.]*

By including a devcontainer.json file in your project repository, you can specify not just the Python version and dependencies, but also any required system packages, VS Code extensions, environment variables, and even custom scripts to run during setup.

## Step 2: Main Process

### Step 2.1: Start Daytona Server
Start the daytona server by running the command

```bash
daytona server
```
Your output should be similar to the screenshot below.
![Start Daytona Server](assets/setting_up_a_python_dev_environment_with_devcontainers_and_daytona_img1.png)

Choose "yes" and you should see a similar output in the screenshot below.
![Start Daytona Server](assets/setting_up_a_python_dev_environment_with_devcontainers_and_daytona_img2.png)

### Step 2.2: Add Git Provider

Daytona integrates with your preferred Git provider, streamlining your workflow by allowing direct access to repositories, and simplifying workspace creation from existing projects.

Execute the command provided below to add your git provider. Daytona also has support for other git providers like Bitbucker and Gitlab. You can learn more about Daytona Git Providers [here](https://www.daytona.io/docs/configuration/git-providers/)

```bash
daytona git-provider add
```

Your output should be similar to the image below
    
![image of github provider](assets/setting_up_a_python_dev_environment_with_devcontainers_and_daytona_img3.png)
    
Select GitHub and provide your personal access token.

![image of github provider](assets/setting_up_a_python_dev_environment_with_devcontainers_and_daytona_img4.png)

**Note:** *[Enable the required scopes while generating the token]*

### Step 2.3: Choose your preferred IDE
     
Run this command in terminal to choose your [IDE](https://www.daytona.io/docs/usage/ide/).
```bash
daytona ide
```
![preferred IDE](assets/setting_up_a_python_dev_environment_with_devcontainers_and_daytona_img5.png)	

### Step 2.4 Create a Daytona Workspace 
Now create a dev environment of the repository you created in GitHub(by forking) and follow the prompts after you run it.
```bash
daytona create
```
Choose Github as provider and select the python-project-template repository.

  #### Step 2.4.1 Provide workspace name
  The name of the workspace is usually the repository name if you didn't modify it when prompted in the creation of the workspace. In my case, it's `python-project-template`

  ![workspace name](assets/setting_up_a_python_dev_environment_with_devcontainers_and_daytona_img6.png)
  
  #### Step 2.4.2 Choose the target 
  Now it will ask you to choose the target, select `local` and enter.

  ![Choose the target ](assets/setting_up_a_python_dev_environment_with_devcontainers_and_daytona_img7.png)
  
Daytona will now start creating a workspace by pulling your project and install all required dependencies, once done it will open your project in your default IDE.

![Daytona workspace](assets/setting_up_a_python_dev_environment_with_devcontainers_and_daytona_img8.png)

![Daytona workspace](assets/setting_up_a_python_dev_environment_with_devcontainers_and_daytona_img9.png)

Now, your python dev environmentis ready to use.

### Step 3: Confirmation
Now, In your VS code run the test cases, you will see all the testcases passed. This means python dev environment has successfull set for your project.

![Daytona workspace](assets/setting_up_a_python_dev_environment_with_devcontainers_and_daytona_img10.png)

## Conclusion
By following this guide, you've set up a fully containerized Python development environment using Daytona and DevContainers. This setup ensures that your projects are reproducible, isolated, and consistent across machines, enabling smooth collaboration and effortless debugging.

## References

- [Python Project Template by Pamela Fox](https://github.com/pamelafox/python-project-template)

- [Daytona Documentation](https://www.daytona.io/dotfiles/the-ultimate-guide-to-managing-python-environments)


<!-- Note on Definitions -->
<!-- Throughout this guide, link relevant terms to their definitions using inline Markdown links. -->
<!-- Format: [term](/definitions/term.md) -->
<!-- If a definition doesn't exist, create it in the definitions directory and link to it. -->