---
title: "How to Create a Devcontainer Feature"
description: "A step-by-step guide to creating and enhancing a devcontainer feature, focusing on the Hugging Face environment for ML and NLP tasks."
date: 2024-08-20
author: "Vamshi Maskuri"
---

# How to Create a Devcontainer Feature

## Introduction

Devcontainer features are essential for standardizing development environments across various teams and projects. They allow developers to easily share and reuse environment setups, ensuring consistency and reducing the time spent on configuring environments. In this guide, we will walk you through the process of creating a Devcontainer feature, using Hugging Face as an example. Hugging Face is a leading library for machine learning (ML) and natural language processing (NLP) tasks, making it an excellent choice for demonstrating how to create a feature that can be widely beneficial. By the end of this guide, you will have developed a fully functional and Devcontainer feature that can be seamlessly integrated into any development workflow.

## Why Create a Devcontainer Feature?

Creating a Devcontainer feature is essential for teams that need to ensure a consistent development environment across different projects. It allows developers to quickly spin up environments that are pre-configured with the necessary tools and dependencies. This is particularly useful in complex projects involving ML and NLP, where setting up environments can be time-consuming and error-prone.

Using Hugging Face as an example highlights the importance of having a pre-configured environment tailored for ML and NLP tasks. This feature can save developers time and reduce the potential for setup errors, enabling them to focus more on development and less on configuration.

### Prerequisites

o follow along with this guide, you should have a basic understanding of[Python](definitions\20240820_defintion_python.md), [shell scripting](definitions\20240820_definition_shell_scripting.md) and [containerization](definitions/20240819_definition_containerization.md).

