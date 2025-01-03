# PDF-Extractor
This repository provides a Python-based implementation of a conversational assistant powered by Pinecone's vector database, Sentence Transformers, and the Groq LLM model. The assistant utilizes Thai recipe data for hybrid search and response generation.

## Features

- **Vector Search with Pinecone:** Efficient and scalable hybrid search using Pinecone's serverless vector database.
- **PDF Knowledge Base:** Extracts information from a PDF containing Thai recipes.
- **Custom Embedding Models:** Leverages Sentence Transformers for embeddings.
- **Conversational Agent:** Implements a conversational loop using the Groq LLM model.

---

## Prerequisites

1. Python 3.8+
2. Required libraries (listed in `requirements.txt`):
    - `typer`
    - `rich`
    - `phi`
    - `dotenv`
    - `pinecone`
    - `sentence-transformers`
3. A valid Pinecone API Key.
4. A valid GROQ LLM API Key.
5. A valid phi-data API Key.
6. PDF URL access permissions.

---

## Setup and Installation

1. **Clone the Repository**

   ```bash
   git clone https://github.com/your-username/PDF-Extractor.git
   cd PDF-Extractor
   ```

2. **Install Dependencies**

   Use `pip` to install the required dependencies:

   ```bash
   pip install -r requirements.txt
   ```

3. **Environment Variables**

   Create a `.env` file in the root directory and add the Pinecone API Key,GROQ API key and PHI-Data API KEY:

   ```env
   PINECONE_API_KEY=<Your-Pinecone-API-Key>
   GROQ_API_KEY=<Your-GROQ-API-Key>
   PHI_DATA_KEY=<Your-PHI-DATA-Key>
   ```

4. **PDF Data Source**

   Ensure the PDF is accessible at `https://phi-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf`. Replace the URL in the script if using a different source.

---

## How to Run

1. **Load the Knowledge Base**

   Uncomment the following line in the script for the first run to load and upsert data to the vector database:

   ```python
   # knowledge_base.load(recreate=True, upsert=True)
   ```

   After the initial run, comment it back to avoid reloading.

2. **Start the Assistant**

   Run the assistant using the command below:

   ```bash
   python main.py
   ```

3. **Interact with the Assistant**

   Once the script starts, type your queries (e.g., "What is a good Thai curry recipe?"). To exit the session, type `exit` or `bye`.

---

## Code Overview

### Components

- **`PineconeDB`**
  - Configures Pinecone with hybrid search enabled.
  - Uses a Sentence Transformer embedder for high-quality text embeddings.

- **`PDFUrlKnowledgeBase`**
  - Loads Thai recipes from a PDF file and stores vectors in Pinecone.

- **`Agent`**
  - Handles conversational interactions using the Groq LLM model.

### Why We Chose These Libraries

1. **Pinecone**
   - Pinecone offers a robust, scalable vector database that supports hybrid search.
   - It provides serverless functionality, eliminating the need for complex infrastructure management.
   - Hybrid search capability combines vector and keyword searches, improving response relevance.

2. **Sentence Transformers**
   - This library enables efficient generation of dense vector embeddings.
   - It supports pre-trained models optimized for semantic similarity tasks.
   - Sentence Transformers integrate seamlessly with Pinecone, ensuring high-quality search results.

3. **`phi` Library**
   - Provides integration with LLM models like Groq.
   - Simplifies the management of knowledge bases and conversational agents.

4. **Rich and Typer**
   - `rich`: Enhances the terminal interface with styled text and prompts.
   - `typer`: Simplifies command-line interface creation for Python scripts.

5. **dotenv**
   - Enables secure management of sensitive environment variables like API keys.

### Workflow

1. **PDF Loading and Vectorization**
   - The `PDFUrlKnowledgeBase` downloads and parses the Thai recipes PDF.
   - Each recipe is converted into vector embeddings using Sentence Transformers.

2. **Hybrid Search Indexing**
   - Pinecone stores these embeddings and indexes them for hybrid search.
   - Keyword and vector-based queries are balanced using the `hybrid_alpha` parameter.

3. **Conversational Interaction**
   - The `Agent` handles user input and queries Pinecone for relevant recipes or information.
   - The Groq LLM processes the results and generates human-readable responses.

4. **User Feedback Loop**
   - The assistant remains in a conversational loop, continuously processing user queries until exited.

---

## Troubleshooting

- **Issue: Pinecone Authentication Errors**
  - Ensure the correct API key is added to `.env`.

- **Issue: Missing Dependencies**
  - Re-run `pip install -r requirements.txt`.

- **Issue: PDF Not Accessible**
  - Verify the PDF URL or replace it with a valid one.

---
