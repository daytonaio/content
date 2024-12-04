---
title: 'How to Create a Devcontainer Feature'
description:
  'A step-by-step guide to creating and enhancing a devcontainer feature,
  focusing on the Hugging Face environment for ML and NLP tasks.'
date: 2024-08-20
author: 'Vamshi Maskuri'
---

# How to Create a Devcontainer Feature

# Introduction

Development Container Features (Devcontainer Features) are essential for
standardizing development environments across various teams and projects. They
allow developers to easily share and reuse environment setups, ensuring
consistency and reducing the time spent configuring environments. Devcontainer
features can be customized to meet the specific needs of a project, making them
highly versatile and effective for various development scenarios.

In this guide, we will walk you through creating a Devcontainer feature, using
Hugging Face as an example. Hugging Face is a leading library for machine
learning (ML) and natural language processing (NLP) tasks, making it an
excellent choice for demonstrating how to create a feature that can be widely
beneficial. By the end of this guide, you will have developed a fully functional
Devcontainer feature that can be seamlessly integrated into any development
workflow.

## Why Create a Devcontainer Feature?

Devcontainer is essential for teams that need to ensure a consistent development
environment. They allow developers to easily add specific tools, libraries, or
configurations to their development environments, ensuring consistency across
different projects and teams. This is particularly useful in complex projects
involving ML and NLP, where setting up environments can be time-consuming and
error-prone.

Using Hugging Face as an example highlights the importance of having a
pre-configured environment tailored for ML and NLP tasks. This feature can save
developers time and reduce the potential for setup errors, enabling them to
focus more on development and less on configuration.

Development Container Features are self-contained, shareable units of
installation code and development container configuration. By using Devcontainer
features, teams can share these optimized environments, ensuring that all
members have access to a consistent and reliable setup that is tailored to the
specific needs of the project.

## Prerequisites

To follow along with this guide, you should have a basic understanding
of[Python](definitions\20240820_defintion_python.md),
[shell scripting](definitions\20240820_definition_shell_scripting.md) and
[containerization](definitions/20240819_definition_containerization.md).

