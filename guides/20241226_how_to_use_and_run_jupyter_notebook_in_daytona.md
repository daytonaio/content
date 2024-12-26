---
title: "How to Use and Run Jupyter Notebook in Daytona."
description: "A brief description of what the guide covers. The description should be a maximum of 160 characters."
date: 2024-12-26
author: "Jeffrey Whewhetu"
tags: ["jupyter notebook", "data analysis", "python"]
---

# How to Use and Run Jupyter Notebook in Daytona

## Introduction

Jupyter Notebook is a very powerful and useful tool every data scientists, AI engineers, AI researchers and other professionals use in their work and personal projects. Knowledge about and how to use it's very necessary.

With the power of Daytona Dev Environment and Jupyter Notebook, our work can be as smooth and streamlined as possible.
In this comprehensive guide, we're going to deep dive into everything you need to get started with using Jupyter Notebook in a Daytona playground, hands-on experience with a real world practical project and much more.

### TL;DR

- What you need to follow along with the guide.
- What's Jupyter Notebook and Everything to Know to get Started
- Setting Up Daytona Playground for Jupyter Notebook
- Demo: Exploring the Jupyter Notebook UI
- Building a Jupyter Notebook Project in the Daytona Playground
- Common Issues and Troubleshooting
- Conclusion

## Prerequisites

## What's Jupyter Notebook and Everything to Know to Get Started

### Introduction

Jupyter Notebook is a powerful opensource interactive web-based application for interactive computing. It offers a simple, streamlined, document centric experience. It supports a wide range of programming languages such as Python, R and Julia.

### Features

### Usage

## Why use Daytona

## Setting Up Jupyter Notebook in Daytona

Alright, that's enough reading, now let us start writing codes. To do so you will need to set up a DuckDB [environment](20240819_definition_development%20environment.md) in a [Daytona workspace](20240819_definition_daytona%20workspace.md). Let’s begin.

### Step 1: Create a GitHub Repository

First head to the GitHub website and create a [repository](20240819_definition_repository.md) with the name of your choice. For my repository name, I’ll use `playground-jupyter-notebook`. The full URL path to the repository is `https://github.com/c0d33ngr/playground-jupyter-notebook`

### Step 2: Clone the repository using Git

After creating the repository, the next step is to clone the repository into your local PC or Mac. To clone the repository, open your terminal and run this command `git clone https://github.com/USERNAME/REPOSITORY-NAME` but replace the placeholders with your GitHub username and repository name you chose in step 1.

In my case, it’s `git clone https://github.com/c0d33ngr/playground-jupyter-notebook`

### Step 3: Prepare your `devcontainer.json` file and dataset in CSV format

Run the command to move into your cloned repository but don’t forget to replace `playground-jupyter-notebook` with the repository name you created if yours isn’t the same as mine.

```bash
cd playground-jupyter-notebook
```

Download the bank campaign dataset you are going to perform data tasks on which is in CSV format, from the GitHub repo [here](https://github.com/c0d33ngr/playground-duckdb/blob/main/bank_marketing.csv).

Note: It has to be in the directory of your clone repository. In my case, it's inside `playground-jupyter-notebook`.

Now, let us proceed to the next step.

Create a hidden directory named `.devcontainer` where our `devcontainer.json` file will be. Let’s do so and move into it.

Run the command to do so

```bash
mkdir .devcontainer && cd .devcontainer
```

Let’s create our devcontainer.json file in the `.devcontainer` directory.

I use `nano` to create my `.devcontainer.json` file using this command.

```bash
nano devcontainer.json
```

Paste this code into your `devcontainer.json` file.

```yaml
{
    "name": "Jupyter Notebook Playground",
    "image": "mcr.microsoft.com/devcontainers/base:ubuntu",
    "features": {
        "ghcr.io/devcontainers/features/python:1": {}
    },
    "postCreateCommand": "pip install notebook"
}
```

The `devcontainer.json` content contains configurations to start your Jupyter Notebook environment in a [Daytona workspace](20240819_definition_daytona%20workspace.md).

- `name`: This sets the name of the development container environment to `Jupyter Notebook Playground`.
- `image`: This uses a base Ubuntu image from the Microsoft image repository.
- `features`: This configuration adds Python setups in the Daytona workspace
- `postCreateComand`: This installs the Python packages needed for this guide into the workspace.

After creating and saving the `devcontainer.json` file, move up back to the root directory of your clone [repository](20240819_definition_repository.md). For me, I run the command below.

```bash
cd ../..
```

### Step 4: Commit and Push Changes to GitHub

Run these commands to push your changes to GitHub.

```bash
git add .
git commit -m “add devcontainer.json file”
git push
```

Now, you have successfully pushed our updated repository, which contains our configuration file (`devcontainer.json`) for our Jupyter Notebook environment.

### Step 5: Verify Daytona Installation

Run this command to check `daytona` is properly installed on your PC or Mac.

```bash
daytona –-version
```

You should see your version of `daytona` installed.

### Step 6: Create a Daytona Workspace with Jupyter Notebook Environment in it

Let’s start the daytona server by running the command.

```bash
daytona serve
```

You should see logs like my screenshot.

Open a new tab in your terminal, for Linux its `Shift + Ctrl + T`

Run the command below in a new tab of your terminal and follow the prompt instructions. It would ask you for a [workspace](20240819_definition_daytona%20workspace.md) name to use, choose the default.

Replace `USERNAME` and `REPOSITORY-NAME` with your username for GitHub and the repository name you created earlier.

```bash
daytona create https://github.com/USERNAME/REPOSITORY-NAME
```

In my case, it's this.

```bash
daytona create https://github.com/c0d33ngr/playground-jupyter-notebook
```

After you successfully run the above command you should see a screenshot like mine showing your Daytona workspace that contains the Jupyter Notebook environment is running.

You can now run this command to open the Jupyter Notebook [environment](20240819_definition_development%20environment.md) in your default [IDE](20240819_definition_integrated%20development%20environment%20_ide_.md) you choose when installing Daytona (Replace `WORKSPACE-NAME` with the name you used when creating the workspace above, in my case it's `playground-duckdb`).

```bash
daytona code WORKSPACE-NAME
```

That’s it. Daytona will create a Jupyter Notebook environment for you and open it in the default IDE you set.

## Demo: Exploring the Jupyter Notebook UI

## Building a Jupyter Notebook Project in the Daytona Playground

## Common Issues and Troubleshooting

*[List common problems and their solutions.]*

**Problem:** *[Description of the problem]*

**Solution:** *[Description of the solution]*

## Conclusion

*[Summarize what was accomplished by following the guide. Optionally, suggest further actions or related guides.]*

## References

*[Cite any sources or references used in the guide.]*

*[Add links to related guides or further reading that might interest the reader.]*

<!-- Note on Definitions -->
<!-- Throughout this guide, link relevant terms to their definitions using inline Markdown links. -->
<!-- Format: [term](/definitions/term.md) -->
<!-- If a definition doesn't exist, create it in the definitions directory and link to it. -->
