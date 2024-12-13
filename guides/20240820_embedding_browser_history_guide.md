---
title: "Embedding Browser History with ChromaDB"
description: "Create a powerful semantic search system for your browser history using vector embeddings and ChromaDB."
date: 2024-08-20
author: "David Anyatonwu"
tags: ["chromadb", "embeddings", "browser-history", "semantic-search", "azure", "python"]
---

# Embedding Browser History with ChromaDB

## Introduction

Have you ever tried searching your browser history for a page you visited but couldn't remember the exact title or URL? Traditional history search relies on exact keyword matches, which often fails to find what you're looking for. This guide introduces a powerful solution using [vector embeddings](/definitions/20240820_embeddings_definition.md) and [ChromaDB](/definitions/20240820_chromadb_definition.md) to make your browser history truly searchable by meaning, not just keywords.

Imagine searching for "machine learning tutorials" and finding that helpful article you read last month about "neural networks for beginners" – even though it never contained the exact words "machine learning tutorials". This is the power of [semantic search](/definitions/20240820_semantic_search_definition.md), and by the end of this guide, you'll have this capability for your entire browsing history.

### TL;DR

- Export Chrome history to CSV
- Convert history entries into vector embeddings using ChromaDB
- Create a semantic search system that understands meaning
- Search history using natural language queries
- Filter results by domain, visit count, and more

## Understanding Vector Embeddings and Semantic Search

Before we dive into the implementation, let's understand what makes this system powerful. When you search your browser history normally, you're limited to exact matches – like trying to find a book in a library by matching exact words in its title. Vector embeddings work differently:

1. **Converting Text to Numbers**: Each page title and URL in your history gets converted into a list of numbers (a vector) that captures its meaning:
   ```python
   "machine learning" → [0.2, -0.5, 0.8, ..., 0.3]
   "neural networks" → [0.3, -0.4, 0.7, ..., 0.4]
   ```

2. **Similarity by Distance**: Similar concepts end up with similar numbers:

  

3. **Smart Searching**: When you search, your query gets converted the same way, and ChromaDB finds the closest matching vectors:
   ```python
   Your search: "AI tutorials"
   Matches: "machine learning guide", "neural networks 101"
   ```

This is why semantic search can find relevant pages even when the exact words don't match.

### How ChromaDB Makes This Possible

ChromaDB handles three crucial tasks:
1. **Embedding Generation**: Converts text to vectors using models like SentenceTransformers
2. **Vector Storage**: Efficiently stores these vectors for quick retrieval
3. **Similarity Search**: Finds the closest vectors to your search query

Here's a visualization of how it works:
![ChromaDB Process](/guides/assets/20240820_embedding_browser_history_guide_img1.png)

## Prerequisites

Before we begin, ensure you have:
- [Daytona](/definitions/20240819_definition_daytona%20workspace.md) v0.12.1 or later installed
- Python 3.8 or higher
- Chrome browser (for history export)
- Azure account (optional, for Azure OpenAI embeddings)

## Step 1: Setting Up Your Development Environment

### Creating the Workspace

1. Open your terminal and create a new workspace using Daytona:

```bash
daytona create https://github.com/nkkko/history.git --ide code
```

![Creating Daytona Workspace](/guides/assets/20240820_embedding_browser_history_guide_img2.png)
2. Start your preferred IDE:

```bash
daytona code
```

### Installing Dependencies

**Note:** One good thing about daytona is that it uses the dev container feature to setup a developement environment. This means that you don't have to worry about installing the dependencies manually. Enabling you to focus on the code and not the setup. So the next step won't be needed if you are using daytona. as it handles all of this for you.

1. Install this required package:

```bash
pip install sentence_transformers
```



### Confirmation
✓ Verify your setup:
- Run `python -c "import chromadb"` to verify ChromaDB installation
- Check that your IDE opened successfully

## Step 2: Exporting Browser History

### Installing the Export Extension

