# Uzbek Knowledge Base RAG System

A Retrieval-Augmented Generation (RAG) system for answering questions over an Uzbek-language knowledge base. The system combines multilingual dense embeddings, vector search, and a fast open-weight LLM to deliver accurate, context-grounded answers in Uzbek.

## Features

- **Multilingual semantic search** using `intfloat/multilingual-e5-large-instruct` embeddings, tuned for accurate retrieval in Uzbek text
- **Vector storage & retrieval** powered by ChromaDB
- **Fast LLM inference** via Groq's `llama-3.3-70b-versatile`
- **REST API** built with FastAPI for easy integration
- **Conversation history support** for multi-turn, context-aware dialogue
- **Containerized deployment** with Docker for consistent, portable setup

## Tech Stack

| Component | Technology |
|---|---|
| Embeddings | `intfloat/multilingual-e5-large-instruct` |
| Vector DB | ChromaDB |
| LLM | Groq (`llama-3.3-70b-versatile`) |
| Backend | FastAPI |
| Deployment | Docker |

## Architecture

```
User Query (Uzbek)
      │
      ▼
Embedding Model (multilingual-e5-large-instruct)
      │
      ▼
ChromaDB Vector Search  ──► Top-K relevant chunks
      │
      ▼
Groq LLM (llama-3.3-70b-versatile)
      │
      ▼
Context-grounded Answer
```

## Getting Started

### Prerequisites

- Python 3.10+
- Docker (optional, for containerized run)
- A Groq API key ([console.groq.com](https://console.groq.com))

### Installation

1. Clone the repository
   ```bash
   git clone https://github.com/YOUR_USERNAME/YOUR_REPO.git
   cd YOUR_REPO
   ```

2. Create a virtual environment and install dependencies
   ```bash
   python -m venv venv
   source venv/bin/activate   # on Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```

3. Configure environment variables
   ```bash
   cp .env.example .env
   ```
   Then open `.env` and add your Groq API key:
   ```
   GROQ_API_KEY=your_api_key_here
   ```

### Running Locally

```bash
uvicorn main:app --reload
```

The API will be available at `http://localhost:8000`.

### Running with Docker

```bash
docker build -t uzbek-rag .
docker run -p 8000:8000 --env-file .env uzbek-rag
```

## Usage

Send a query to the API endpoint:

```bash
curl -X POST http://localhost:8000/query \
  -H "Content-Type: application/json" \
  -d '{"question": "Savolingiz shu yerda"}'
```

The system will retrieve relevant context chunks from the knowledge base and generate a grounded answer using the LLM.

## Project Structure

```
.
├── app/                # Core application code (embedding, retrieval, generation)
├── data/               # Source documents / knowledge base
├── chroma_db/          # Vector store (gitignored)
├── Dockerfile
├── .dockerignore
├── .gitignore
├── .env.example
├── requirements.txt
└── README.md
```

## Roadmap

- [ ] Add evaluation metrics for retrieval quality
- [ ] Support additional document formats
- [ ] Add streaming responses
- [ ] Deploy to a cloud platform

## License

This project is open source and available under the [MIT License](LICENSE).

## Author

Built by Odilbek Baxtiyarov as part of an ongoing portfolio of applied ML/AI projects.