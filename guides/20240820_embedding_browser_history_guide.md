---
title: "Embedding and Searching Browser History with ChromaDB"
description: "A comprehensive guide on how to embed and search your browser history using ChromaDB and optional Azure OpenAI embeddings."
date: 2024-08-20
author: "David Anyatonwu"
---

# Embedding and Searching Browser History with ChromaDB

## Introduction

In today's digital age, our browser history contains a wealth of information about our online activities, interests, and research. However, searching through this vast amount of data can be challenging and time-consuming. This guide introduces a powerful solution that leverages [ChromaDB](/definitions/20240820_chromadb_definition.md) and [embeddings](/definitions/20240820_embeddings_definition.md) to make your browser history searchable and more accessible.

We'll walk you through setting up a Python-based tool that can embed your browser history into a [vector database](/definitions/20240820_vector_database_definition.md), allowing for [semantic search](/definitions/20240820_semantic_search_definition.md) capabilities. This means you can find relevant web pages based on the meaning of your search query, not just exact keyword matches. The tool supports both local embeddings and [Azure OpenAI](/definitions/20240820_azure_openai_definition.md) embeddings, giving you flexibility in your setup.

### TL;DR

- Set up a development environment using Daytona
- Export your browser history to a CSV file
- Embed your history into ChromaDB using either local or Azure OpenAI embeddings
- Perform semantic searches on your embedded browser history

## Step 1: Preparations

Before we begin, ensure you have the following prerequisites:

