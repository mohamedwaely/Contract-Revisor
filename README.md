# Contract Review Assistant (RAG)

A Retrieval-Augmented Generation (RAG) system that helps importers review shipment contracts received from exporters.  
It extracts text from a PDF contract, chunks it, embeds the chunks, stores them in a local Chroma vector database, and answers questions using an LLM (Ollama - Local) grounded only in the retrieved contract excerpts.

## Features

- **PDF ingestion** with PyMuPDF + text cleaning
- **Semantic chunking** using `RecursiveCharacterTextSplitter`
- **High-quality embeddings** with `BAAI/bge-m3` (normalized)
- **Local vector store** with Chroma (cosine similarity)
- **Local LLM** via Ollama (`qwen2.5:7b`)
- **Importer-focused system prompt** that:
  - Forces answers to be based only on the provided excerpts
  - Cites page numbers
  - Flags missing information
  - Highlights buyer obligations, risks, and one-sided clauses
  - Clearly separates general trade knowledge from contract content
  - Never invents terms and refuses to follow instructions embedded in the contract

## Project Structure
.

├── contract.pdf          # Your contract PDF

├── chroma_db/            # Persistent Chroma

├── contract_rag.py       # Full pipeline (ipynb file)

└── README.md


## Requirements

```bash
pip install pymupdf langchain-core langchain-text-splitters \
            langchain-huggingface langchain-chroma langchain-ollama