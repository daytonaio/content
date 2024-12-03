---
title: "Embedding Browser History with ChromaDB"
description: "Learn how to embed and search browser history using ChromaDB and Azure OpenAI for semantic search capabilities."
date: 2024-08-20
author: "David Anyatonwu"
tags: ["chromadb", "embeddings", "browser-history", "semantic-search", "azure", "python"]
---

# Embedding Browser History with ChromaDB

## Introduction

In today's digital age, our browser history contains a wealth of information about our online activities, interests, and research. However, searching through this vast amount of data can be challenging and time-consuming. This guide introduces a powerful solution that leverages [ChromaDB](/definitions/20240820_chromadb_definition.md) and [embeddings](/definitions/20240820_embeddings_definition.md) to make your browser history searchable and more accessible.

We'll walk you through setting up a Python-based tool that can embed your browser history into a [vector database](/definitions/20240820_vector_database_definition.md), allowing for [semantic search](/definitions/20240820_semantic_search_definition.md) capabilities. By the end of this guide, you'll have a powerful system for searching your browsing history based on meaning rather than just keywords.

### Prerequisites

Before starting this guide, ensure you meet the following requirements:

**System Requirements:**
- Operating System: Windows 10+, macOS 10.15+, or Linux
- RAM: Minimum 4GB (8GB recommended)
- Storage: 1GB free space
- Internet connection for downloading dependencies

**Required Knowledge:**
- Basic command line usage
- Basic understanding of Python
- Familiarity with browser extensions

### TL;DR

- Set up a development environment using Daytona
- Export your browser history to a CSV file
- Embed your history into ChromaDB using either local or Azure OpenAI embeddings
- Perform semantic searches on your embedded browser history

### Materials and Requirements Checklist

Before starting this guide, ensure you have the following:

**Required:**
- [ ] [Daytona](https://github.com/daytonaio/daytona?tab=readme-ov-file#installing-daytona) installed on your system
- [ ] Python 3.8 or higher
- [ ] Chrome browser installed (for history export)
- [ ] At least 4GB of free RAM for processing
- [ ] Git installed for cloning the repository

**Optional (for Azure OpenAI integration):**
- [ ] Azure account with active subscription
- [ ] Azure OpenAI service enabled
- [ ] Azure OpenAI API key
- [ ] Azure OpenAI endpoint URL

**Software Dependencies:**
- [ ] ChromaDB
- [ ] Pandas
- [ ] Python-dotenv
- [ ] SentenceTransformers (for local embeddings)
- [ ] Azure OpenAI SDK (if using Azure embeddings)

**Time Requirements:**
- Setup: ~15 minutes
- History Export: ~5 minutes
- Embedding Process: 30-120 minutes (depending on history size)

## Step 1: Preparations

### Step 1.1: Install Required Software

1. Install Daytona following the [official installation guide](https://github.com/daytonaio/daytona?tab=readme-ov-file#installing-daytona)
2. Install the Chrome browser if not already installed
3. Install Git for version control

### Step 1.2: Export Browser History

1. Install the Export Chrome History extension ([Chrome Web Store](https://chromewebstore.google.com/detail/export-chrome-history/dihloblpkeiddiaojbagoecedbfpifdj?hl=en))
2. Export your history to CSV format

**Note:** Review the exported CSV file for sensitive information before proceeding.

### Confirmation
✓ Verify that:
- Daytona is installed (`daytona --version` shows version number)
- Chrome extension is installed and working
- CSV file is exported and accessible

## Step 2: Setting Up the Development Environment

### Step 2.1: Create Daytona Workspace

1. Open your terminal and run:

```bash copy
# Clone the repository and create a new Daytona workspace
# The --code flag automatically opens your preferred editor
# Ensure daytona server is running, if not run `daytona server`

daytona create https://github.com/nkkko/history --ide code
```

Expected output:
```
Creating workspace...
Cloning repository...
Setting up development environment...
Workspace 'history' created successfully!
```

2. If the editor doesn't open automatically:

```bash
# Open the workspace in your default editor
daytona code
```

### Step 2.2: Configure Environment

1. Set up environment variables:

```bash
# Copy the example environment file
cp .env.example .env

# Edit the .env file with your configuration
# For Azure OpenAI users:
echo "AZURE_API_VERSION=2023-05-15
AZURE_ENDPOINT=https://your-resource.openai.azure.com
AZURE_OPENAI_API_KEY=your-key-here" > .env

# Set proper permissions
chmod 600 .env
```

2. Install dependencies:
Daytona automatically installs the required Python packages from `requirements.txt`. You can also install them manually:
```bash
# Install all required Python packages
pip install -r requirements.txt

# Install sentence-transformers explicitly (required for embeddings)
pip install sentence_transformers
```

### Confirmation
✓ Verify that:
- `.env` file exists with correct permissions
- All packages are installed (`pip list` shows required packages)
- sentence-transformers is installed (`python -c "import sentence_transformers"` runs without error)
- Dev container is running if using VS Code

## Step 3: Processing and Searching Your History

### Step 3.1: Embedding Your History

First, embed your history data:

```bash
# Start the embedding process
python search.py --embed history.csv
```

You'll see a progress bar showing the embedding status:
```
Embedding CSV Rows: 100%|███████████████████████████████████████████████████| 5877/5877 [03:34<00:00, 27.34row/s]
Embedded data from history.csv
```

### Step 3.2: Basic Search

Once your history is embedded, you can start searching. Let's try a basic search:

```bash
python search.py "machine learning"
```

Example output:
```
1. AI Image Generator
   URL: https://deepai.org/machine-learning-model/text2img
   Date: 11/30/2024 Time: 22:01:22
   Visit Count: 2
   Typed Count: 0
   Transition: reload
   Relevance: 0.15

2. zack (in SF) on X: "Competitive programming is like 90% memorization..."
   URL: https://x.com/zack_overflow/status/1862216354750923188
   Date: 11/28/2024 Time: 21:07:18
   Visit Count: 2
   Typed Count: 0
   Transition: link
   Relevance: 0.07

3. Neural Networks: Zero To Hero
   URL: https://karpathy.ai/zero-to-hero.html
   Date: 12/2/2024 Time: 8:20:36
   Visit Count: 2
   Typed Count: 1
   Transition: reload
   Relevance: 0.05

... and more results ...
```

**Note:** The relevance score indicates how closely each result matches your query. Higher scores (closer to 1.0) indicate better matches.

### Step 3.3: Advanced Search Options

You can refine your search using various options:

```bash
--domain DOMAIN     # Filter URLs by domain
--newest           # Sort by newest first
--visit-count N    # Filter by minimum visit count
--typed-count N    # Filter by minimum typed count
--transition TYPE  # Filter by transition type (link/typed/reload)
--azure            # Use Azure OpenAI for search
```

Example advanced searches:

1. Filter by domain and sort by newest:
```bash
python search.py "python tutorials" --domain python.org --newest
```

2. Filter by visit count and transition type:
```bash
python search.py "documentation" --visit-count 5 --transition typed
```

3. Using Azure OpenAI for search (if data was embedded with Azure):
```bash
python search.py "data science" --azure --domain coursera.org
```

### Confirmation
✓ Verify that:
- Embedding process completed successfully
- Search queries return relevant results
- Filters work as expected
- Results show proper formatting and relevance scores





## Conclusion

You've now set up a powerful tool to semantically search your browser history! This can be incredibly useful for recalling important information, tracking your research progress, or analyzing your browsing patterns. As you continue to use this tool, you may find new and innovative ways to leverage your browsing data.

Consider periodically re-embedding your history to keep your searchable database up-to-date with your latest browsing activities.

## References

### Official Documentation
- [ChromaDB Documentation](https://docs.trychroma.com/)
- [SentenceTransformers Documentation](https://www.sbert.net/)
- [Azure OpenAI Service Documentation](https://docs.microsoft.com/en-us/azure/cognitive-services/openai/)

### Related Guides
- [Understanding Vector Databases](/guides/20240820_understanding_vector_databases.md)
- [Getting Started with Azure OpenAI](/guides/20240820_azure_openai_getting_started.md)

### Tools and Resources
- [Export Chrome History Extension](https://chromewebstore.google.com/detail/export-chrome-history/dihloblpkeiddiaojbagoecedbfpifdj)
- [Project Repository](https://github.com/nkkko/history)

---