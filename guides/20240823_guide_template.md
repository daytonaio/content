---
title: "How to Setup PostgreSQL Playground in Daytona."
description: "A brief description of what the guide covers. The description should be a maximum of 160 characters."
date: 2024-08-23
author: "Jeffrey Whewhetu"
tags: ["daytona", "postgresql", "devcontainer"]
---

# How to Setup PostgreSQL Playground in Daytona

## Introduction

This guide will walk you through on how to set up PostgresQL database playground in a Daytona environment which is a development environment management platform.

### TL;DR

- **Bullet Point Summary**: *[Summarize the key points in a few bullet points for quick reference.]*

## Prerequisities

In order to follow this guide, you’ll need the software installations below on your PC or Mac.
- VS Code, link to install it [here](https://code.visualstudio.com/download)
- Docker, link to it [here](https://docs.docker.com/engine/install/)
- Daytona, link to install it here

## Overview of PostgreSQL

PostgreSQL or also known as Postgres is the world’s most advanced open source relational database system that has been in use by the developer community for over 35 years with so much great love shown to it because of its strong reputation for reliability, feature robustness and performance.

PostgreSQL has some much benefits on to why one should use it some are highlighted below:
- Open Source and Free: It’s a completely free software to install and use and also its source code is freely available online to see how it’s implemented under the hood. You don’t have to spend more to purchase license which might be very expensive
- Cross-Platform Compatibility: PostgreSQL can be run in most of the major OSes in the world. It can run on most Linux distros, Windows, and MacOS making it to be a number one choice.
- In-Exhaustive LIst of Features: Some of the features are Data Types, Data Integrity and Security. Lots of features can be found in the PostgreSQL website here with more being added in every major release.

## Overview of Daytona

Daytona is a self hosted and secure open source development environment manager that use configurations from a project's repository to build workspace and provision the workspace in a platform of your choice. It's innovative and incredibly easy for all levels including beginners to get started with it.

Daytona provides some interesting features which make it one the best products in the area of simplifying development environments for both enterprise and individual levels.

Some of those features it boast of include:
- It has support for popular IDE like VS Code and JetBrains
- It connect with repository providers like GitHub, GitLab, BitBucket and Gitea
- It's very secure. It uses VPN connection to make that possible
- It has reverse proxy support

For more info about Daytona and it's features, check [here](https://daytona.io)

## Creating a DevContainer for PostgreSQL

A development container (or a devcontainer for short) allows you to use a docker container as a full-featured development environment. It can be configured to meet your development environment needs. It could include tools and runtimes like npm, git, maven, Golang compiler and others too.

For this guide we're going to create a devcontainer for PostgreSQL using a config file. The file is always named `devcontainer.json` with code syntax in it following the correct config specifications. Its a norm to keep the file in an hidden directory call `.devcontainer`

Let's get started. I will use the terminal to set up mine but the commands should work fine on Mac terminal or Windows powershell. You can also follow along with the GUI using any OS.

**Step 1**: Create a directory with any name of your choice and go into it. I use the name `postgresql-playground` and move into the directory.

```bash
mkdir postgresql-playground && cd postgresql-playground
```

**Step 2**: Create a hidden directory called `.devcontainer` and enter it. This is where our devcontainer config file will be stored.

```bash
mkdir .devcontainer && cd .devcontainer
```

**Step 3**: Now, create a file called `devcontainer.json` and paste the following code into it and then save it.

[CODE]

Code explanation

**Step 4**: While still in the same directory, create another file named `docker-compose.yml` and paste the code below into it. Save it

[CODE]

Code explanation

**Step 5**: In the same directory, create the last file named `.env` and paste code below. Save the file.

[CODE]

Code explanation

Your directory structure should look like mine if you follow along using the same directory name as I did.

```
postgresql-playground/
├── .devcontainer/
│   ├── .env
│   ├── docker-compose.yml
│   └── devcontainer.json
```

Now, we have successfully created the files needed to spin up a devcontainer for PostgreSQL using Daytona.

## Setting Up PostgreSQL in Daytona

## Performing Some Basic PostgreSQL CRUD Operations in the Workspace

- ### Create a Table
  **Example**: The SQL code below creates a table named `users`.

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

- ### Insert a Record
  **Example**: The SQL codes insert different records into the table `users` that was created by us above

```sql
INSERT INTO users (name, email) VALUES ('Mark Zuckerberg’, 'zuck@fb.com');
INSERT INTO users (name, email) VALUES ('Elon Musk', 'info@telsa.com');
INSERT INTO users (name, email) VALUES ('Bill Gates', 'bill.gates@gatesfoundation.org');
INSERT INTO users (name, email) VALUES ('Jack Dorsey', 'jack.dorsey@gmail.com');
```

- ### Read Data from Table
  **Example**: This SQL query selects all records in the table `users` and return them.

```sql
  SELECT * FROM users WHERE name = 'Mark Zuckerberg';
```

- ### Update a Table Record
  **Example**: This SQL query updates the table `users` record where `id` is 1.

```sql
  UPDATE users SET email = 'johndoe@email.com' WHERE id = 2;
```

- ### Delete a Table Record
  **Example**: This SQL code deletes the record where `id` is 2.

```sql
  DELETE FROM users WHERE id = 2;
```

## Conclusion

By following the steps above you should have learned how to set up a working PostgreSQL playground running on Daytona for you to start building or practice with PostgreSQL. From here, you could continue to explore the opportunities of using Daytona as your dev environment that suits your needs.

## References

*[Daytona](https://daytona.io)*

*[PostgreSQL](https://postgresq.ort)*

*[DevContainer](https://containers.dev)*

<!-- Note on Definitions -->
<!-- Throughout this guide, link relevant terms to their definitions using inline Markdown links. -->
<!-- Format: [term](/definitions/term.md) -->
<!-- If a definition doesn't exist, create it in the definitions directory and link to it. -->
