---
title: "Streamlining Data Science Workflows with Cookiecutter and Daytona"
description: "Learn how to enhance your data science projects using Cookiecutter templates and Daytona's devcontainer features."
date: 2024-09-10
author: "Busayo Samuel"
tags: ["Datascience", "devcontainer", "cookiecutter"]
---

# Streamlining Data Science Workflows with Cookiecutter and Daytona

## Introduction

Have you ever felt like you're spending more time setting up projects than actually coding and analyzing data? You're not alone. Tools like [Cookiecutter Data Science](https://cookiecutter-data-science.drivendata.org/) and Daytona were created so that you don't have to create projects from scratch and reinvent the wheel each time you want to jump into a new project.

Cookiecutter gives you a solid starting point for your data science projects. Daytona, on the other hand, ensures everyone on your team is working with the same tools and setup, no matter where they are. The [Dev Container feature](/definitions/20240910_definition_dev_container_feature.md) supported by Daytona makes sure your models work the same way in testing as they do in the real world, especially when you are working with a team. Essentially, these tools will make your life easier when it comes to deploying and scaling data science projects.

### TL;DR

- **Standardized Project Structure**: Cookiecutter Data Science provides a flexible template to organize data science projects.

- **Reproducible Environments**: By using Cookiecutter with Daytona’s devcontainer feature, you can create consistent and reproducible development environments.

- **Improved Workflow**: Combining Cookiecutter and Daytona automates the setup of project structures and environments. This allows data scientists to spend more time on analysis and modeling.

- **Enhanced Collaboration**: Standardized templates and reproducible environments help data scientists, machine learning engineers, and DevOps professionals work better together and share knowledge more effectively.

### Prerequisites

Before starting this tutorial, you need to have the following:

- A basic understanding of command-line interfaces
- Familiarity with Git and version control concepts

Along with Python, the following need to also be installed:

- **Visual Studio Code**: An free source-code editor developed by Microsoft.
- **Docker**: An open-source platform that enables developers to build, deploy, run, update, and manage applications in containers.
- **Remote - Containers**: An extension for Visual Studio Code allows developers to use a Docker container as a full-featured development environment,

### Installation Guide:

1. Download and install VS Code from the [official website](https://code.visualstudio.com/)

2. Install Docker:

    - For Windows and Mac: Download Docker Desktop [here](https://www.docker.com/products/docker-desktop)
    - For Linux: Follow [this installation instructions](https://docs.docker.com/engine/install/) for your specific distribution.

3. Install the Remote - Containers extension in VS Code:

    - Open VS Code
    - Go to the Extensions view (Ctrl+Shift+X)
    - Search for "Remote - Containers"
    - Click "Install"

4. Download and install Git [here](https://git-scm.com/downloads)

5. Install the [latest version of python](https://www.python.org/downloads/) from their website.

Now that you have the necessary tools installed, let's proceed with the step-by-step guide to add a Dev Container to your project.

## What are Dev Container Features?

Dev container features are pre-built, shareable components that can be easily added to your development container. They allow you to modularize and customize your dev container setup, making it easier to add tools, runtimes, or libraries to your environment.

Benefits of using dev container features include:
- Simplified configuration
- Improved consistency across team environments
- Easier maintenance and updates
- Flexibility to mix and match tools as needed

## Step-by-Step Guide to Adding Dev Container Features

### Step 1: Set Up Your Basic Dev Container

1. Create a `.devcontainer` folder in your project root.
2. Inside this folder, create a `devcontainer.json` file.

Here's a basic structure:

```json
{
    "name": "Python Data Science",
    "dockerFile": "Dockerfile",
    "settings": {
        "python.defaultInterpreterPath": "/usr/local/bin/python"
    }
}
```

### Step 2: Identify Needed Features

Consider what tools and libraries you need for your data science project. Common needs might include:
- Python
- Jupyter Notebooks
- Data manipulation libraries (Pandas, NumPy)
- Version control (Git)
- Code quality tools (Black, Flake8)

### Step 3: Add Features to Your devcontainer.json

To add features, include a `features` object in your `devcontainer.json`:

```json
{
    "name": "Python Data Science",
    "dockerFile": "Dockerfile",
    "image": "mcr.microsoft.com/devcontainers/python:3.12-bookworm",
    "features": {
        "ghcr.io/devcontainers/features/python:1": {},
    },
    "settings": {
        "python.defaultInterpreterPath": "/usr/local/bin/python"
    }
}
```

### Step 4: Add VS Code Extensions

While not strictly part of dev container features, adding relevant VS Code extensions enhances your development experience:

```json
"extensions": [
    "ms-python.python",
    "ms-python.vscode-pylance"
]
```

### Step 5: Configure Settings

Adjust VS Code settings to match your preferences:

```json
"settings": {
    "python.defaultInterpreterPath": "/usr/local/bin/python",
    "python.linting.enabled": true,
    "python.linting.pylintEnabled": true
}
```

### Step 6: Add Post-Create Commands

If you need to run commands after the container is created (e.g., installing additional packages), use `postCreateCommand`:

```json
"postCreateCommand": "pip install -r requirements.txt"
```

Your `devcontainer.json` file should look like this:

```json
{
    "name": "Python Data Science",
    "image": "mcr.microsoft.com/devcontainers/python:3.12-bookworm",
    "features": {
        "ghcr.io/devcontainers/features/python:1":  {},

    },
  "customizations": {
    "vscode": {
        "settings": {
            "python.defaultInterpreterPath": "/usr/local/bin/python",
            "python.linting.enabled": true,
            "python.linting.pylintEnabled": true
        },
        "extensions": [
            "ms-python.python",
             "ms-python.vscode-pylance"
        ]
    }
  },

    "postCreateCommand": "pip install -r requirements.txt"
}
```

### Step 7: Create a requirements file

At the root of your project, create a `requirements.txt` file. List any additional packages you want to include in your project (e.g., Flask) by adding the package names to the file. These packages will automatically be installed via the `postCreateCommand`.

### Step 8: Rebuild and Test

After making changes:
- Press F1 or Ctrl+Shift+P.
- Type and select Remote-Containers: Reopen in Container.
- Alternatively, click the blue button at the bottom-left corner of VS Code and select Reopen in Container from the modal.

VS Code will then build the container based on the configuration in your `devcontainer.json` file and open your project inside the container. This process might take a few minutes the first time, as it needs to download and set up the container environment.

Once the container is running, you can start coding and running your application within this isolated environment.

You can find other lists of useful dev container featurers [here](https://containers.dev/features)

## Using Cookiecutter Data Science Feature in Daytona

Combining Cookiecutter Data Science with Daytona's dev container features creates a powerful synergy for data science workflows. This integration allows you to leverage the standardized project structure of Cookiecutter Data Science within the reproducible environment provided by Daytona's dev containers.

By using this feature, you'll be able to:

- Quickly set up a standardized data science project structure
- Ensure all team members are working with the same tools and dependencies
- Seamlessly switch between projects without worrying about conflicting environments

### Getting started

To use this feature in your Daytona cloud development environment, follow these steps:

- Install Daytona. You can follow these [installation steps](https://www.daytona.io/docs/installation/installation/) to install daytona for you operating system.

- After you have successfully installed Daytona, start a new server and create a new Daytona workspace.

```bash
daytona server
```

```bash
daytona create --code
```
The command above creates a new Daytona workspace and opens the workspace in VSCode.
When prompted to either enter a **custom Repository URL** or **Create from sample**, select the latter. Then select Python from the options of sample workspaces.

- Navigate to the `.devcontainer/devcontainer.json` file and edit the file by adding a new feature.

```json
  "features": {
    "ghcr.io/bellatrick/feature-starter/cookiecutter:latest": {}
  }
```
The feature in the json file will install Cookiecutter Datascience into your workspace along with required packages.

- Commit this file to your repository.

- Open the Command Palette (F1 or Ctrl+Shift+P). Type and select **Remote-Containers: Rebuild Container**.

- Once the workspace is rebuilt, you can now use the `ccds` command to create a new data science project structure.

```bash
ccds
```

This will prompt you for project details and create a new data science project structure based on the cookiecutter-data-science template.

Note: If the `ccds` command is not recognized, try running `source /usr/local/bin/activate-cookiecutter-ds` first to activate the environment then run `ccds` again.

## Step 3: Confirmation

To confirm that you've successfully set up your Daytona workspace with Cookiecutter Data Science, follow these steps:

- In your workspace, run the `ccds` command. You should be prompted to enter project details.
- After entering the details, check that a new directory has been created with the project name you specified.
- Navigate into the new directory and verify that it contains the standard Cookiecutter Data Science project structure, including folders like data, models, and notebooks.
- Try running a Python script or Jupyter notebook within the new project structure to ensure that all necessary libraries are installed and functioning correctly.

If you can complete these steps without errors, you've successfully set up your Daytona workspace with Cookiecutter Data Science!

## Common Issues and Troubleshooting

**Unable to run daytona code**: If you are using WSL2, you might run into issues while trying to run the command, `daytona code`.

**Solution:**: Follow the instructions in [this Github issue](https://github.com/daytonaio/daytona/issues/282).

## Conclusion

By integrating Cookiecutter Data Science templates with Daytona's devcontainer features, you've set up a powerful, reproducible environment for your data science projects. As your projects grow or as you onboard new team members, this setup makes it easy to maintain best practices and consistent workflows.

Moving forward, consider exploring more advanced features of both Cookiecutter and Daytona. You might want to customize the Cookiecutter template to better fit your specific needs or explore additional devcontainer features to further enhance your development environment.

Remember, the goal is to spend less time on setup and more time on solving data science problems. With this workflow in place, you're well-equipped to do just that. Happy coding!

## References

The code for the dev container feature is available on [Github](https://github.com/bellatrick/feature-starter). You should also check out these resources:

- [Cookiecutter Data Science](https://cookiecutter-data-science.drivendata.org/#with-pip)
- [Daytona Documentation](https://www.daytona.io/docs/)
- [VS Code Remote - Containers](https://code.visualstudio.com/docs/devcontainers/containers)
- [Dev Containers Features](https://containers.dev/features)
