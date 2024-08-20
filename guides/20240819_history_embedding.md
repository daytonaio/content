---
title: "Embedding and Searching Browser History with ChromaDB"
description: "A step-by-step guide to embedding and searching your browser history with ChromaDB using OpenAI or a local environment."
date: 2024-08-19
author: "Jacob Gaffke"
---

# Embedding and Searching Browser History with ChromaDB

## Introduction

[Embedding](/definitions/d/embedding) your browser history with ChromaDB is a great way to dive into the world of machine learning. In this guide, you'll learn how to transform your web activity into structured, searchable formats by converting URLs and metadata into numerical representations. You’ll be guided through setting up a development environment, [embedding](/definitions/d/embedding) your browser history, and running advanced searches using ChromaDB, whether you’re using a local model or an OpenAI compatible service.

This guide is perfect for those eager to understand [embeddings](/definitions/d/embedding) and explore their various applications. From setting up the necessary tools to crafting detailed search queries with filters, you’ll gain practical experience that will lay the foundation for future projects. Whether you’re a developer starting your journey into [embeddings](/definitions/d/embedding) or someone looking to better manage their digital footprint, these step-by-step instructions will help you create a functional project with ChromaDB.

### TL;DR

- **Export Browser History**: Use the Export Chrome History extension to get a CSV file.
- **Set Up Environment**: Install Daytona and create a [workspace](/definitions/d/daytona-workspace).
- **Embed History**: Run the `search.py` script to embed your history data.
- **Search History**: Perform searches using various filters and options.

## What Are Embeddings?

## Preparations

### Installing Prerequisites

