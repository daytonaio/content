---
title: "Browser History Embedding and Search with ChromaDB"
description: "A detailed guide on embedding and searching browser history using ChromaDB with support for both local and Azure embeddings."
date: 2024-08-19
author: "Jacob Gaffke"
---

# 🔍 Browser History Embedding and Search with ChromaDB: A Comprehensive Guide

## Table of Contents

1. [Introduction](#introduction)
2. [TL;DR](#tl;dr)
3. [Key Components](#key-components)
4. [Preparations](preparations)
5. [Step-by-Step Setup](#step-by-step-setup)
6. [Running the Embedding Process](#running-the-embedding-process)
7. [Performing Searches on Your Embedded Data](#performing-searches-on-your-embedded-data)
8. [Understanding the Code: Key Functions in search.py](#understanding-the-code-key-functions-in-searchpy)
9. [Project Structure and File Breakdown](#project-structure-and-file-breakdown)
10. [Common Issues and Troubleshooting](#Common-issues-and-troubleshooting)
11. [Conclusion](#conclusion)
12. [References](#references)

---

## Introduction

This project enables embedding and searching of browser history using ChromaDB with local or Azure models. The core idea is to transform your browser history into vector embeddings, which can then be queried and searched using semantic similarity. It converts browser activity into vector embeddings, facilitating efficient and context-aware searches through semantic similarity. Unlike traditional keyword searches, this method captures the relationships and meanings between data points, providing more nuanced and relevant query results.

This guide will walk you through embedding and searching your browser history using ChromaDB. Whether you’re a developer exploring personalized search or a data enthusiast curious about embedding techniques, this guide covers it all. You'll learn how to set up your environment, export browser history, embed the data into vectors using local or Azure models, and perform efficient searches. We’ll break down each step with detailed explanations, focusing especially on embedding models and the flexibility between local and cloud-based (Azure) options.

---

### TL;DR

- **Export Browser History**: Use the Export Chrome History extension to get a CSV file.
- **Set Up Environment**: Install Daytona and create a [workspace](/definitions/d/daytona-workspace).
- **Embed History**: Run the `search.py` script to embed your history data.
- **Search History**: Perform searches using various filters and options.

---

## Key Components

### 1. **ChromaDB: The Vector Database**

ChromaDB is a vector database that lets you efficiently store and query embeddings. Think of it as the engine that powers all your search capabilities by indexing your browser history as vectorized data.

### 2. **Embedding Models: Turning Text into Vectors**

Embedding models are responsible for converting text (like your browser history) into vector representations. This project supports:

- **Local Embedding Model**: `all-MiniLM-L6-v2`, from [SentenceTransformers](https://www.sbert.net/), a lightweight model that runs locally.
- **Azure OpenAI Model**: For those who want cloud-powered embeddings with Microsoft’s Azure infrastructure.

### 3. **Daytona: Your Development Environment Manager**

Daytona is used to containerize and set up your development environment quickly. Here’s how to get started:

---

## Preparations

### Installing Prerequisites

Before you begin, ensure you have [Daytona](https://github.com/daytonaio/daytona) installed.

You can install Daytona by running the following command in your terminal:

```bash
curl -L https://download.daytona.io/daytona/install.sh | sudo bash
```

Daytona creates a controlled [development environment](/definitions/d/development-environment) where you can work on the project with all dependencies correctly configured, reducing the likelihood of compatibility issues.

#### **Create Your Daytona Workspace**

Create your workspace using this command:

```bash
daytona create https://github.com/nkkko/history --code
```

This automatically sets up a containerized environment where you can run and modify the project without worrying about compatibility issues.

---

## Step-by-Step Setup

### 1. **Export Your Browser History**

Before diving into the code, you need your browser history in a `.csv` format. The easiest way to do this is through the [Export Chrome History](https://chromewebstore.google.com/detail/export-chrome-history/dihloblpkeiddiaojbagoecedbfpifdj?hl=en) Chrome extension.

- **Steps to Export:**
  1. Install the extension from the Chrome Web Store.
  2. Use the extension to export your history.
  3. Save the file as `history.csv` or any name you prefer.

---

### 2. **Install Dependencies**

Once the workspace is set up, navigate to your project directory and install the required Python packages:

```bash
pip install -r requirements.txt
```

This command ensures all necessary libraries, like ChromaDB and SentenceTransformers, are ready to go.

---

### 3. **(Optional) Set Up Azure Embeddings**

If you want to leverage Azure’s cloud embeddings, you’ll need to set up environment variables:

1. Create a `.env` file in the project’s root directory.
2. Add the following variables:

```env
AZURE_API_VERSION=<your_azure_api_version>
AZURE_ENDPOINT=<your_azure_endpoint>
AZURE_OPENAI_API_KEY=<your_azure_api_key>
```

If you skip this step, the script will default to using the local embedding model.

---

## Running the Embedding Process

### What Are Embeddings?

Embeddings are vector representations of text. Instead of storing words or sentences as raw text, embeddings convert them into numerical vectors that capture semantic meaning. In this project, each URL, page title, and metadata from your browser history is transformed into a vector that can be efficiently searched using similarity measures.

### **Embedding Your Browser History**

To start embedding your history, run:

```bash
python search.py --embed path/to/your/history.csv
```

This command reads your `.csv` file, processes each row, and creates vector embeddings using the `all-MiniLM-L6-v2` model by default.

#### **Using Azure for Embeddings (Optional)**

If you’ve set up Azure credentials, you can use the `--azure` flag to switch to cloud-based embeddings:

```bash
python search.py --embed path/to/your/history.csv --azure
```

**What’s Happening Under the Hood?**

- The script reads the `.csv` file and parses each entry.
- It then uses either the local model or Azure API to generate embeddings.
- These embeddings are stored in ChromaDB for fast, semantic querying.

### Local vs. Cloud Embeddings: When to Use What?

- **Local Model (`all-MiniLM-L6-v2`)**:
  - Lightweight, doesn’t require internet.
  - Best for small-scale projects or testing.
- **Azure Embeddings**:
  - Cloud-based, suitable for large datasets.
  - Can handle more complex and nuanced queries.

---

## Performing Searches on Your Embedded Data

Once your data is embedded, you can perform searches using:

```bash
python search.py "your search query"
```

The query is converted into a vector, and ChromaDB searches for similar vectors in the stored history.

### Search Options and Filters

You can refine your search using these flags:

- **`--domain`**: Filter by specific domains (e.g., `example.com`).
- **`--newest`**: Prioritize recent results.
- **`--visit-count`**: Filter by a minimum number of visits.
- **`--typed-count`**: Filter by entries you typed directly (e.g., not auto-filled).
- **`--transition`**: Filter by how the page was accessed (e.g., via a link, typing, or reload).

**Example Command:**

```bash
python search.py "AI tools" --domain example.com --newest --visit-count 5
```

This search prioritizes the most recent pages from `example.com` that were visited at least five times.

---

## Understanding the Code: Key Functions in `search.py`

Here’s a quick overview of the core functions and what they do:

- **`create_chroma_client()`**: Initializes ChromaDB with a persistent storage path, ensuring your embeddings are saved across sessions.
- **`create_or_get_collection(client, embedding_function)`**: Either creates a new collection or retrieves an existing one for storing embeddings. A collection is like a table in a traditional database, but for vectors.
- **`embed_csv(csv_file, collection)`**: Reads the `.csv` file, processes each entry, and adds embeddings to the ChromaDB collection.
- **`search(query, collection, n_results=10, domain=None, newest=False, visit_count=None, typed_count=None, transition=None)`**: Handles querying the database, applying filters, and returning results based on similarity.

---

## Project Structure and File Breakdown

- **`requirements.txt`**: Lists all the Python libraries you need to run this project.
- **`README.md`**: The documentation for the project (you’re reading an extended version here).
- **`search.py`**: The main script where all the magic happens—embedding and searching.

---

## Common Issues and Troubleshooting

- **Script Not Running**: Ensure that your Python environment is properly configured and that all dependencies are installed. Check for any error messages in the terminal for specific issues.
- **The script fails to embed the CSV file**: Ensure that the CSV file is correctly formatted and accessible from the path provided. Double-check your Python environment and dependencies.
- **Getting Irrelevant Search Results?**: Check if the correct [embedding](/definitions/d/embedding) model is being used. If the local model is inadequate, try using Azure's [embedding](/definitions/d/embedding) service for more accurate results. Also, review your filters and search query for specificity.
- **Azure [embedding](/definitions/d/embedding)s are not being used despite setting environment variables.**: Verify that the `.env` file is correctly configured and located in the root directory. Ensure that the Azure keys and endpoints are correct and match the required format.

---

## Conclusion

By following this guide, you’ve transformed your browser history into a searchable, vectorized dataset using ChromaDB. Now you can explore more advanced filtering, integrate additional data sources, or even switch models based on your needs.

You can continue experimenting with different [embedding](/definitions/d/embedding) models and search parameters to refine your results. Consider expanding this setup to include other data types or integrate it into larger data analysis projects

## References

- [ChromaDB GitHub Repositry](https://github.com/nkkko/history.git)
- [Daytona GitHub Repository](https://github.com/daytonaio/daytona)
- [SentenceTransformers Documentation](https://www.sbert.net)
- [Daytona Installation Guide](https://daytona.io/docs/installation/installation/)
- [Export Chrome History Extension](https://chrome.google.com/webstore/detail/export-chrome-history/)
