# User Manual

This manual provides step-by-step instructions for using the DeepSeek PageIndex RAG Test application. The system is divided into two main tools:

1.  **PageIndex Pro (pgui.py)**: For processing PDFs and creating vectorized RAG databases.
2.  **Knowledge Recall Center (pgirecallwindow.py)**: For exploring and searching the structured JSON data.

## Part 1: Processing PDFs with PageIndex Pro

PageIndex Pro is the main application for preparing your documents for the RAG system.

### Step 1: Launch the Application

Run `pgui.py` to launch the PageIndex Pro application. You will be presented with a tabbed interface.

### Step 2: PDF Parsing (PageIndex Tab)

This tab is for converting your PDF documents into a structured JSON format.

1.  **Load a PDF**: Click the "LOAD PDF" button to select the PDF document you want to process.
2.  **Select an AI Model**: Choose the AI model you want to use for generating summaries and other metadata.
3.  **Choose a Schema**: Select a processing schema. "Full Intelligence" is recommended for the best results, but it is the slowest.
4.  **Start Indexing**: Click the "START INDEXING" button to begin the parsing process. You can monitor the progress in the "SYSTEM KERNEL LOGS" window.
5.  **Output**: Once the process is complete, a structured JSON file will be created in the same directory as the PDF. This file is the "PageIndex" and will be used in the next step.

### Step 3: RAG Vectorization (RAG Vectorization Tab)

This tab is for converting the structured JSON into a vectorized database that the RAG system can use.

1.  **Select JSON**: Click the "SELECT JSON" button to choose the PageIndex JSON file you created in the previous step.
2.  **Set Output**: The output path for the vectorized data will be automatically generated. You can change it by clicking the "SET OUTPUT" button.
3.  **Select a Summarizer Model**: Choose the AI model to use for generating the semantic vectors (embeddings).
4.  **Choose a Strategy**:
    -   **Data Lossless**: The original text is preserved along with the AI-generated summary. Good for tables and schedules.
    -   **Semantic Summary**: Only the AI-generated summary is used. Good for policy documents.
    -   **Hybrid**: A mix of the two.
5.  **Generate Vectors**: Click the "GENERATE VECTORS" button to start the vectorization process. This may take a significant amount of time, depending on the size of the document.
6.  **Output**: This will create a SQLite database file containing the vectorized data, ready to be used by the RAG backend.

## Part 2: Exploring Data with the Knowledge Recall Center

The Knowledge Recall Center is a separate tool for exploring the PageIndex JSON files.

### Step 1: Launch the Application

Run `pgirecallwindow.py` to launch the Knowledge Recall Center.

### Step 2: Load a JSON File

1.  Click the "LOAD INDEX JSON" button to select a PageIndex JSON file.
2.  The application will load the file and display all the "nodes" (sections of the document) in the left-hand list.

### Step 3: Search and Explore

-   **Global Search**: Use the search bar at the top of the window to search for keywords across all nodes in the document.
-   **View Node Details**: Click on any node in the left-hand list to see its details in the right-hand pane. This includes the title, page numbers, AI-generated summary, and the full text of the section.
-   **In-Text Search**: When viewing a node's details, you can use the "In-text search" bar to highlight keywords within that specific section.

### Step 4: Export Data

You can export the entire content of the loaded JSON file to various formats:

1.  Select the desired format from the "Export format" dropdown menu (DOCX, TXT, CSV, or XLSX).
2.  Click the "EXPORT ALL NODES" button and choose a location to save the file.