Before you begin, ensure you have [Daytona](https://github.com/daytonaio/daytona) installed.

You can install Daytona by running the following command in your terminal:

```bash
curl -L https://download.daytona.io/daytona/install.sh | sudo bash
```

Daytona creates a controlled [development environment](/definitions/d/development-environment) where you can work on the project with all dependencies correctly configured, reducing the likelihood of compatibility issues.

### Exporting Browser History

To work with your browser history, you'll need to export it from your browser:

1. **Install the Export Chrome History Extension**: Download and install the [Export Chrome History](https://chrome.google.com/webstore/detail/export-chrome-history/) Chrome extension.
2. **Export to CSV**: Use the extension to export your browser history as a CSV file. Save it to a convenient location, such as `~/Downloads/history.csv`.

Example CSV snippet:

```csv
visit_time,url,title,visit_count,typed_count
2023-08-10 12:34:56,http://example.com,Example Site,5,2
2023-08-09 11:22:33,http://anotherexample.com,Another Example,3,1
```

## Setting Up the Development Environment

### Creating a Daytona Workspace

With Daytona installed, you can create a [workspace](/definitions/d/daytona-workspace) for the [`nkkko/history` repository](https://github.com/nkkko/history):

```bash
daytona create https://github.com/nkkko/history --code
```

This command clones the [repository](/definitions/r/repository) and sets up the necessary environment. Daytona manages dependencies and configurations, ensuring that your environment is set up correctly for running the project scripts.

### Set Up OpenAI Service (Optional)

There are many hosted models compatible with the OpenAI API. Here's a basic rundown of available services:

|                             | **Azure**                   | **OpenAI**                   | **Cohere**                  | **Anthropic**                | **Jurassic-2**              |
|-----------------------------|-----------------------------|------------------------------|-----------------------------|------------------------------|-----------------------------|
| **Model Size**              | 175B+ parameters            | 1B-175B+ parameters          | 6B-12B parameters           | 100B+ parameters             | 20B-178B parameters         |
| **Context Length**          | 4,000-32,000 tokens         | 4,000-32,000 tokens          | Up to 2,048 tokens          | Up to 100,000 tokens         | Up to 2,048 tokens          |
| **Vector Size**             | 1,536 dimensions            | 1,536 dimensions             | 512-768 dimensions          | 768-1,024 dimensions         | 1,024-2,048 dimensions      |
| **Time for Embedding**      | 0.5 - 6 seconds (varies)    | 0.5 - 6 seconds (varies)     | 0.2 - 4 seconds (varies)    | 0.5 - 6 seconds (varies)     | 1 - 5 seconds (varies)      |
| **API Cost**                | $0.0004-$0.0120 per token   | $0.0004-$0.0120 per token    | $0.0001-$0.0005 per token   | $0.0005-$0.0030 per token    | $0.0005-$0.0020 per token   |

#### Key Notes

1. **Model Size:**
  - **Azure & OpenAI:** The sizes refer to GPT-3 and GPT-4 models. GPT-3 has 175B parameters; GPT-4 is larger but the exact size is proprietary.
  - **Anthropic:** Claude models are estimated to be in the 100B+ range, but exact figures are not officially confirmed.

2. **Context Length:**
  - **OpenAI and Anthropic:** Both platforms offer models with larger context lengths, particularly in newer versions.
  - **Cohere & Jurassic-2:** Smaller context lengths compared to OpenAI's latest models.

3. **Time for Embedding:**
  - This is highly variable and depends on multiple factors, such as the specific model, server load, and input length. The provided ranges should be taken as rough estimates rather than definitive benchmarks.

4. **API Cost:**
  - **Azure & OpenAI:** The cost can vary significantly based on the model, with GPT-4 generally costing more per token than GPT-3.
  - **Cohere, Anthropic, and Jurassic-2:** These ranges are more general and reflect common usage scenarios. Always check the latest pricing from providers as it can change.

#### Environment Variables

Ensure you have the necessary environment variables configured in a local `.env` file. For example, this is how you would configure Azure:

```env
AZURE_API_VERSION=<your_azure_api_version>
AZURE_ENDPOINT=<your_azure_endpoint>
AZURE_OPENAI_API_KEY=<your_azure_api_key>
```

## Embedding and Searching Your Browser History

### Embedding

With your [development environment](/definitions/d/development-environment) ready, you can now embed your browser history into ChromaDB.

To embed using the local model (multi-qa-distilbert-cos-v1), run:

```bash
python search.py --embed path/to/your/history.csv  # Ex: ~/Downloads/history.csv
```

This command reads each entry from the CSV, processes it into an [embedding](/definitions/d/embedding), and stores it in ChromaDB. The local model `multi-qa-distilbert-cos-v1` is lightweight and works well for most purposes.

#### Using Azure Embeddings

If you’re leveraging Azure for [embeddings](/definitions/d/embedding), use the `--azure` flag:

```bash
python search.py --embed path/to/your/history.csv --azure
```

### Searching

Once your history is embedded, you can perform targeted searches using the `search.py` script.

To start a basic search, simply use:

```bash
python search.py "search query"
```

To refine your results, consider using filters. For example, if you recently read an article on "AI ethics" on `example.com` but can’t recall the exact URL or title, you can narrow your search to that specific domain:

```bash
python search.py "AI ethics" --domain example.com
```

This command restricts the search to `example.com`, making it easier to locate the specific page.

If you want to find the most recent page you visited about "quantum computing," you can sort the results by the latest entries:

```bash
python search.py "quantum computing" --newest
```

This will display the most recent pages related to "quantum computing," which is useful for quickly revisiting the latest content.

For frequently visited pages, such as those related to a project management tool, you can filter by the number of visits:

```bash
python search.py "project tasks" --visit-count 10
```

This filter highlights pages you’ve visited at least ten times, likely indicating their importance.

If you’re trying to locate a specific coding tutorial site that you’ve manually typed the URL for multiple times, use:

```bash
python search.py "python tutorial" --typed-count 3
```

This focuses on pages where you’ve intentionally typed the URL, helping you find the exact tutorial.

To find a document where you remember directly typing the URL, use:

```bash
python search.py "project proposal" --transition typed
```

This command searches for pages accessed by typing the URL directly, excluding those reached through links.

For a more complex search, such as finding the most recent paper on "deep learning" that you’ve visited multiple times on `researchsite.com`, you can combine multiple filters:

```bash
python search.py "deep learning" --domain researchsite.com --newest --visit-count 5
```

This command combines domain restriction, recent sorting, and visit count filtering, allowing you to quickly locate the most relevant content.

## Real-world Use Cases

Understanding how to apply the concepts in this guide to real-world scenarios can help you better appreciate the power of [embedding](/definitions/d/embedding) your browser history. Below are some practical examples of how this tool can be used in various contexts:

### Personal Productivity Tracking

For individuals looking to optimize their time online, this tool can be invaluable. By [embedding](/definitions/d/embedding) your browser history and using the search functionality, you can analyze how much time you spend on work-related sites versus leisure activities. For example, you could filter your history by domains associated with productivity tools (like Google Docs or Trello) and compare them against social media or entertainment sites. Over time, this data can reveal patterns in your online behavior, helping you make more informed decisions about time management.

**Example**:
```bash
python search.py "to do" --domain trello.com --newest
```

### Content Curation and Management

If you're a content creator or curator, keeping track of all the resources you come across online can be challenging. Using this guide, you can [embed](/definitions/d/embedding) and index your browsing history, allowing you to quickly retrieve articles, videos, or research papers you’ve encountered. For instance, if you're writing a blog post and need to revisit a source you found weeks ago, a quick search using relevant keywords or filters like visit count can bring it up immediately.

**Example**:
```bash
python search.py "python" --typed-count 3 --newest
```

### Academic Research

Researchers often sift through vast amounts of online material during literature reviews or while gathering data. By [embedding](/definitions/d/embedding) and searching your browser history, you can easily retrieve previously visited papers, articles, or datasets. This is particularly useful for ongoing projects where you may need to reference multiple sources over time. Additionally, you can filter results by the domain of academic databases or journals to focus solely on credible sources.

**Example**:
```bash
python search.py "machine learning" --domain arxiv.org --visit-count 2
```

### Personalized Content Recommendations

[Embedding](/definitions/d/embedding) your browser history can enhance personalized content recommendations by allowing you to track and retrieve relevant content easily. For example, if you frequently visit sites like Medium for articles on data science, embedding this history lets you quickly find similar content or revisit specific posts, ensuring your recommendations are more aligned with your interests.

**Example**:
```bash
python search.py "data science" --domain medium.com --newest
```

## Common Issues and Troubleshooting

### CSV Embedding Failure

**Problem:**  
The script fails to embed the CSV file.

**Solution:**  
Ensure that the CSV file is correctly formatted and accessible from the path provided. Double-check your Python environment and dependencies.

### Hosted Embeddings Not Applied

**Problem:**  
Hosted [embedding](/definitions/d/embedding) model is not being used despite setting environment variables.

**Solution:**  
Verify that the `.env` file is correctly configured and located in the root directory. Ensure that the keys and endpoints are correct and match the required format.

### Inaccurate Search Results

**Problem:**  
Search results don’t seem to match your query.

**Solution:**  
Check if the correct [embedding](/definitions/d/embedding) model is being used. If the local model is inadequate, try using a hosted [embedding](/definitions/d/embedding) service for more accurate results. Also, review your filters and search query for specificity.

## Conclusion

By following this guide, you've successfully set up a system to embed and search your browser history using ChromaDB. You now have a powerful tool at your disposal for exploring your browsing habits, whether for productivity analysis, research, or personal curiosity. 

You can continue experimenting with different [embedding](/definitions/d/embedding) models and search parameters to refine your results. Consider expanding this setup to include other data types or integrate it into larger data analysis projects.

## References

- [ChromaDB Documentation](https://chromadb.com/docs)
- [Daytona Installation Guide](https://daytona.io/docs/installation/installation/)
- [Export Chrome History Extension](https://chrome.google.com/webstore/detail/export-chrome-history/)

For further reading, consider exploring guides on data [embedding](/definitions/d/embedding) techniques and using alternative [embedding](/definitions/d/embedding) models for specialized tasks.
