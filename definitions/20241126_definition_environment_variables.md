---
title: "Environment Variable"
description: "A dynamic-named value that can affect the way running processes will behave on a computer"
---

# Environment Variable

## Definition

An environment variable is a dynamic-named value stored in the operating system's memory that provides configuration information to running processes, applications, and system programs. These variables consist of a name and an associated value, which can be accessed by programs to modify their behavior, configure settings, or store runtime information.

## Context and Usage

Environment variables serve multiple critical purposes in computer systems and software development:

1. **Configuration Management**
   - Provide runtime configuration for applications
   - Store sensitive information like API keys or database credentials
   - Enable flexible software deployment across different environments

2. **System and Application Behavior**
   - Modify program execution paths
   - Set language and locale preferences
   - Define system-wide or user-specific settings

3. **Development and Deployment**
   - Support different configurations for development, testing, and production environments
   - Allow containerized applications to receive runtime parameters
   - Enable secure and flexible software deployment strategies

**Common Examples**:
- `PATH`: Specifies directories where executable programs are located
- `HOME`: Indicates the current user's home directory
- `LANG`: Sets the default language and localization settings
- `DATABASE_URL`: Stores database connection information in web applications