# RAG Question Answering API

This project implements a Retrieval-Augmented Generation (RAG) Question Answering system using **FastAPI**, **Langchain**, **FAISS**, and **Groq LLM**. It allows users to query a knowledge base built from various document formats (PDF, TXT, CSV, Excel, Word, JSON).

## 🚀 Features

-   **Semantic Search**: Uses `all-MiniLM-L6-v2` via `SentenceTransformers` for high-quality embeddings.
-   **Fast Vector Store**: Utilizes **FAISS** for efficient similarity search.
-   **LLM Integration**: powered by **Groq** (Llama 3 model) for generating concise summaries and answers.
-   **Multi-format Support**: Ingests documents from:
    -   PDF (`.pdf`)
    -   Text (`.txt`)
    -   CSV (`.csv`)
    -   Excel (`.xlsx`)
    -   Word (`.docx`)
    -   JSON (`.json`)
-   **API First**: Built with **FastAPI** for easy integration and deployment.

## 🛠️ Tech Stack

-   **Python 3.x**
-   **FastAPI** & **Uvicorn** (Web Framework)
-   **Langchain** (Orchestration)
-   **FAISS** (Vector Database)
-   **SentenceTransformers** (Embeddings)
-   **Groq** (LLM Provider)

## 📋 Prerequisites

-   Python 3.9+ installed.
-   A [Groq API Key](https://console.groq.com/).

## 📦 Installation

1.  **Clone the repository:**
    ```bash
    git clone <repository-url>
    cd Langchain-Model
    ```

2.  **Create and activate a virtual environment (optional but recommended):**
    ```bash
    python -m venv venv
    # Windows
    venv\Scripts\activate
    # macOS/Linux
    source venv/bin/activate
    ```

3.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

## ⚙️ Configuration

1.  Create a `.env` file in the root directory.
2.  Add your Groq API key:

    ```env
    GROQ_API_KEY=your_groq_api_key_here
    ```

## 🏃 Usage
### 1. Document Ingestion (Automatic)
By default, if the vector store (`faiss_store/`) does not exist, the application will attempt to load documents from a `data/` directory in the root folder when the API starts.
*   Create a `data` folder in the root directory.
*   Place your documents (PDF, TXT, etc.) inside.

### 2. Running the API Server
Start the FastAPI server:
```bash
CD
```
The API will be available at `http://localhost:8000`.

### 3. API Documentation
Visit `http://localhost:8000/docs` to interact with the API using the Swagger UI.

### 4. Querying the API
**Endpoint:** `POST /query`

**Payload:**
```json
{
  "query": "What is Database Management System?",
  "top_k": 3
}
```

**Response:**
```json
{
  "query": "What is Database Management System?",
  "answer": "A Database Management System (DBMS) is..."
}
```

### 5. CLI Usage (Optional)
You can directly test the pipeline using `main.py`. Note that `main.py` is configured to look for documents in `Research/data/pdf` and save the index to `faiss_Store`.
```bash
python main.py
```

## 📂 Project Structure

```
Langchain-Model/
├── app.py                 # FastAPI Application entry point
├── main.py                # CLI script for testing/building pipeline
├── requirements.txt       # Project dependencies
├── .env                   # Environment variables (Groq API Key)
├── src/
│   ├── data_loader.py     # Logic to load PDF, TXT, CSV, etc.
│   ├── embedding.py       # Embedding generation pipeline
│   ├── vectorstore.py     # FAISS vector store management
│   └── search.py          # RAG Search logic (retrieval + summarization)
├── faiss_store/           # Generated Vector Store (Faiss index + metadata)
└── data/                  # (Create this) Directory for source documents
```