1. Install the [Export Chrome History](https://chromewebstore.google.com/detail/export-chrome-history/dihloblpkeiddiaojbagoecedbfpifdj) extension
2. Click the extension icon and configure export settings:
   - Format: CSV
   - Fields: All (especially Title, URL, Visit Count, and Visit Time)
   
![Exporting Chrome History](/guides/assets/20240820_embedding_browser_history_guide_img4.png)

3. Save the CSV file in your project directory

**Warning:** Review the exported CSV file for sensitive information before proceeding.

### Confirmation
✓ Check your exported file:
- File ends with .csv extension
- Contains required columns (Title, URL, Visit Count, Visit Time)
- No sensitive information is included

## Step 3: Configuring the Environment

### Local Embeddings Setup
No additional configuration needed - the system will use [SentenceTransformers](/definitions/sentence_transformers.md) by default.

### Azure OpenAI Setup (Optional)
1. Create a `.env` file:

```bash
echo "AZURE_API_VERSION=2023-05-15
AZURE_ENDPOINT=your-azure-endpoint
AZURE_OPENAI_API_KEY=your-api-key" > .env
```

2. Set proper file permissions:
```bash
chmod 600 .env
```

**Warning:** Never commit your `.env` file to version control.

### Confirmation
✓ Verify your configuration:
- For local setup: No additional verification needed
- For Azure setup: Check `.env` file exists and has correct permissions

## Step 4: Understanding the Code

The main script (`search.py`) handles both embedding and searching. Let's examine the key components:

### Embedding Function
```python
def embed_csv(csv_file, collection):
    df = pd.read_csv(csv_file)
    documents = df['title'].tolist()
    metadatas = df.to_dict('records')
    collection.add(
        documents=documents,
        metadatas=metadatas
    )
```

This function:
1. Reads your history CSV
2. Extracts titles for embedding
3. Stores full records as metadata
4. Uses ChromaDB's add method to create and store embeddings

### Search Function
```python
def search(query, collection, n_results=10, **kwargs):
    where = {}
    if kwargs.get('domain'):
        where['domain'] = kwargs['domain']
    if kwargs.get('visit_count'):
        where['visit_count'] = {"$gte": kwargs['visit_count']}
        
    results = collection.query(
        query_texts=[query],
        n_results=n_results,
        where=where
    )
    return results
```

The search function supports:
- Semantic similarity via query_texts
- Filtering using ChromaDB's where clauses
- Customizable number of results

## Step 5: Embedding Your History

### Running the Embedding Process

1. Execute the embedding command:
```bash
python search.py --embed history.csv
```

![Embedding Process](/guides/assets/20240820_embedding_browser_history_guide_img4.png)


2. The process will:
   - Load your history CSV
   - Create embeddings for each entry
   - Store embeddings and metadata in ChromaDB
   - Show progress as it processes

**Note:** This process may take several minutes depending on your history size.

### Confirmation
✓ Verify successful embedding:
- Check for "Embedding complete" message
- Verify ChromaDB files created in ./chroma_db directory
- No error messages in the output

## Step 6: Searching Your History

### Basic Search
Try a simple search:
```bash
python search.py "machine learning tutorials"
```

![Basic Search Results](/guides/assets/20240820_embedding_browser_history_guide_img5.png)
### Advanced Search
Use filters for more specific results:
```bash
python search.py "python documentation" --domain python.org --newest --visit-count 2
```

![Advanced Search Results](/guides/assets/20240820_embedding_browser_history_guide_img6.png)

### Understanding Results

Each result includes:
- Title and URL
- Visit timestamp
- Visit and typed counts
- Transition type
- Relevance score (cosine similarity from 0 to 1)

### Confirmation
✓ Verify search functionality:
- Results are relevant to your query
- Filters work as expected
- Results include all expected metadata

## Common Issues and Troubleshooting

### Memory Issues
**Problem:** Out of memory during embedding
**Solution:** Reduce batch size in `search.py`:
```python
BATCH_SIZE = 500  # Default is 1000
```

### Performance Issues
**Problem:** Slow search performance
**Solution:** Enable memory mapping in ChromaDB:
```python
client = chromadb.Client(Settings(
    chroma_db_impl="duckdb+parquet",
    persist_directory="./chroma_db",
    anonymized_telemetry=False
))
```

### Import Errors
**Problem:** ModuleNotFoundError for ChromaDB or other packages
**Solution:** Reinstall requirements with:
```bash
pip install --force-reinstall -r requirements.txt
```

## Conclusion

You now have a powerful semantic search system for your browser history! This setup demonstrates the practical application of embeddings and vector search, allowing you to find relevant pages based on meaning rather than just keywords.

Consider periodically re-running the embedding process to keep your searchable database current with your latest browsing history.

## References

- [ChromaDB Documentation](https://docs.trychroma.com/)
- [SentenceTransformers Documentation](https://www.sbert.net/)
- [Azure OpenAI Service](https://learn.microsoft.com/en-us/azure/cognitive-services/openai/)
- [Project Repository](https://github.com/nkkko/history)
