# 🚀 Eternal Contextual RAG

> **Advanced RAG system combining Contextual Retrieval, Hybrid Search, and Web Grounding for superior accuracy**

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1TCHRVvtsu2LaZke2JPBtBba5qWyYRSD-?usp=sharing)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## 🌟 What Makes This Different?

Traditional RAG systems struggle with retrieval accuracy, especially when chunks lack context or don't contain exact keywords. **Eternal Contextual RAG** solves this with three breakthrough innovations:

### 1️⃣ **Contextual Retrieval** 
Instead of embedding isolated chunks, we use LLMs to generate contextual descriptions that explain *where each chunk fits* in the document. This dramatically improves retrieval accuracy.

**Example:**

- **Traditional Chunk:** "Revenue increased by 23% reaching $4.2M in September."
- **Contextualized Chunk:**:"This chunk from the 2024 Q3 Financial Report presents key performance metrics for September. It shows that the company achieved significant growth with a 23% revenue increase to $4.2 million, indicating strong quarterly performance and potential market expansion during the third quarter of fiscal year 2024."


### 2️⃣ **Hybrid Search (Vector + BM25)**
Combines semantic similarity (vector search) with keyword matching (BM25) using **Elasticsearch**, ensuring we catch both conceptual matches and exact terms.

### 3️⃣ **Web Search Grounding**
When confidence is low, the system automatically:
- Searches the web using Gemini's grounding capabilities
- Extracts and contextualizes new information  
- Expands the knowledge base dynamically
- Re-searches with enhanced knowledge

## 🏗️ Architecture Highlights
```
Documents → Smart Chunking → Context Generation → Embeddings
                                    ↓
User Query → Hybrid Search (ES) → Cohere Rerank → Answer
                                    ↓
                            Low Confidence?
                                    ↓
                            Web Search → Index → Re-search
```

## ✨ Key Features

- **📚 Intelligent Chunking**: Sentence-aware, ~800 tokens with 100-token overlap
- **🧠 Context-Aware Embeddings**: Gemini 2.5 Flash generates chunk context
- **🔍 Hybrid Retrieval**: Elasticsearch kNN + BM25 for best-of-both-worlds
- **📊 Cohere Reranking**: Ultra-precise relevance scoring
- **🌐 Automatic Knowledge Expansion**: Web grounding when needed
- **⚡ Production-Ready**: Error handling, retry logic, progress tracking

## 🛠️ Tech Stack

| Component | Technology |
|-----------|------------|
| **LLM** | Gemini 2.5 Flash (context + generation) |
| **Embeddings** | Gemini text-embedding-004 (768D) |
| **Vector DB** | Elasticsearch Cloud (Hybrid) |
| **Reranking** | Cohere Rerank v4 |
| **Web Search** | Gemini Grounding API |



## 🚀 Quick Start

### Prerequisites
```bash
# API Keys needed:
- Google Gemini API (free tier available)
- Elasticsearch Cloud (14-day trial)
- Cohere API (free tier available)
```

### Installation
Open the Colab notebook and add your API keys to Secrets:
1. Click 🔑 icon in left sidebar
2. Add: `GOOGLE_API_KEY`, `ELASTIC_API_KEY`, `Cohre_API`

### Basic Usage
```python
# 1. Load your documents
documents = [
    {
        "name": "My Document",
        "content": "Your document text here..."
    }
]

# 2. Build pipeline
pipeline = build_contextual_rag_pipeline(
    es_client,
    "my_index",
    documents
)

# 3. Query
result = query_pipeline(
    es_client,
    "my_index",
    "Your question here?",
    use_reranking=True,
    use_web_search_fallback=True
)

print(result["answer"])
```

## 📁 Project Structure
```
Eternal_Contextual_RAG/
│
├── Document Processing
│   ├── PDF/Text Loaders
│   ├── Smart Chunking (sentence-aware)
│   └── Token Counting
│
├── Context Enhancement
│   ├── Gemini Context Generation
│   └── Chunk Contextualization
│
├── Embedding & Indexing
│   ├── Gemini Embeddings
│   └── Elasticsearch Hybrid Index
│
├── Query Pipeline
│   ├── Hybrid Search (Vector + BM25)
│   ├── Cohere Reranking
│   └── Answer Generation
│
└── Knowledge Expansion
    ├── Web Search Detection
    ├── Gemini Grounding
    └── Dynamic Re-indexing
```

## 🎯 Use Cases

- **📖 Educational Q&A**: NCERT textbooks, course materials
- **📄 Document Analysis**: Research papers, reports, manuals
- **💼 Enterprise Knowledge Base**: Company docs, policies, wikis
- **🔬 Research Assistant**: Literature review, citation finding
- **📚 Personal Knowledge Management**: Notes, journals, articles

## 🔧 Configuration I used
```python
# Core Settings
INDEX_NAME = "contextual_rag_index"
EMBEDDING_DIMENSION = 768
CHUNK_SIZE = 800
CHUNK_OVERLAP = 100

# Pipeline Tuning
KNN_WEIGHT = 0.6          # Vector search weight
BM25_WEIGHT = 0.4         # Keyword search weight
RERANK_TOP_N = 10         # Results to rerank
MIN_CONFIDENCE = 0.65     # Web search threshold
```



## 🤝 Contributing

Contributions welcome! Areas for enhancement:
- Multimodal support (images, tables)
- OR ...

## 📝 License

MIT License - feel free to use in your projects!

## 🙏 Acknowledgments

This implementation is inspired by the work on **Contextual Retrieval** by Anthropic team:


Their research paper demonstrated how simple context prepending can reduce retrieval failures by 49% (67% with reranking). This project extends their ideas with:
- Hybrid search integration
- Dynamic web grounding
- Production-ready architecture

Read the original article: [Introducing Contextual Retrieval - Anthropic](https://www.anthropic.com/news/contextual-retrieval)



---

⭐ If this project helps your work, consider giving it a star!
```
