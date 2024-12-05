---
title: 'Building a Link Shortener with FastHTML and Dub.co'
description:
  'Learn how to build a link shortener using FastHTML lightweight framework and Dub.co robust link management API.'
date: 2024-12-05
author: 'Author Name'
tags: ['Daytona', 'FastHTML', 'Dub.co', 'Link Shortener']
---

# Building a Link Shortener with FastHTML and Dub.co

# Introduction

Development environments play a crucial role in software development. Developers need developments environments to experiment with new ideas and debug them without impacting existing products. When working on web applications, the ability to rapidly prototype, isolate dependencies, and seamlessly integrate APIs can significantly enhance productivity.

This guide focuses on **Daytona**, a powerful tool for managing development environments. Daytona provides isolated, containerized workspaces that ensure consistency, reduce setup overhead, and simplify team collaboration. By leveraging Daytona, developers can streamline their workflows, avoid common configuration issues, and focus on building impactful solutions.

In this tutorial, you'll learn how to set up a robust link shortener using **FastHTML**, a Python library for server-rendered applications, and the **Dub.co API**, a service for creating and managing shortened links. You’ll gain hands-on experience in:

- Configuring a Daytona workspace.
- Building a landing page with FastHTML.
- Integrating external APIs.
- Deploying the finished application to a production environment.

Before diving in, make sure you have the following:

Before diving in, make sure you have the following:

- **[Daytona](https://docs.daytona.dev/getting-started)** installed: Follow the official documentation to set up Daytona for managing your development environments.
- **[Docker](https://docs.docker.com/get-docker/)** running: Install Docker to enable containerized workspaces.
- **[Python 3.10](https://www.python.org/downloads/)** or later: Download and install the latest compatible version of Python.
- An **Integrated Development Environment (IDE)**: Use an IDE to write, debug, and manage your code efficiently. Examples include **[VS Code](https://code.visualstudio.com/)**, **PyCharm**, or **Atom**.
- **[GitHub](https://github.com/)** account: Use GitHub to manage your project's version control and collaborate effectively.
- Basic familiarity with **[Python](https://docs.python.org/3/tutorial/)** and **[web development concepts](https://developer.mozilla.org/en-US/docs/Learn)** (helpful but not strictly required).

Let's get started!

---

## TL;DR

### 1. Daytona Setup
Learn how to configure a Daytona workspace for isolated and efficient development.

### 2. FastHTML Integration
Build a clean and responsive landing page using FastHTML with server-rendered output.

### 3. Dub.co API Integration
Incorporate external API calls to generate and manage shortened links.

### 4. Deployment
Deploy the final application to a production-ready environment, such as **Render**.

---

With this guide, you'll have a working link shortener in no time while mastering the tools to create efficient, collaborative development workflows.

## Overview of Daytona
Daytona is a powerful development environment manager that streamlines the process of creating, managing, and sharing isolated workspaces. Built on containerization technology, Daytona eliminates the "it works on my machine" problem, ensuring consistency across development environments. It is particularly useful for collaborative teams and individual developers who want to focus on coding rather than dealing with setup complexities. Daytona integrates seamlessly with Docker to provide efficient, lightweight workspaces that are easy to set up and share.

**Key Features**:
- **Dependency Isolation**: Ensures that each workspace has its own set of dependencies, avoiding conflicts.
- **Quick Startup**: Launch ready-to-use environments in seconds.
- **Collaboration**: Share reproducible environments across teams with ease.
- **Integration**: Works seamlessly with Docker and other container-based tools.
- **Flexibility**: Suitable for prototyping, debugging, and production environments.

Learn more: [Daytona Documentation](https://docs.daytona.dev/)

---

## Overview of FastHTML
FastHTML is a Python-based lightweight framework for building server-rendered web applications. It focuses on delivering clean and responsive HTML with minimal overhead, making it ideal for small to medium-sized projects. FastHTML allows developers to utilize Python's robust ecosystem while simplifying the creation of web pages. Its templating engine and server-side rendering capabilities ensure fast page load times and improved SEO, making it a great choice for developers seeking speed and simplicity.

**Why Choose FastHTML?**:
- **Minimalistic Design**: Reduces complexity, focusing on speed and efficiency.
- **Server-Side Rendering (SSR)**: Delivers pre-rendered HTML for better performance and SEO.
- **Clean Templating System**: Makes creating dynamic, responsive pages intuitive.
- **Python Ecosystem**: Integrates smoothly with Python libraries and frameworks.
- **Fast Prototyping**: Perfect for quickly building and deploying MVPs.

Explore FastHTML: [FastHTML GitHub Repository](https://github.com/example/fasthtml)

---

## Overview of Dub.co
Dub.co is a robust link management platform that allows developers and businesses to create, manage, and track shortened URLs. It provides a powerful API for seamless integration, enabling developers to add advanced link management functionality to their applications. Dub.co supports custom branding, analytics, and scalability, making it a top choice for marketing campaigns, content sharing, and app integrations.

**Core Features**:
- **Link Creation**: Easily generate shortened, branded URLs.
- **Analytics**: Track link performance with insights into clicks, geographic data, and device types.
- **Custom Branding**: Add personalized domains or custom slugs for professional link sharing.
- **Scalability**: Handles high traffic and integrates with large-scale applications.
- **API Access**: Integrate with external tools and workflows effortlessly.

**Use Cases**:
- Marketing campaigns to measure user engagement.
- Building link shorteners with custom branding.
- Managing links in applications and content delivery.

Check out Dub.co: [Dub.co API Documentation](https://www.dub.co/api)

#  Setting up Daytona development environment
To set up your Daytona development environment and integrate it with your IDE (such as VSCode, IntelliJ, or Cursor) and Git providers (including Bitbucket and GitHub), follow these steps:

**Step 1: Create a GitHub Repository**: 
   Start by creating a GitHub repository for your project. This repository will be used to create your Daytona workspace.

**Step 2: Start the Daytona Server**: 
   Open your terminal and run the following command to start the Daytona server and Docker desktop:
   ```bash
   daytona serve
   ```
   ![Terminal after starting Daytona serve](path/to/your/image1.png)

**Step 3: Set the Target to Local Docker Provider**: 
   Once the server is running, set up a target to your local Docker provider by executing:
   ```bash
   daytona target set
   ```
   ![Terminal after setting target](path/to/your/image2.png)

**Step 4: Add Git Provider**: 
   Next, set up your Git provider using the command:
   ```bash
   daytona git-providers add
   ```
   Select your preferred Git provider from the options presented. 
   ![Terminal after adding git provider](path/to/your/image3.png)

**Step 5: Set Up IDE for Development**: 
   Use the following command to set up your IDE for development:
   ```bash
   daytona ide
   ```
   Choose any IDE you prefer, such as Visual Studio Code or IntelliJ. 
   ![Terminal after setting up IDE](path/to/your/image4.png)

**Step 6: Create a Workspace**: 
   Finally, create a workspace using your GitHub repository URL with the command:
   ```bash
   daytona create <github_url>
   ```
   ![Terminal after creating workspace](path/to/your/image5.png)


The workspace will be opened in your ide using SSH from daytona. You can start experimenting in your development environment

# Setting Up the Project

In this section, we will install the necessary dependencies for our project and set up the environment variables required for integration with the Dub.co API. We will also create a main entry point for our application.

## Step 1: Install Dependencies
To begin, we need to install the required Python packages. Open your terminal and run the following command:

```
pip install python-fasthtml dub python-dotenv
```
## Step 1: Create a .env File and Add the Environmental Variable
1. Create a file named `.env`.
2. Add the following line to the file, replacing `your_api_key_here` with your actual API key:
   ```
   DUB_API_KEY=your_api_key_here
   ```


# Building the Link Shortener

In this section, we will guide you through the process of building a link shortener using FastHTML and Dub.co. This will involve setting up the project structure, implementing the main application logic, and explaining each step in detail.

## Step 1: Create the Application Structure

Organize your project as follows:
fasthtml-link-shortener/
├── main.py          # Application logic
├── .env             # API key

## Step 2: Implement main.py

The following code implements the main application logic for the link shortener. It begins by importing necessary modules and loading environment variables.

```python
from fasthtml.common import *
import dub
from dotenv import load_dotenv
import os

# Load environment variables
load_dotenv()

# Initialize Dub with the API key from the environment variables
d = dub.Dub(token=os.getenv('DUB_API_KEY'))

# Initialize the FastHTML app
app, rt = fast_app()

@rt("/")
def index():
    # This function defines the home page of the application, which includes a form to input URLs for shortening.
    return Titled(
        "AI Link Shortener",
        Article(
            Form(method="post", action="/shorten")(
                Label("Enter URL: ", Input(name="url", type="url", required=True)),
                Button("Shorten", type="submit")
            ),
            Div(id="result")
        )
    )

@rt("/shorten")
async def shorten(url: str):
    # This function handles the shortening of URLs. It attempts to shorten the URL using Dub.co and returns the result.
    try:
        response = d.links.create(request={"url": url})
        short_link = response.short_link
    except Exception as e:
        short_link = f"Error: {e}"

    # This returns the result of the shortening process, including the original URL, the shortened URL, and a link to shorten another URL.
    return Titled(
        "Shortened Link",
        Article(
            P(f"Original URL: {url}"),
            P(f"Shortened URL: ", A(href=short_link)(short_link)),
            A(href="/")("Shorten another link")
        )
    )

# This starts the FastHTML application server.
serve()
```

## Step 3: Testing Application
To run the project, use the following command in your terminal:
```bash
python main.py
```
If you are using Python 3, use the following command instead:
```bash
python3 main.py
```
Once the project is running, open [http://127.0.0.1:5001](http://127.0.0.1:5001) in your browser to access the interface.

 ![Image of the interface](path/to/your/image6.png)

To test the link shortening functionality, enter an AI artefact link and click the "Shorten" button to see the shortened link.

 ![Image of the interface after link has been shortened](path/to/your/image7.png)