You will also need the following tools installed: [Docker](https://www.docker.com/),  [Visual Studio Code](https://code.visualstudio.com/), and the [Remote - Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers).

- **Docker**: Used for containerizing applications, ensuring consistency across different environments.
- **Visual Studio Code**: An Integrated Development Environment (IDE) that supports Devcontainer development.
- **Remote - Containers Extension**: A VS Code extension that allows you to open any folder inside a container and take advantage of Visual Studio Code’s full feature set.

### TL;DR

- **Clone and Prepare**: Fork and clone the feature-starter repository.
- **Create Feature Directory**: Set up the `huggingface` directory within the `src` folder.
- **Configure and Implement**: Define metadata in `devcontainer-feature.json` and implement the feature installation script.
- **Test and Publish**: Test the feature locally and publish it using GitHub Actions.

## Step 1: Preparations

### Fork the Starter Repository

To create your custom Devcontainer feature, start by forking the [feature-starter repository](https://github.com/devcontainers/feature-starter) on GitHub. This repository provides a solid foundation for building new Devcontainer features.

- **Step 1.1**: Fork the Repository

Click on the "Fork" button at the top right of the repository page to create a local copy under your GitHub account.

- **Step 1.2**: Clone this repository:

Once forked, clone the repository to your local machine using the following commands:

```bash
git clone https://github.com/your-username/feature-starter.git
cd feature-starter
```

- **Step 1.3**: Open the project in VS Code:

```bash
code .
```

- **Step 1.4**: When prompted, click "Reopen in Container" to develop inside a container with the necessary tools installed.

**Note:** _[Ensure your development environment is set up with Docker, Visual Studio Code and the Remote - Containers extension]_

## Step 2: Main Process

### Create a New Feature Directory

Inside the `src` directory of your forked repository, create a new folder named `huggingface`. This folder will contain all the necessary configuration files and scripts for the Hugging Face feature.

```bash
mkdir -p src/huggingface
```

### Configure `devcontainer-feature.json`

The `devcontainer-feature.json` file defines the metadata and options for the Hugging face feature. For a detailed guide on devcontainer-feature json file see the [Create Devcontainer JSON File Guide](https://www.daytona.io/dotfiles/guide-create-devcontainer-json-file).
Below is an example configuration:

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

**Note:** _[Ensure that descriptions are clear and informative, making it easy for users to understand what each option does. This step is crucial for providing a seamless user experience]_

### Implement `install.sh`

The `install.sh` script is the core of the feature’s installation process. Below is an optimized version of the script that incorporates modular functions and error handling.

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

**Note:** _[The script allows users to customize their installation through the provided options, making the feature flexible for various use cases]_

## Step 3: Confirmation

After implementing the feature, confirm that everything works as expected by testing the feature locally. For testing use GitHub Actions to automatically test the feature. You can also test locally using the Dev Container CLI:

```bash
devcontainer features test -f huggingface -i mcr.microsoft.com/devcontainers/base:ubuntu .
```

Ensure all installations are completed successfully and that the Hugging Face environment is functional.

## Step 4: Automated Testing

To automate testing whenever changes are pushed to your repository, set up GitHub Actions. Automated tests help catch issues early in the development process, ensuring that your feature remains reliable as it evolves.

**Note:** _[Never skip the testing phase; it ensures reliability and functionality. Testing not only validates your code but also builds confidence in the stability of the feature]_

## Step:5 Publish the Feature

Once you have completed the feature and tested it, publish it to your repository. This makes the feature to publish it using GitHub Actions. This process will make your feature available for others to use and contribute to.

### Push Changes to GitHub

Use the following commands to push the developed feature into your local repository.

```bash
git add .
git commit -m "Add Hugging Face devcontainer feature"
git push origin main
```

### Run the Workflow

1. Navigate to the `Actions` tab in your GitHub repository.

2. Run the `Release dev container features & Generate Documentation` workflow. This workflow will package your feature and update the documentation automatically

## Set Visibility

Ensure that the package visibility is set to public in the repository's `Packages` settings. This step is essential for making your feature accessible to the community.

**Note:** _[Documentation is key. Ensure that all steps and options are well-documented for users. Clear documentation will guide users through the setup process and help them troubleshoot any issues]_

## Common Issues and Troubleshooting

**Problem:** _[Installation of dependencies fails due to network issues]_

**Solution:** _[Ensure your network connection is stable and consider using a proxy if necessary]_

**Problem:** _[Python is not recognized as a command]_

**Solution:** _[Make sure Python is installed and accessible in your system's `PATH`]_

**Problem:** _[CUDA is not available after installation.]_

**Solution:** _[Verify that your GPU supports CUDA and that the correct drivers are installed.]_

## Examples of Great Devcontainer Features

To inspire your work, here are a few examples of highly effective Devcontainer features:

1. **[Github CLI](https://github.com/devcontainers/features/src/kubectl-helm-minikube):** A feature that sets up the GitHub CLI in Devcontainer, making it easy to manage GitHub repositories from within your containerized environment.

2. **[Kubectl-Helm-Minikube](https://github.com/devcontainers/features/src/kubectl-helm-minikube):** This feature installs latest version of kubectl, Helm, and optionally minikube. Auto-detects latest versions and installs needed dependencies.

3. **[Docker-in-Docker](https://github.com/devcontainers/features/tree/main/src/docker-in-docker):** This feature enables Docker to run inside a container, allowing you to test Dockerized applications from within your Devcontainer.

4. **[Node.js](https://github.com/devcontainers/features/tree/main/src/node):** A feature that installs Node.js along with npm or Yarn, enabling JavaScript and TypeScript development in a consistent environment.

5. **[Python](https://github.com/devcontainers/features/tree/main/src/python):** Sets up Python with popular tools like pip, Poetry, and venv, ensuring a reliable Python environment for development.

For more features available refer [here](https://containers.dev/features)

## Conclusion

By following this guide, you've successfully created and improved a `devcontainer` feature for setting up a Hugging Face environment. This feature is now ready for use in any development container, providing a consistent environment for ML and NLP tasks.

## References

- [Dev Container Features Documentation](https://containers.dev/overview)
- [Microsoft Devcontainer Features Marketplace](https://containers.dev/features)
- [GitHub Feature Starter Repository](https://github.com/devcontainers/feature-starter)
- [Devcontainer JSON Schema](https://github.com/devcontainers/spec/blob/main/schemas/devContainerFeature.schema.json)
