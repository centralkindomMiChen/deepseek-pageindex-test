# Developer Guide

This guide provides instructions for developers who want to work on the DeepSeek PageIndex RAG Test project.

## Getting Started

### 1. Environment Setup

To set up your development environment, follow these steps:

1.  **Clone the repository**:
    ```bash
    git clone https://github.com/centralkindomMiChen/deepseek-pageindex-test.git
    cd deepseek-pageindex-test
    ```

2.  **Create a virtual environment**:
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    ```

3.  **Install dependencies**:
    ```bash
    pip install -r requirements.txt
    ```

### 2. Configuration

The application requires API keys and other configuration settings to be set up correctly.

**Important**: API keys are currently hardcoded in `RAG_Backend.py` and `pgui.py`. For security and flexibility, it is **highly recommended** to move these to a central configuration file (e.g., `config.json` or a `.env` file) and load them at runtime.

#### a. RAG Backend (`RAG_Backend.py`)

You will need to set the following constants:

-   `API_KEY`: Your API key for the DeepSeek, Rerank, and Embedding APIs.
-   `EMBEDDING_API_URL`: The URL for the embedding API.
-   `RERANK_API_URL`: The URL for the rerank API.
-   `DEEPSEEK_API_URL`: The URL for the DeepSeek chat completion API.

#### b. GUI (`pgui.py`)

The `VECTOR_GEN_SCRIPT` embedded in this file also contains a hardcoded `API_KEY` and `BASE_URL`. These should be updated to match the values in the RAG backend.

## Architectural Overview

The system is composed of three main components that work together to create a full RAG pipeline.

### 1. Data Preparation (`pgui.py`)

-   This is the main entry point for the data pipeline.
-   It uses a `WorkerThread` to run the PDF parsing and vectorization processes in the background, which prevents the GUI from freezing.
-   The PDF parsing is handled by an external script, `run_pageindex.py`, which is called as a subprocess.
-   The vectorization is handled by an embedded script, `VECTOR_GEN_SCRIPT`, which is also run as a subprocess. This script takes the structured JSON from the parsing step and generates semantic embeddings for each node.

### 2. RAG Backend (`RAG_Backend.py`)

-   This is the core of the retrieval and generation system.
-   It's designed to be run in a thread, making it suitable for integration into a Q&A interface.
-   The `RecallWorker` class orchestrates the entire RAG pipeline:
    1.  **Query Rewriting**: The initial query is rewritten by an LLM to be more descriptive.
    2.  **Hybrid Retrieval**: It performs both a vector search (using a SQLite database) and a keyword search (on the PageIndex JSON).
    3.  **Reciprocal Rank Fusion (RRF)**: The results from the two search methods are merged.
    4.  **Reranking**: The merged results are reranked using a dedicated reranker model.
    5.  **Answer Generation**: The top-ranked results are passed to an LLM to generate a final answer.

### 3. Knowledge Recall UI (`pgirecallwindow.py`)

-   This is a standalone tool for exploring the PageIndex JSON files.
-   It's a useful utility for debugging the data preparation process and for manually inspecting the structured data.
-   It provides features for searching, viewing, and exporting the data.

## How to Extend the Project

-   **Adding a Q&A Interface**: The `RAG_Backend.py` is designed to be used in a separate thread. You could create a new PyQt5 window with a chat-like interface that uses the `RecallWorker` to answer user questions.
-   **Supporting More Document Types**: The PDF parsing is handled by an external script. You could add support for other document types (e.g., DOCX, HTML) by creating new parsing scripts and adding them as options in the `pgui.py` application.
-   **Improving Configuration Management**: Refactor the code to load API keys and other settings from a central configuration file. This would make the application more secure and easier to configure.
