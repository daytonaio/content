---
title: "Title of the Guide. The title should be a max. of 55 characters."
description: "A brief description of what the guide covers. The description should be a maximum of 160 characters."
date: 2024-09-20
author: "Jeffrey Whewhetu"
tags: ["DuckDB", "OLAP", "daytona", "Python"]
---

# How to Set Up DuckDB Playground Environment in Daytona Workspace

# Introduction

# TL;DR

- What you need to follow along with the guide.
- What's DuckDB and Why use it
- Set up a Daytona Workspace with DuckDB environment
- Hands-on practice using DuckDB as a CLI Tool
- Hands-on practice using DuckDB client API with Python
- Summary

# Prerequisites

To follow along with hands-on guide about DuckDB Playground in Daytona, you'll need to have the following;

- An IDE(It could be VS Code, or JetBrains) or just a terminal.
- Docker installation on your PC or Mac. Click here for more info
- Daytona installation on your PC or Mac. Click here for more info
- A GitHub account to create a repository. Link here to create one, if you don’t have
- Basic knowledge of Git and GitHub

# What's DuckDB and Why use it

## DuckDB

DuckDB is a fast in-process data analytical database with support of feature-rich SQL dialect complemented with deep integrations into client APIs. It's designed to provide high performance on complex queries against large databases in embedded configuration, such as combining tables with hundreds of columns and billions of rows. It's specialised for online analytical processing (OLAP) workloads

## Features of it

DuckDB has lots of features that make it stand out among other databases which focus on OLAP. Some of the features are:

- **Simple:** It's very simple to install and perform embedded in-process operation.
- **Portable:** Since it has no external dependencies, it's extremely portable and can be compiled for all major operating systems and CPU architectures.
- **Feature-Rich:** DuckDB has some interesting features such as extensive support for SQL complex queries, integrations to languages like Python, R and Java and data can be stored as persistent, single-file databases.
- **Speed:** it's faster as it uses columnar-vectorized query execution engine which improves performance to run OLAP workloads.
- **Free:** Lastly, it's a free open source database system which anyone can use because of its permissive MIT License.

# Setting up Daytona Workspace for DuckDB Playground

Alright that's enough reading, now let us get started to writing codes. To do so we’ll need to set up a DuckDB environment in a Daytona workspace. Let’s begin.

## Step 1: Create a Github Repository

First head to GitHub website and create a repository with the name of your choice. For my repository name, I’ll use `playground-duckdb`. The full URL path to the repository is `<https://github.com/c0d33ngr/playground-duckdb`>

## Step 2: Move in to the Cloned repository

After creating the repository, the next step is to clone the repository into your local PC or Mac. To clone the repository, open your terminal and run this command `git clone <https://github.com/USERNAME/REPOSITORY-NAME`> but replace the placeholders with your github name and repository name you chose in step 1.

In my case, it’s `git clone <https://github.com/c0d33ngr/playground-duckdb>

## Step 3: Create your devcontainer.json file

The next step to take after cloning the repository is to move into the repository so we can create our `devcontainer.json` file.

Run the command to move into your cloned repository but don’t forget to replace `playground-duckdb` to your own repository name you created if yours isn’t same with mine.

```bash

cd playground-duckdb

```

Next, we’ll create a hidden directory named `.devcontainer` where our `devcontainer.json` file will be. Let’s do so and move into it

Run command in the same terminal

```bash

mkdir .devcontainer && cd .devcontainer

```

Let’s create our devcontainer.json file while in the `.devcontainer` directory.

I use `nano` to create my own `.devcontainer.json` file using this command but you can use any GUI or other terminal text editor if you prefer.

```bash

nano devcontainer.json

```

Paste this code into your `devcontainer.json` file

```yaml

{

"name": "DuckDB Playground",

"image": "mcr.microsoft.com/devcontainers/base:ubuntu",

"features": {

"ghcr.io/eitsupi/devcontainer-features/duckdb-cli:1": {}

}

}

```

The `devcontainer.json` content contains configurations to start your DuckDB environment in a Daytona workspace.

- `name`: This sets the name of the development container environment to `DuckDB Playground`.
- `image`: This uses a base Ubuntu image from Microsoft image repository.
- `features`: This configuration add DuckDB installation setup in Daytona workspace

After created and saved the `devcontainer.json` file, move up back to the root directory of your clone repository. For me, I run the command below

```bash

cd ../..

```

## Step 4: Commit and Push Changes to GitHub

Run this commands to push your changes to GitHub

```bash

git add .

git commit -m “add devcontainer.json file”

git push

```

Now, we have successfully push our updated repository that contains our configuration file (`devcontainer.json`) for our DuckDB environment

## Step 5: Verify Daytona Installation

Run this command to check `daytona` is properly installed in your PC or Mac

```bash

daytona –version

```

You should see your version of `daytona` installed

## Step 6: Create a Daytona Workspace with DuckDB Playground Environment in it

Let’s start daytona server by running the command

```bash

daytona serve

```

You should see logs like my screenshot

Open a new tab in your terminal, for Linux is `Shift + Ctrl + T`

Run this command in the new tab of your terminal

```bash

daytona create <https://github.com/c0d33ngr/playground-duckdb> –code

```

That’s it. Daytona will create a DuckDB playground environment for you and open it in your default IDE you set.

# Using DuckDB as a Command Line Interface (CLI) Tool

# Using DuckDB with Python through it's Client API

# Conclusion

# References

- [DuckDB Documentation](https://duckdb.org/docs/)
- [Daytona Documentation](https://daytona.io/docs)
- [DuckDB Tricks](https://duckdb.org/2024/08/19/duckdb-tricks-part-1.html)
- [DuckDB CLI Data Processing](https://duckdb.org/2024/06/20/cli-data-processing-using-duckdb-as-a-unix-tool.html)
- [DuckDB Python Examples](https://github.com/duckdb/duckdb/blob/main/examples/python/duckdb-python.py)
