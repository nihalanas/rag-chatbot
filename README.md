# RAG Chatbot

A Retrieval-Augmented Generation (RAG) chatbot that answers questions over your own documents. It ingests PDFs into a FAISS vector store, retrieves the most relevant passages at query time, and generates grounded answers with a local Llama 2 model — all behind a Chainlit web UI.

## Features

- **Document ingestion** — load and chunk PDFs from a local folder.
- **Vector search** — FAISS similarity search over sentence-transformer embeddings.
- **Grounded generation** — `RetrievalQA` chain with a customisable prompt that answers strictly from retrieved context.
- **Chat UI** — interactive web interface via Chainlit.

## Tech Stack

| Area | Tools |
|------|-------|
| Orchestration | LangChain |
| Vector store | FAISS |
| Embeddings | sentence-transformers (`all-MiniLM-L6-v2`) |
| LLM | Llama 2 (GGUF) via CTransformers |
| Interface | Chainlit |
| Language | Python |

## Getting Started

### Prerequisites
- Python 3.10+
- pip

### 1. Install dependencies

```bash
pip install -r requirements.txt
```

### 2. Add your documents

Place the PDFs you want the chatbot to answer from in a `data/` folder at the project root.

### 3. Build the vector store

```bash
python src/ingest.py
```

This chunks the documents, generates embeddings and saves a FAISS index to `vectorstore/db_faiss`.

### 4. Run the chatbot

```bash
chainlit run src/chatbot.py
```

## Customisation

- **Prompt** — edit `CUSTOM_PROMPT_TEMPLATE` in `src/chatbot.py` to steer the model's behaviour.
- **Model** — the default is `TheBloke/Llama-2-7B-Chat-GGUF`; swap the model reference in `src/chatbot.py` to use another GGUF model.

## License

Released under the [MIT License](LICENSE).
