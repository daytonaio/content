---
title: "How to Setup PostgreSQL Playground in Daytona."
description: "Learn how to create PostgreSQL playground in Daytona and interact with the it hands-on in your favourite IDE terminal"
date: 2024-08-23
author: "Jeffrey Whewhetu"
tags: ["daytona", "postgresql", "devcontainer"]
---

# How to Setup PostgreSQL Playground in Daytona

## Introduction

This guide will walk you through on how to set up [PostgresQL](definitions/20240823_definitions_postgresql.md) database playground in a [Daytona workspace](definitions/20240819_definition_daytona workspace.md) which is a development environment management platform. In a world where companies what to increase development [productivity](definitions/20240819_definition_productivity.md) and individual developers want to start coding right away, Daytona is the best option.

### TL;DR

- What is needed to get started in this hands-on learning
- Overviews of both PostgreSQL and Daytona
- How to create a PostgreSQL devcontainer file
- Setup PostgreSQL playground workspace in Daytona
- Hands-on practice with PostgreSQL commands in the workspace
- Conclusion

## Prerequisities

In order to follow this guide, you’ll need the software installations below on your PC or Mac.
- An [IDE](definitions/20240819_definition_integrated development environment _ide_.md) like VS Code, link to install it [here](https://code.visualstudio.com/download) or just a terminal
- Docker, link to it [here](https://docs.docker.com/engine/install/)
- Daytona, link to install it [here](https://github.com/daytonaio/daytona#installing-daytona)

## Overview of PostgreSQL

[PostgreSQL](definitions/20240823_definitions_postgresql.md) or also known as Postgres is the world’s most advanced open source relational database system that has been in use by the developer community for over 35 years with so much great love shown to it because of its strong reputation for reliability, feature robustness and performance.

PostgreSQL has some much benefits on to why one should use it some are highlighted below:
- [Open Source](definitions/20240819_definition_open source.md) and Free: It’s a completely free software to install and use and also its source code is freely available online to see how it’s implemented under the hood. You don’t have to spend more to purchase license which might be very expensive
- Cross-Platform Compatibility: PostgreSQL can be run in most of the major OSes in the world. It can run on most Linux distros, Windows, and MacOS making it to be a number one choice.
- In-Exhaustive LIst of Features: Some of the features are Data Types, Data Integrity and Security. Lots of features can be found in the PostgreSQL website here with more being added in every major release.

## Overview of Daytona

Daytona is a self hosted and secure [open source](definitions/20240819_definition_open source.md) development environment manager that uses configurations from a project's repository to build workspace and provision the workspace in a platform of your choice. It's innovative and incredibly easy for all levels including beginners to get started with it.

Daytona provides some interesting features which make it one the best products in the area of simplifying development environments for both enterprise and individual levels.

Some of those features it boast of include:
- It has support for popular [IDE](definitions/20240819_definition_integrated development environment _ide_.md) like VS Code and JetBrains
- It connect with repository providers like GitHub, GitLab, BitBucket and Gitea
- It's very secure. It uses VPN connection to make that possible
- It has reverse proxy support

For more info about Daytona and it's features, check [here](https://daytona.io)

## Creating a DevContainer for PostgreSQL

A [development container](definitions/20240819_definition_development container.md) (or a devcontainer for short) allows you to use a [docker](definitions/20240819_definition_docker.md) container as a full-featured development environment. It can be configured to meet your development environment needs. It could include tools and runtimes like npm, [git](definitions/20240819_definition_git.md), maven, [Golang](definitions/20240819_definition_golang.md) compiler and others too.

For this guide we're going to create a [devcontainer](definitions/20240819_definition_development container.md) for PostgreSQL using a config file. The file is always named `devcontainer.json` with code syntax in it following the correct config specifications. Its a norm to keep the file in an hidden directory call `.devcontainer`

Let's get started. I will use the terminal to create mine in my linux PC but the commands should work fine on Mac terminal or the Windows powershell.

### **Step 1**: Create a Directory

Create a directory with any name of your choice and go into it. I use the name `postgresql-playground-in-daytona` and move into the directory.

  ```bash
mkdir postgresql-playground-in-daytona && cd postgresql-playground-in-daytona
  ```

### **Step 2**: Create the `.devcontainer` directory

Create a hidden directory called `.devcontainer` and enter it. This is where our devcontainer config file will be stored.

```bash
mkdir .devcontainer && cd .devcontainer
```

### **Step 3**: Create `devcontainer.json` file

Now, create a file called `devcontainer.json` and paste the following code into it and then save it.

```json
{
    "name": "PostgreSQL Dev Container Playground",
    "image": "mcr.microsoft.com/devcontainers/base:ubuntu",
    "features": {
        "ghcr.io/itsmechlark/features/postgresql:1": {
            "version": "latest"
        }
    }  
}
```

The `devcontainer.json` code content defines a configuration for a PostgreSQL development container environment.

- **`name`:** Set the name of the development container environment to ``PostgreSQL Dev Container Playground``.
- **`image`:** This uses a base Ubuntu image from Microsoft image repository.
- **`features`:** This configuration adds PostgreSQL setup in the environment.

Your directory structure should look like mine below if you follow along using the same directory name as I did earlier.

```
postgresql-playground-in-daytona/
├── .devcontainer/
│   ├── devcontainer.json
```

### **Step 4:** Go back to the top level

Paste the code below to go back to the top level of the directory you created

```bash
cd ..
ls -al
```

and you should see this output in the terminal:
  
```
├── .
├── ..
├── .devcontainer
├── .git
```

### **Step 5:** Initialize and make commit

Paste the code below to initialize git and commit the changes you made to your directory.

```bash
git init
git add .
git commit -m "inital commit"
```

### **Step 6:** Create a repository in GitHub

Create a repository without README, LICENSE or .gitignore files from GitHub web using the name of the directory you created. Mine is `postgresql-playground-in-daytona`.

You should see a code block similar to this from your GitHub web. Copy it and paste in your terminal or Windows Powershell for Windows PC users(Git must be installed in it)

```bash
git remote add origin https://github.com/YOUR-GITHUB-USERNAME/YOUR-DIRECTORY-NAME.git
git branch -M main
git push -u origin main
```

After you run the code, you'll be prompted to input your GitHub username and password.

You can find the GitHub repository where my devcontainer config is located which I used for this guide [here](https://github.com/c0d33ngr/postgresql-playground-in-daytona). I later added a README and LICENSE files which wasn't neccessary to follow along with this guide.

Now, we have successfully created a GitHub repository needed to spin up a devcontainer for PostgreSQL using Daytona.

## Setting Up PostgreSQL in Daytona

Before starting this section be sure `daytona` is installed in your PC

### Step 1

Run the code below to setup `daytona` server

```bash
daytona server
```

Your output should be similar to the screenshot below

![screenshot of running daytona server](assets/20240823_how_to_setup_postgresql_playground_in_daytona_img_1.jpg)

Choose yes and should see similar output in the screenshot below

![screenshot of successfully running daytona](assets/20240823_how_to_setup_postgresql_playground_in_daytona_img_2.jpg)
  
### Step 2

Run the command below to add your git provider if you haven't setup one

```bash
daytona git provider add
```

Follow the prompts after running the command to setup your provider. In our case it's GitHub

### Step 3

Run this command in terminal to add your preferred IDE.

```bash
daytona ide
```

### Step 4

Modified the terminal command below to create the dev environment of the repository you created in GitHub and follow the prompts after you run it. Don't forget to use the correct GitHub URL, in my case it's `https://github.com/c0d33ngr/postgresql-playground-in-daytona.git`

```bash
daytona create https://github.com/YOUR-USERNAME/YOUR-DIRECTORY-NAME.git
```

### Step 5

Run the code in your terminal to confirm the workspace is created for the repository.

```bash
daytona ls
```
You should see that the workspace is running

### Step 6

Run this command to open workspace in the IDE you selected when setting up your preferred one. The name of the workspace is usually the repository name if you didn't modify it when prompted in the creation of the workspace. In my case, it's `postgresql-playground-in-daytona`

```bash
daytona code WORKSPACE-NAME
```

Now, your preferred IDE should be open and you'll be prompted to reopen in container. Click it and the IDE should restart. Now, you should be in the workspace of the repository you created.

In my case, i used terminal SSH as the default IDE in my `daytona` installation. So my workspace is opened in my terminal.
![screenshot of my workspace in my terminal](assets/20240823_how_to_setup_postgresql_playground_in_daytona_img_3.jpg)

Follow the set of instructions in the next section to interact with the PostgreSQL development environment.

## Performing Some Basic PostgreSQL CRUD Operations in the Workspace

### Login to PostgreSQL using `psql` and username `postgres`

  ```bash
psql -U postgres
```

Your output should look this

  ![screenshot of logging in via psql](assets/20240823_how_to_setup_postgresql_playground_in_daytona_img_4.jpg)
  
### Create a Table
**Example**: The SQL code below creates a table named `users`.

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

Your output should display similar one as mine

![screenshoot of creating a database](assets/20240823_how_to_setup_postgresql_playground_in_daytona_img_5.jpg)


### Insert a Record
**Example**: The SQL codes insert different records into the table `users` that was created by us above

```sql
INSERT INTO users (name, email) VALUES ('Mark Zuckerberg', 'zuck@fb.com');
INSERT INTO users (name, email) VALUES ('Elon Musk', 'info@telsa.com');
INSERT INTO users (name, email) VALUES ('Bill Gates', 'bill.gates@gatesfoundation.org');
INSERT INTO users (name, email) VALUES ('Jack Dorsey', 'jack.dorsey@gmail.com');
  ```

You should have similar screen like this below

![screenshot of inserting records to table](assets/20240823_how_to_setup_postgresql_playground_in_daytona_img_6.jpg)

### Read Data from Table
**Example**: This SQL query selects all records in the table `users` and return them.

```sql
SELECT * FROM users WHERE name = 'Mark Zuckerberg';
  ```

Your output should display something similar

![screenshot of selecting a record from the table](assets/20240823_how_to_setup_postgresql_playground_in_daytona_img_7.jpg)

### Update a Table Record
**Example**: This SQL query updates the table `users` record where `id` is 1.

```sql
UPDATE users SET email = 'johndoe@email.com' WHERE id = 2;
  ```

You output should be similar

![screenshot of updating a record in the table](assets/20240823_how_to_setup_postgresql_playground_in_daytona_img_8.jpg)

### Delete a Table Record
**Example**: This SQL code deletes the record where `id` is 2.

```sql
DELETE FROM users WHERE id = 2;
```

You should have similar output

![screenshot of deleting a record from the table](assets/20240823_how_to_setup_postgresql_playground_in_daytona_img_9.jpg)

Run the SQL code below to check the table

```sql
SELECT * FROM users;
```

You should now see the deleted record is gone

![screenshot of querying the table for all records](assets/20240823_how_to_setup_postgresql_playground_in_daytona_img_10.jpg)

Now we are done with performing some PostgreSQL queries in the playground environment. To exit the PostgreSQL prompt type the command below

```sql
\q
```

![screenshot of ending psql shell](assets/20240823_how_to_setup_postgresql_playground_in_daytona_img_11.jpg)

## Conclusion

By following the steps above you should have learned how to set up a working PostgreSQL playground running on Daytona for you to start building or practice with PostgreSQL. From here, you could continue to explore the opportunities of using Daytona as your [dev environment](definitions/20240819_definition_development environment.md) that suits your needs.

## References

*[Daytona](https://daytona.io)*

*[PostgreSQL](https://postgresq.ort)*

*[DevContainer](https://containers.dev)*
