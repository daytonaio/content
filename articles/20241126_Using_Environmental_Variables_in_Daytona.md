---
title: "Using Environmental Variables in Daytona"
description: "Learn how to set, manage, and use environmental variables in Daytona workspaces with a simple Python project for demonstration."
date: 2024-11-26
author: "Busayo Samuel"
tags: ["Environment Variables", "Development Environment", "Daytona Workspaces"]
---

# Using Environmental Variables in Daytona

## Introduction

[Environmental variables]('/definitions/20241126_definition_environment_variables.md') are important for configuring development environments, storing sensitive information, and managing application settings. Daytona provides a straightforward method to set and manage environmental variables across different workspaces using the `daytona env` command.

### TL;DR

- **What**: Learn to use `daytona env set` for managing workspace environmental variables

- **Why**: Simplify configuration and securely manage development environment settings

- **How**:
  - Set variables using `daytona env set key=value`
  - Create a workspace with `daytona create --code`
  - Verify variables with `daytona env list`

## Prerequisites

- Daytona installed on your system
- Docker
- Visual Studio Code (VSCode)

## Set Environmental Variables

Before adding an environment variable to Daytona, ensure the both Docker and your server is running. Start your server using:

```bash
daytona server
```

Then use the `daytona env set` command to define environmental variables:

```bash
daytona env set USERNAME=JohnDoe PASSWORD=123456
```

This command allows you to set multiple environmental variables in a single operation.

### How `daytona env set` Works

The command stores environmental variables at the workspace level. The variables are persistent across multiple workspace and are accessible to all containers and development tools within the workspace. This provides a secure way to manage configuration without modifying project files.

You can verify that the environmental variables have been saved by running:

```bash
daytona env list
```

You should see output similar to the image below:

![Screenshot example of Daytona env variable list](assets/20241126_Using_Environmental_Variables_in_Daytona_1.png)

## Create a New Workspace

You can create and open a new workspace using Daytona's create command with the `--code` flag:

```bash
daytona create --code
```

When prompted, choose to enter a GitHub URL. For this tutorial, let's use a simple Python project with a DevContainer configuration. Enter this URL in the input space: `https://github.com/bellatrick/python_starter.git`

The command will clone the repository, set up the development environment and open Visual Studio Code.

### Using Environmental Variables in Your Project

In your development enviroment, create a Python script to demonstrate accessing environmental variables:

`env_demo.py`:
```python
import os

def main():
    # Access environmental variables
    username = os.environ.get('USERNAME')
    password = os.environ.get('PASSWORD')

    if username and password:
        print(f"Logged in as: {username}")
        # Note: In a real application, never print passwords!
    else:
        print("Environmental variables not found")

if __name__ == "__main__":
    main()
```
Run the script using:

```bash
python env-demo.py
```

Your output should look like this:

![Result of running python script](assets/20241126_Using_Environmental_Variables_in_Daytona_2.png)

### Best Practices

1. **Security**:
   - Avoid storing sensitive information like passwords directly in environmental variables
   - Use secure secret management tools for production credentials
   - Consider using environment-specific configurations

2. **Naming Conventions**:
   - Use clear, descriptive variable names
   - Follow your team's or project's naming standards
   - Use uppercase for global constants

### Troubleshooting

- Ensure Daytona is up to date
- Verify the environmental variables using `daytona env list`

## Conclusion

The `daytona env` command provides a simple and powerful method for managing environmental variables in your development workflow. Understanding how to set, list, and use these variables, developers can create more flexible and configurable development environments.

## References

- [Daytona Official Documentation](https://www.daytona.io/docs/)
- [Daytona CLI](https://www.daytona.io/docs/tools/cli/#daytona-env)
- [DevContainer Specification](https://containers.dev/)
