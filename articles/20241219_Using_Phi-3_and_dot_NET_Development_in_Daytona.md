---

**Title**: _Using Phi-3 and .NET Development in Daytona_  
**Description**: _Learn how to configure and run Phi-3 Labs samples in a Daytona environment using .NET and devcontainer.json._  
**Date**: _2024-12-24_  
**Author**: _Oreoluwa Ajayi_  
**Tags**: _["Phi-3 Labs", "Daytona", ".NET", "AI Development", "devcontainer"]_

---

## Using Phi-3 and .NET Development in Daytona: A Comprehensive Guide

### Introduction

With the release of Phi-3.5, Phi-3 Labs has introduced advanced features for AI and machine learning research. This guide walks you through how to configure and run Phi-3.5 Labs samples in a Daytona environment using .NET, ensuring a seamless development experience.

### TL;DR

- **Set up Daytona with .NET**: Configuring a Daytona environment with .NET
- **Integrate Phi-3.5 Labs**: Incorporate Phi-3.5 models into your development workflow.
- **Run and Test Samples**: Execute and test Phi-3.5 Labs samples within Daytona.
- **Best Practices**: Optimize your AI development workflow.

---

## Setting Up the Development Environment

### 1. Initialize the Project

Start by creating a new directory for your project:

```bash
# Create project directory
mkdir phi-3_devcontainer
cd phi-3_devcontainer
```

### 2. Create the Development Container

#### 2.1. Set Up the `.devcontainer` Directory

Create the `.devcontainer` folder in your project root:

```bash
mkdir .devcontainer
cd .devcontainer
```

#### 2.2. Configure `devcontainer.json`

In your `.devcontainer` folder, create a `devcontainer.json` file with the following content:

```json
{
  "name": "Daytona .NET Environment for Phi-3",
  "image": "mcr.microsoft.com/dotnet/sdk:9.0",
  "features": {
    "ghcr.io/devcontainers/features/docker-in-docker:1": {}
  },
  "customizations": {
    "vscode": {
      "extensions": [
        "ms-dotnettools.csharp",
        "ms-vscode.cpptools",
        "visualstudioexptteam.vscodeintellicode"
      ]
    }
  },
  "postCreateCommand": "dotnet restore Phi3Sample.csproj"
}
```

#### 2.3. Configure Dockerfile

In your `.devcontainer` folder,, create a `Dockerfile` with the following content to configure the development environment:

```dockerfile
# Use the ASP.NET 7.0 runtime as the base image
FROM mcr.microsoft.com/dotnet/aspnet:7.0

# Set the working directory
WORKDIR /app

# Copy the project file and restore dependencies
COPY Phi3Sample.csproj ./
RUN dotnet restore

# Copy the rest of the application files
COPY . ./

# Optional: Build the application
RUN dotnet build --configuration Release
```

### 3. Set Up `setup.sh`

Create a `setup.sh` file in the root of your project by running the command below on your terminal:

```bash
touch setup.sh
```

Add the following script to your file:

```bash
#!/bin/bash

# Ensure .NET dependencies are restored
dotnet restore Phi3Sample.csproj

# Add any other setup tasks here
echo "Setup completed successfully!"
```

### 4. Create the .NET Project

#### 4.1. Create `Phi3Sample.csproj`

In the root of your project, create the following `.NET` project file (`Phi3Sample.csproj`) by running the command on terminal:

```bash
touch Phi3Sample.csproj
```

Add this script to the new .NET project file:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net9.0</TargetFramework>
  </PropertyGroup>

</Project>
```

#### 4.2. Create `Phi3Sample.cs`

Create the ``Phi3Sample.cs` file in your project root by running the command below in your terminal:

```bash
touch Phi3Sample.cs
```

Add this script to test the environment setup:

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.WriteLine("Running Phi-3.5 Labs Sample");
    }
}
```

#### 4.3. Commit the Project to a GitHub Repository

Before launching the Daytona server, ensure your project is pushed to a GitHub repository. Follow these steps:

1. **Initialize a Git Repository**:

   ```bash
   git init
   git add .
   git commit -m "Initial commit for Phi-3 and .NET setup"
   ```

2. **Create a GitHub Repository**:

   - Log in to your GitHub account.
   - Create a new repository, for example, `Phi3-Daytona`.

3. **Add the Remote Repository**:

   ```bash
   git remote add origin https://github.com/<your-username>/Phi3-Daytona.git
   ```

4. **Push the Code**:

   ```bash
   git branch -M main
   git push -u origin main
   ```

### 5. Launch the Daytona Environment

Once you've committed your project files to your repository, follow these steps to launch the Daytona environment:

#### 5.1. Start the Daytona Server

```bash
daytona serve
```

#### 5.2. Create a New Daytona Workspace

```bash
daytona create your-repo-url
```

This will set up the Daytona workspace and ensure your container is ready to go. You can now run the .NET project with Phi-3.5 Labs samples inside the Daytona environment.

---

## Running and Testing the Sample

Once the Daytona environment is ready, navigate to your project folder and run the sample:

Thank you for the clarification. Based on the sequence you provided, here is the exact step-by-step process that was followed in your environment to run a .NET console application:

### 1. Verify .NET Version

Check the installed .NET version to ensure everything is up to date:

```bash
dotnet --version
```

### 2. Create a New Console Application

Generate a new .NET console application named `MyApp`:

```bash
dotnet new console -n MyApp
```

Ensure that you are in the `MyApp` directory on your terminal by running the command:

```bash
cd MyApp/
```

### 3. Restore Dependencies

Restore the project dependencies using:

```bash
dotnet restore
```

This will fetch and restore the necessary NuGet packages specified in the project.

### 4. Run the Application

Finally, run the application to see the output:

```bash
dotnet run
```

![Dotnet run](assets/20250109_final_dotnet_run.jpg)

## Best Practices

### 1. Resource Management

- Monitor memory usage when running models
- Optimize instance sizes in Daytona based on your workload
- Clean up unused resources regularly

### 2. Version Control

- Keep all code and models under version control
- Use branching for experimenting with different models and configurations
- Regularly commit changes to ensure team collaboration remains synchronized

### 3. Troubleshooting

#### 1. Model Loading Problems

- Ensure memory allocation is sufficient
- Verify the model path and download status

#### 2. Connectivity Issues

- If you encounter issues connecting to Daytona’s reverse proxy, check firewall or VPN configurations. Ensure that the following IP addresses are whitelisted:
  - `35.198.165.62` (Europe-based reverse proxy)
  - `34.133.75.4` (US-based reverse proxy)

---

## References

- [Daytona Documentation](https://daytona.io/docs)
- [.NET Installation Guide](https://learn.microsoft.com/en-us/dotnet/?WT.mc_id=dotnet-35129-website)
- [Microsoft Phi-3.5-mini-guide](https://huggingface.co/microsoft/Phi-3.5-mini-instruct)

---

## Conclusion

This guide walks through setting up a Phi-3 and .NET environment in Daytona, allowing you to run and test Phi-3.5 Labs samples with ease. By using Daytona’s cloud-based workspace management, you can enhance collaboration, streamline workflows, and ensure consistent environments across teams.

```

```
