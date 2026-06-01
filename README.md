# 🇺🇿 Uzbek Language RAG System

A question-answering system for Uzbek language documents.

## Stack
- **LLM:** Groq — llama-3.3-70b (free)
- **Embedding:** multilingual-e5-large (local, free)
- **Vector DB:** ChromaDB (local, free)
- **PDF reading:** PyMuPDF

## Installation

```bash
pip install groq chromadb sentence-transformers pymupdf
```

## Getting API Key

1. Go to [console.groq.com](https://console.groq.com)
2. Sign up (free)
3. Create a new key under API Keys section
4. Replace `YOUR_GROQ_API_KEY_HERE` in the notebook

## Usage

```python
# Load TXT file
add_document("file.txt")

# Load PDF book
add_pdf("book.pdf")

# Ask a question
answer = ask("What is the main idea of the book?")
print(answer)
```

## Supported File Formats

| Format | Status | Note |
|--------|--------|------|
| TXT | ✅ | Must be UTF-8 encoded |
| MD | ✅ | Markdown files |
| PDF | ✅ | Text-based PDF only |

## Configuration

| Parameter | Default | Description |
|-----------|---------|-------------|
| CHUNK_SIZE | 500 | Chunk size in characters |
| CHUNK_OVERLAP | 50 | Overlap between chunks |
| TOP_K | 3 | Number of chunks to retrieve |

## Architecture

```
Document (PDF/TXT)
      │
      ▼
  chunk_text()  ──→  500-character chunks
      │
      ▼
  embedder.encode()  ──→  Vectors
      │
      ▼
  ChromaDB  ──→  Stored
      │
  [When a question is asked]
      │
      ▼
  search()  ──→  Top 3 relevant chunks
      │
      ▼
  Groq API  ──→  Answer in Uzbek
```