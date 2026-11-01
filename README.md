# Meridian Securities — Stock Broker Intelligent System

## Project Overview

The Stock Broker Intelligent System is a Retrieval-Augmented Generation (RAG) application designed to answer financial research questions using retrieved information from SEC filings, market news, and historical price data.

The application combines semantic search, an AI language model, a Flask REST API, and an interactive Streamlit interface.

Developed as part of hands-on AI and machine learning training.

## Key Features

- AI-assisted financial document research
- Semantic search using FAISS
- Hugging Face embeddings for document retrieval
- GPT-4o-mini for answer generation
- Answers grounded in retrieved financial information
- Option to inspect supporting document passages
- Configurable retrieval and generation settings
- Separate Flask backend and Streamlit frontend
- Docker configuration for application deployment

## Technologies Used

- Python
- Flask
- Streamlit
- LangChain
- FAISS
- Hugging Face Embeddings (`BAAI/bge-base-en-v1.5`)
- OpenAI GPT-4o-mini
- Docker
- Requests

## Application Architecture

1. The user enters a financial research question in Streamlit.
2. Streamlit sends a JSON request to the Flask backend.
3. FAISS retrieves relevant passages from the saved financial document vector store.
4. The retrieved information is supplied to GPT-4o-mini with financial research instructions.
5. The backend returns the generated answer.
6. Streamlit displays the answer and optionally the supporting passages.

## API Endpoints

| Endpoint | Description |
|---|---|
| `GET /` | API welcome message |
| `POST /v1/relevant_chunks` | Retrieve relevant financial document passages |
| `POST /v1/answer` | Generate an answer |
| `POST /v1/answer_with_relevant_chunks` | Generate an answer with supporting passages |

## Streamlit User Interface

The interface includes:

- A financial research question field
- Retrieval count slider (1–10 chunks, default 4)
- Temperature slider (0.0–1.0, default 0.0)
- Maximum-token slider (64–2048, default 512)
- Answer only and Answer + Relevant Chunks response modes
- Expandable sections displaying retrieved passages
- Connection and error handling messages

## Financial Research Safeguards

The language model is instructed to:

- Use only information supported by retrieved documents
- Identify relevant companies, reporting periods, currencies, and units
- Avoid confusing fiscal years, quarters, or reporting dates
- Avoid inventing financial figures or market information
- Identify conflicting or insufficient evidence
- Avoid unsupported investment recommendations or price predictions

These instructions are intended to improve reliability but do not guarantee the accuracy of every generated answer.

## Example Research Questions

- What were Apple's total net sales in fiscal 2025?
- What were Amazon's AWS net sales in 2025?
- What information does a company's annual report provide about its financial performance?

Answers depend on the documents available in the vector store.

## Repository Structure

```text
stock-broker-intelligent-system/
├── backend/
│   ├── app.py
│   ├── rag_utils.py
│   ├── requirements.txt
│   ├── Dockerfile
│   └── faiss_index/
├── frontend/
│   ├── app.py
│   ├── requirements.txt
│   └── Dockerfile
└── README.md
```

## Configuration

The backend uses the following environment variables:

- `OPENAI_API_KEY`
- `OPENAI_API_BASE`

The frontend communicates with the backend at `http://localhost:7860`.

The saved FAISS index must come from a trusted source because loading it enables pickle deserialization.

## Project Purpose

This project demonstrates the integration of financial document retrieval, language models, REST API development, and an interactive web interface into a practical AI research application.

It is intended for informational research, not personalized investment advice.

## Author

Victor Marek II

GitHub: https://github.com/VicGL156