- [Daytona](https://github.com/daytonaio/daytona) installed on your system
- A CSV export of your browser history (we'll cover how to get this)
- (Optional) An Azure account with OpenAI API access for enhanced embeddings

### Exporting Your Browser History

To get started, you'll need to export your browser history to a CSV file:

1. Install the [Export Chrome History](https://chromewebstore.google.com/detail/export-chrome-history/dihloblpkeiddiaojbagoecedbfpifdj?hl=en) Chrome extension.
2. Use the extension to export your history, saving it as a `.csv` file.

**Note:** Keep this CSV file handy, as we'll use it later in the process.

## Step 2: Setting Up the Development Environment

We'll use Daytona to create a consistent and isolated development environment for our project.

### Create a Daytona Workspace

1. Open your terminal and run the following command to create a new Daytona workspace:

```bash
daytona create https://github.com/nkkko/history --code
```
![Running Daytona](/assets/20240820_embedding_browser_history_img1.png)

This command clones the repository and sets up a workspace for you.

1. Once the workspace is created, Daytona will automatically open your preferred code editor. If it doesn't, you can manually open it with:

```bash
daytona code
```

### Configure the Environment

1. If you plan to use Azure OpenAI embeddings, create a `.env` file in the root directory of the project with the following content:

```
AZURE_API_VERSION=<your_azure_api_version>
AZURE_ENDPOINT=<your_azure_endpoint>
AZURE_OPENAI_API_KEY=<your_azure_api_key>
```

Replace the placeholders with your actual Azure OpenAI API details.

2. Install the required Python packages:

```bash
pip install -r requirements.txt
```

## Step 3: Understanding Embeddings

Before we proceed with embedding your browser history, let's briefly discuss what embeddings are and why they're useful in this context.

Embeddings are dense vector representations of text that capture semantic meaning. When we convert text (in this case, your browser history entries) into embeddings, we're essentially transforming them into a format that allows for semantic similarity comparisons.

The tool offers two embedding options:

1. **Local Embeddings (Default)**: Uses the `all-MiniLM-L6-v2` model from [SentenceTransformers](/definitions/20240820_sentencetransformers_definition.md). This option runs entirely on your local machine and doesn't require an internet connection or API keys.

2. **Azure OpenAI Embeddings**: Utilizes Azure's powerful embedding service for potentially more accurate results. This option requires an Azure account and API keys.

The choice between these options depends on your needs for accuracy, processing speed, and data privacy.

**Comparison of Local and Azure OpenAI Embeddings**

| Feature | Local Embeddings | Azure OpenAI Embeddings |
| --- | --- | --- |
| Accuracy | Good | Higher |
| Processing Speed | Fast | Slower (dependent on internet connection) |
| Data Privacy | Local data, no cloud transmission | Data sent to Azure for processing |
| Requirements | No additional setup | Azure account and API keys required |

**Performance Metrics**

The performance of the embedding process and search queries will depend on the size of your browser history and the chosen embedding method. Here are some general guidelines:

| Browser History Size | Local Embedding Time | Azure OpenAI Embedding Time | Search Query Time |
| --- | --- | --- | --- |
| 1,000 entries | < 1 minute | 1-2 minutes | < 1 second |
| 10,000 entries | 5-10 minutes | 10-30 minutes | 1-5 seconds |
| 100,000 entries | 1-2 hours | 2-6 hours | 10-30 seconds |

**Security and Privacy**

When using Azure OpenAI embeddings, your browser history data will be transmitted to Azure for processing. This may raise privacy concerns for some users. If you're concerned about data privacy, using local embeddings is a suitable alternative.

## Alternatives and Comparisons

While this tool offers unique capabilities, it's worth considering alternatives for searching and managing your browser history:

1. **Browser's Built-in Search**: 
   - Pros: Quick and easy to use, no setup required.
   - Cons: Limited to keyword matching, often lacks advanced filtering options.

2. **Browser History Extensions**:
   - Examples: History Trends, Better History (Chrome extensions)
   - Pros: Offer better organization and visualization of browsing history.
   - Cons: Usually lack semantic search capabilities, limited to a single browser.

3. **Bookmarking Services**:
   - Examples: Pocket, Raindrop.io
   - Pros: Good for intentional saving and organizing of web pages.
   - Cons: Require manual input, don't capture your entire browsing history automatically.

4. **Personal Knowledge Management Tools**:
   - Examples: Notion, Obsidian
   - Pros: Offer structured data management and note-taking capabilities.
   - Cons: Require manual input and curation, not specifically designed for browser history.

5. **Local Desktop Search Tools**:
   - Examples: Everything (Windows), Spotlight (macOS)
   - Pros: Can index and search local files, including browser history exports.
   - Cons: Lack semantic understanding, limited to local data.

6. **Command-line History Search**:
   - Example: Using grep or similar tools on exported history files
   - Pros: Fast and flexible for power users.
   - Cons: Requires technical knowledge, lacks semantic understanding.

Our ChromaDB-based tool stands out by offering:
- Semantic search across your entire browsing history
- No need for manual curation or bookmarking
- Cross-browser support (when importing history from multiple browsers)
- Local processing option for privacy-conscious users
- Scalability to handle large history datasets efficiently

While each alternative has its strengths, our tool provides a unique combination of comprehensive history coverage, semantic understanding, and flexibility in deployment options.

## Step 5: Searching Your Embedded History

Once the embedding process is complete, you can start searching your browser history using semantic queries.

### Basic Search

To perform a basic search, use the following command:

```bash
python search.py "your search query"
```

For example:

```bash
python search.py "machine learning tutorials"
```

### Advanced Search Options

The tool provides several options to refine your search:

- `--domain`: Filter results by a specific domain
- `--newest`: Sort results by the most recent date and time
- `--azure`: Use Azure OpenAI embeddings for the search (if you used Azure for embedding)
- `--visit-count`: Filter by minimum visit count
- `--typed-count`: Filter by minimum typed count
- `--transition`: Filter by transition type (link, typed, or reload)

Example of an advanced search:

```bash
python search.py "data visualization techniques" --domain medium.com --newest --visit-count 5
```

This search would look for pages about data visualization techniques, specifically on Medium.com, sorted by the newest first, and only including pages you've visited at least 5 times.

## Step 6: Understanding the Results

The search results will be displayed in your terminal, providing rich information about each matching entry:

```
1. Introduction to Data Visualization with Python
   URL: https://medium.com/towards-data-science/introduction-to-data-visualization-in-python-89a54c97fbed
   Date: 2024-08-15 Time: 14:30:22
   Visit Count: 7
   Typed Count: 2
   Transition: link
   Relevance: 0.92

2. ...
```

The relevance score indicates how closely the result matches your query semantically. A higher score means a more relevant result.

## Common Issues and Troubleshooting

**Problem:** The embedding process is very slow.

**Solution:** If you're using local embeddings on a large history file, this is normal. Consider using Azure OpenAI embeddings for faster processing on large datasets.

**Problem:** Search results are not as relevant as expected.

**Solution:** Try refining your search query or using more specific filters. If using local embeddings, consider switching to Azure OpenAI embeddings for potentially more accurate results.

**Problem:** Error when trying to use Azure OpenAI embeddings.

**Solution:** Ensure that your `.env` file is correctly set up with valid Azure API details. Double-check that you have the necessary permissions and quota in your Azure account.

## Conclusion

You've now set up a powerful tool to semantically search your browser history! This can be incredibly useful for recalling important information, tracking your research progress, or analyzing your browsing patterns. As you continue to use this tool, you may find new and innovative ways to leverage your browsing data.

Consider periodically re-embedding your history to keep your searchable database up-to-date with your latest browsing activities.

## References

- [ChromaDB Documentation](https://docs.trychroma.com/)
- [SentenceTransformers Documentation](https://www.sbert.net/)
- [Azure OpenAI Service Documentation](https://docs.microsoft.com/en-us/azure/cognitive-services/openai/)

For more advanced usage and customization options, refer to the [project's GitHub repository](https://github.com/nkkko/history).

---