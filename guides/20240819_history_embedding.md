---
title: "Embedding and Searching Browser History with ChromaDB"
description: "A step-by-step guide to embedding and searching your browser history using ChromaDB using Azure or a local environment."
date: 2024-08-19
author: "Jacob Gaffke"
---

# Embedding and Searching Browser History with ChromaDB

## Introduction

This guide will walk you through the process of embedding and searching your browser history using ChromaDB, a powerful tool for managing and querying large sets of data with high efficiency. By the end of this guide, you’ll be able to embed your browser history into ChromaDB using either a local model or Azure's embedding service, and perform advanced searches with various filtering options.

Embeddings are numerical representations of data that capture its semantic meaning. In this context, embedding your browser history means transforming each URL entry into a vector that ChromaDB can efficiently search and compare.

### TL;DR

- **Export Browser History**: Use the Export Chrome History extension to get a CSV file.
- **Set Up Environment**: Install Daytona and create a workspace.
- **Embed History**: Run the `search.py` script to embed your history data.
- **Search History**: Perform searches using various filters and options.

## Preparations

### Installing Prerequisites

Before you begin, ensure you have [Daytona](https://github.com/daytonaio/daytona) installed.

You can install Daytona by running the following command in your terminal:

```bash
curl -L https://download.daytona.io/daytona/install.sh | sudo bash
```

Daytona creates a controlled environment where you can work on the project with all dependencies correctly configured, reducing the likelihood of compatibility issues.

### Exporting Browser History

To work with your browser history, you'll need to export it from your browser:

1. **Install the Export Chrome History Extension**: Download and install the [Export Chrome History](https://chrome.google.com/webstore/detail/export-chrome-history/) Chrome extension.
2. **Export to CSV**: Use the extension to export your browser history as a CSV file. Save it to a convenient location, like `~/Downloads/history.csv`.

Example CSV snippet:

```csv
visit_time,url,title,visit_count,typed_count
2023-08-10 12:34:56,http://example.com,Example Site,5,2
2023-08-09 11:22:33,http://anotherexample.com,Another Example,3,1
```

## Setting Up the Development Environment

### Creating a Daytona Workspace

With Daytona installed, you can create a workspace for the [`nkkko/history`](https://github.com/nkkko/history) repository:

```bash
daytona create https://github.com/nkkko/history --code
```

This command clones the repository and sets up the necessary environment. Daytona manages dependencies and configurations, ensuring that your environment is set up correctly for running the project scripts.

### Set Up Environment Variables (Optional for Azure)

If you plan to use Azure's embedding services instead of the local model, you need to configure the environment variables. Create a `.env` file in the root directory of the repository and add the following:

```env
AZURE_API_VERSION=<your_azure_api_version>
AZURE_ENDPOINT=<your_azure_endpoint>
AZURE_OPENAI_API_KEY=<your_azure_api_key>
```

**Example**:
```env
AZURE_API_VERSION=2021-06-01-preview
AZURE_ENDPOINT=https://your-resource-name.openai.azure.com/
AZURE_OPENAI_API_KEY=your-secret-key
```

**Why Azure?**  
Using Azure's embedding service can be beneficial if you need higher performance or better semantic accuracy in your embeddings, especially when dealing with large datasets.

## Embedding and Searching Your Browser History

### Embedding

With your development environment ready, you can now embed your browser history into ChromaDB. Embedding is the process of converting your history into vectors that ChromaDB can store and search. 

To embed using the local model (all-MiniLM-L6-v2), run:

```bash
python search.py --embed path/to/your/history.csv
```

**Practical Example**:
If your history CSV is located at `~/Downloads/history.csv`, the command would be:

```bash
python search.py --embed ~/Downloads/history.csv
```

This command reads each entry from the CSV, processes it into an embedding, and stores it in ChromaDB. The local model `all-MiniLM-L6-v2` is lightweight and works well for most purposes.

**Using Azure Embeddings**:
If you’re leveraging Azure for embeddings, use the `--azure` flag:

```bash
python search.py --embed ~/Downloads/history.csv --azure
```

### Searching

Once your history is embedded, you can perform searches using the `search.py` script. Here's how to use it effectively:

```bash
python search.py "search query"
```

#### Refining Searches

When searching your embedded browser history, using filters can help you narrow down results and make your searches more effective:

1. **Domain (`--domain`)**: Restrict results to a specific website. Useful when you remember the site but not the exact URL.
   - *Example*: `python search.py "article title" --domain example.com`

2. **Newest (`--newest`)**: Sort results by the most recent entries. Ideal for finding pages you visited recently.
   - *Example*: `python search.py "recent topic" --newest`

3. **Visit Count (`--visit-count`)**: Filter results by a minimum number of visits. Helps focus on frequently visited pages.
   - *Example*: `python search.py "important page" --visit-count 5`

4. **Typed Count (`--typed-count`)**: Filter by how often you manually typed the URL. Targets pages you intentionally visited.
   - *Example*: `python search.py "favorite site" --typed-count 3`

5. **Transition Type (`--transition`)**: Filter by how you arrived at a URL (e.g., link, typed, reload). Useful for distinguishing between different browsing actions.
   - *Example*: `python search.py "specific content" --transition typed`

**Comprehensive Example**:
```bash
python search.py "search query" --domain example.com --newest --visit-count 5 --typed-count 2 --transition typed
```

#### Practical Scenario

Imagine you frequently visit a research site. You want to find the latest article you visited on that site. You would run:

```bash
python search.py "latest research" --domain researchsite.com --newest
```

## Common Issues and Troubleshooting

**Problem:**  
The script fails to embed the CSV file.

**Solution:**  
Ensure that the CSV file is correctly formatted and accessible from the path provided. Double-check your Python environment and dependencies.

---

**Problem:**  
Azure embeddings are not being used despite setting environment variables.

**Solution:**  
Verify that the `.env` file is correctly configured and located in the root directory. Ensure that the Azure keys and endpoints are correct and match the required format.

---

**Problem:**  
Search results don’t seem to match your query.

**Solution:**  
Check if the correct embedding model is being used. If the local model is inadequate, try using Azure's embedding service for more accurate results. Also, review your filters and search query for specificity.

## Conclusion

By following this guide, you've successfully set up a system to embed and search your browser history using ChromaDB. You now have a powerful tool at your disposal for exploring your browsing habits, whether for productivity analysis, research, or personal curiosity. 

You can continue experimenting with different embedding models and search parameters to refine your results. Consider expanding this setup to include other data types or integrate it into larger data analysis projects.

## References

- [ChromaDB Documentation](https://chromadb.com/docs)
- [Daytona Installation Guide](https://daytona.io/docs/installation)
- [Export Chrome History Extension](https://chrome.google.com/webstore/detail/export-chrome-history/)

For further reading, consider exploring guides on data embedding techniques and using alternative embedding models for specialized tasks.
