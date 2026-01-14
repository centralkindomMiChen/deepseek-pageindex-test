# Software Requirements Specification (SRS)

## 1. Introduction

### 1.1 Purpose

This document provides a detailed description of the requirements for the DeepSeek PageIndex RAG Test project. Its purpose is to define the scope, features, and behavior of the system, serving as a guide for development and testing.

### 1.2 Scope

The project is a Retrieval-Augmented Generation (RAG) system designed for industrial document processing. The system will provide a graphical user interface (GUI) for users to:
-   Process PDF documents into a structured JSON format.
-   Generate vector embeddings for the processed content.
-   Perform advanced hybrid searches to answer user queries.
-   Explore and export the processed data.

The system is intended for users who need to extract and query information from large, complex documents.

## 2. Overall Description

### 2.1 Product Perspective

The system is a standalone desktop application composed of three main components: a data preparation GUI, a RAG backend, and a data exploration tool. It is designed to be a self-contained solution for building and querying a knowledge base from PDF documents.

### 2.2 Product Features

-   **PDF Processing**: The system will be able to parse PDF documents and convert them into a structured JSON format.
-   **Vectorization**: The system will generate vector embeddings for the content of the processed documents.
-   **Hybrid Search**: The system will provide a hybrid search engine that combines vector search and keyword search.
-   **Query Rewriting**: The system will use a Large Language Model (LLM) to rewrite user queries for better search results.
-   **Reranking**: The system will rerank search results to improve relevance.
-   **Answer Generation**: The system will use an LLM to generate answers based on the search results.
-   **Data Exploration**: The system will provide a tool for users to manually explore and search the processed data.
-   **Data Export**: The system will allow users to export the processed data to various formats (DOCX, TXT, CSV, XLSX).

## 3. Specific Requirements

### 3.1 Functional Requirements

#### 3.1.1 Data Preparation GUI (`pgui.py`)

-   The user shall be able to select a PDF file from their local file system.
-   The user shall be able to choose an AI model for processing.
-   The user shall be able to start and stop the PDF parsing and vectorization processes.
-   The system shall display real-time logs of the processing status.

#### 3.1.2 RAG Backend (`RAG_Backend.py`)

-   The system shall accept a user query as input.
-   The system shall rewrite the query using an LLM.
-   The system shall perform a hybrid search using both vector and keyword search.
-   The system shall merge the search results using the Reciprocal Rank Fusion (RRF) algorithm.
-   The system shall rerank the merged results.
-   The system shall generate an answer based on the top-ranked results using an LLM.

#### 3.1.3 Knowledge Recall UI (`pgirecallwindow.py`)

-   The user shall be able to load a processed JSON file.
-   The user shall be able to search for keywords across all content in the file.
-   The user shall be able to view the details of each section of the document.
-   The user shall be able to export the data to DOCX, TXT, CSV, or XLSX format.

### 3.2 Non-Functional Requirements

-   **Usability**: The GUI shall be intuitive and easy to use for non-technical users.
-   **Performance**: The GUI shall remain responsive during long-running processes. The RAG backend should provide answers in a timely manner.
-   **Security**: API keys and other sensitive information should not be stored in plain text in the source code.
-   **Extensibility**: The system should be designed in a modular way to allow for future extensions, such as supporting new document types or search algorithms.