You will also need the following tools installed:
[Docker](https://www.docker.com/),
[Visual Studio Code](https://code.visualstudio.com/), and the
[Remote - Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers).

- **Docker**: Used for containerizing applications, ensuring consistency across
  different environments.
- **Visual Studio Code**: An Integrated Development Environment (IDE) that
  supports Devcontainer development.
- **Remote - Containers Extension**: A VS Code extension that allows you to open
  any folder inside a container and take advantage of Visual Studio Code’s full
  feature set.
- **Dev Container CLI**: A command-line tool used for working with Devcontainer
  features, enabling you to test and manage your Devcontainer setups.

### Installing the Dev Container CLI

To install the Dev Container CLI, you can use npm:

```bash
npm install -g @devcontainers/cli
```

This command installs the CLI globally, making it available for use in testing
and managing Devcontainer features throughout this guide.

## TL;DR

This guide helps you:

- **Create a Devcontainer Feature**: Start by forking and cloning a starter
  repository.
- **Set Up Your Feature**: Define metadata in `devcontainer-feature.json` and
  implement the feature installation script.
- **Test and Publish**: Validate your feature locally and then publish it using
  GitHub Actions.

## Step 1: Preparations

### Fork the Starter Repository

To create your custom Devcontainer feature, start by forking the
[feature-starter repository](https://github.com/devcontainers/feature-starter)
on GitHub. This repository provides a solid foundation for building new
Devcontainer features.

- **Step 1.1**: Fork the Repository

Click on the "Fork" button at the top right of the repository page to create a
local copy under your GitHub account.

- **Step 1.2**: Clone this repository:

Once forked, clone the repository to your local machine using the following
commands:

```bash
git clone https://github.com/your-username/feature-starter.git
cd feature-starter
```

- **Step 1.3**: Open the project in VS Code:

```bash
code .
```

- **Step 1.4**: When prompted, click "Reopen in Container" to develop inside a
  container with the necessary tools installed.

**Note:** _[Ensure your development environment is set up with Docker, Visual
Studio Code and the Remote - Containers extension]_

## Step 2: Main Process

### Create a New Feature Directory

Inside the `src` directory of your forked repository, create a new folder named
`huggingface`. This folder will contain all the necessary configuration files
and scripts for the Hugging Face feature.

```bash
mkdir -p src/huggingface
```

### Configure `devcontainer-feature.json`

The `devcontainer-feature.json` file defines the metadata and options for the
Hugging face feature. Below is an example configuration:

```json
{
  "name": "Hugging Face",
  "id": "huggingface",
  "version": "1.0.3",
  "description": "Installs Hugging Face libraries and tools for NLP and ML tasks.",
  "options": {
    "version": {
      "type": "string",
      "proposals": ["latest", "4.28.1", "4.27.4", "4.26.0"],
      "default": "latest",
      "description": "Select the version of Hugging Face Transformers to install."
    },
    "cuda": {
      "type": "boolean",
      "default": false,
      "description": "Enable this option to install the CUDA-enabled version of PyTorch for GPU support."
    },
    "datasets_version": {
      "type": "string",
      "proposals": ["latest", "1.14.0", "1.13.3"],
      "default": "latest",
      "description": "Select the version of Hugging Face Datasets to install."
    },
    "tokenizers_version": {
      "type": "string",
      "proposals": ["latest", "0.11.6", "0.11.5"],
      "default": "latest",
      "description": "Select the version of Tokenizers to install."
    }
  },
  "installsAfter": ["ghcr.io/devcontainers/features/common-utils"]
}
```

**Note:** _[Ensure that descriptions are clear and informative, making it easy
for users to understand what each option does. This step is crucial for
providing a seamless user experience]_

### Implement `install.sh`

The `install.sh` script is the core of the feature’s installation process. Below
is an optimized version of the script that incorporates modular functions and
error handling.

```bash
#!/bin/bash
set -e

echo "Activating feature 'huggingface'"

# Function to install Python packages
install_python_package() {
    local package_name=$1
    local package_version=$2
    if [ "$package_version" = "latest" ]; then
        pip install $package_name
    else
        pip install "$package_name==$package_version"
    fi
}

# Ensure Python and pip are available
if ! command -v python3 &> /dev/null; then
    apt-get update && apt-get install -y python3 python3-pip python3-venv
else
    echo "Python3 is already installed."
fi

# Set up a virtual environment if not present
VENV_PATH="/opt/huggingface-venv"
if [ ! -d "$VENV_PATH" ]; then
    python3 -m venv $VENV_PATH
    echo "Virtual environment created at $VENV_PATH."
else
    echo "Using existing virtual environment at $VENV_PATH."
fi

# Activate the virtual environment
source $VENV_PATH/bin/activate

# Upgrade pip to the latest version
pip install --upgrade pip

# Install required Python packages
install_python_package "transformers" "$VERSION"

# Install PyTorch with or without CUDA support
if [ "$CUDA" = "true" ]; then
    pip install torch torchvision torchaudio
else
    pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cpu
fi

install_python_package "datasets" "$DATASETS_VERSION"
install_python_package "tokenizers" "$TOKENIZERS_VERSION"
pip install sentencepiece huggingface_hub

# Create a script to activate the virtual environment
cat <<EOL > /usr/local/bin/activate-huggingface
#!/bin/bash
source $VENV_PATH/bin/activate
EOL
chmod +x /usr/local/bin/activate-huggingface

echo "Hugging Face setup completed successfully."
```

**Note:** _[The script allows users to customize their installation through the
provided options, making the feature flexible for various use cases]_

## Step 3: Confirmation

After implementing the feature, confirm that everything works as expected by
testing the feature locally. For testing use GitHub Actions to automatically
test the feature.

### Adding a Basic Test Script

To ensure that the feature installs the correct versions of the Hugging Face
libraries, create a basic test script. This test will validate the installation
by checking the versions of the installed packages.

Create a new directory named `test` inside the feature root directory:

```bash
mkdir -p src/huggingface/test
cd test
```

Inside this directory, create a test script `version_check.sh`:

```bash
#!/bin/bash
set -e

check_version() {
    local package_name=$1
    local expected_version=$2
    local installed_version=$(python -c "import $package_name; print($package_name.__version__)")

    if [ "$installed_version" == "$expected_version" ]; then
        echo "$package_name version is correct: $installed_version"
    else
        echo "$package_name version is incorrect: $installed_version (expected: $expected_version)"
        exit 1
    fi
}

# Example checks
check_version "transformers" "$VERSION"
check_version "torch" "$TORCH_VERSION"
```

This script will ensure that the versions of `transformers`, `torch`, and any
other critical packages match the expected versions.

### Integrate the Test Script into the Devcontainer

In the `devcontainer-feature.json` file, which you have configured earlier in
Step 2, add the following `postCreateCommand` at the end of the file to run the
test automatically after the container is created:

```json
"postCreateCommand": "bash /workspaces/src/huggingface/test/version_check.sh"
```

This configuration will automatically run the version_check.sh script after the
Devcontainer is created, ensuring that all installations are correct and
up-to-date.

### Running the Test

You can also test locally using the Dev Container CLI:

```bash
devcontainer features test -f huggingface -i mcr.microsoft.com/devcontainers/base:ubuntu .
```

Ensure all installations are completed successfully and that the Hugging Face
environment is functional.

## Step 4: Automated Testing

To automate testing whenever changes are pushed to your repository, set up
GitHub Actions. Automated tests help catch issues early in the development
process, ensuring that your feature remains reliable as it evolves.

**Note:** _[Never skip the testing phase; it ensures reliability and
functionality. Testing not only validates your code but also builds confidence
in the stability of the feature]_

## Step:5 Publish the Feature

Once you have completed the feature and tested it, publish it to your
repository. This makes the feature to publish it using GitHub Actions. This
process will make your feature available for others to use and contribute to.

### Push Changes to GitHub

Use the following commands to push the developed feature into your local
repository.

```bash
git add .
git commit -m "Add Hugging Face devcontainer feature"
git push origin main
```

### Run the Workflow

1. Navigate to the `Actions` tab in your GitHub repository.

2. Run the `Release dev container features & Generate Documentation` workflow.
   This workflow will package your feature and update the documentation
   automatically

## Set Visibility

Ensure that the package visibility is set to public in the repository's
`Packages` settings. This step is essential for making your feature accessible
to the community.

## Examples of Great Devcontainer Features

To inspire your work, here are a few examples of highly effective Devcontainer
features:

1. **[Github CLI](https://github.com/devcontainers/features/src/kubectl-helm-minikube):**
   A feature that sets up the GitHub CLI in Devcontainer, making it easy to
   manage GitHub repositories from within your containerized environment.

2. **[Kubectl-Helm-Minikube](https://github.com/devcontainers/features/src/kubectl-helm-minikube):**
   This feature installs the latest version of kubectl, Helm, and optionally
   minikube. Auto-detects latest versions and installs needed dependencies.

3. **[Docker-in-Docker](https://github.com/devcontainers/features/tree/main/src/docker-in-docker):**
   This feature enables Docker to run inside a container, allowing you to test
   Dockerized applications from within your Devcontainer.

4. **[Node.js](https://github.com/devcontainers/features/tree/main/src/node):**
   A feature that installs Node.js along with npm or Yarn, enabling JavaScript
   and TypeScript development in a consistent environment.

5. **[Python](https://github.com/devcontainers/features/tree/main/src/python):**
   Sets up Python with popular tools like pip, Poetry, and venv, ensuring a
   reliable Python environment for development.

For more features available refer [here](https://containers.dev/features)

## Conclusion

In this guide, we have walked through the essential steps to create a
Devcontainer feature, focusing on setting up a Hugging Face environment and
emphasizing the importance of automating and simplifying the setup process for
complex tools used in ML and NLP. From forking the starter repository to
implementing the `install.sh` script, we have covered how to define metadata,
configure options, and test the feature locally. These steps ensure that your
feature is both robust and flexible, meeting the needs of various development
scenarios.

One of the key takeaways from this guide is the importance of customization and
testing. By providing users with configurable options, such as selecting
specific versions of libraries or enabling CUDA support, you are making the
feature adaptable to different project requirements. Moreover, testing your
feature both locally and through automated CI pipelines ensures reliability and
helps catch potential issues early, contributing to a smoother development
experience for your users.

As you move forward, remember that Devcontainer features are a powerful tool for
standardizing development environments across teams. By creating your own
features, you can streamline the setup process, reduce the chances of
misconfiguration, and ultimately increase productivity. Now that you have the
knowledge and tools, consider contributing back to the community by sharing your
features, or explore the many existing features available
[here](https://containers.dev/features) to enhance your own development
workflow.

You can find the complete implementation of the Hugging Face Devcontainer
feature in the
[Hugging Face Devcontainer Feature Repository](https://github.com/nkkko/features/tree/main/src/huggingface).
This repository includes all the scripts and configurations discussed in this
guide, allowing you to easily clone and adapt the feature for your own projects.

## References

- [Dev Container Features Documentation](https://containers.dev/overview)
- [Microsoft Devcontainer Features Marketplace](https://containers.dev/features)
- [GitHub Feature Starter Repository](https://github.com/devcontainers/feature-starter)
- [Devcontainer JSON Schema](https://github.com/devcontainers/spec/blob/main/schemas/devContainerFeature.schema.json)
