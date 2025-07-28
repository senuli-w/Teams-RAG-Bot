# RAG Q\&A Chatbot for Microsoft Teams

This project is a functional Question & Answering (Q\&A) chatbot integrated with Microsoft Teams. It uses a Retrieval-Augmented Generation (RAG) architecture to answer questions based on a custom knowledge base (e.g., a PDF document).

This was developed as a hands-on exercise for the "Charlie" engineering onboarding plan.

-----

## Key Features

  * **Answers Questions from a Custom Source:** Ingests and indexes a private document to provide answers based solely on that content.
  * **Modern AI Architecture:** Implements the RAG pattern to ground the language model, reducing hallucinations and improving factual accuracy.
  * **Microsoft Teams Integration:** Allows users to interact with the chatbot directly within their Teams environment using the Azure Bot Service.
  * **Built on Azure:** Leverages a suite of Azure AI services for a scalable and robust solution.

-----

## Technology Stack

  * **Orchestration:** LangChain
  * **LLM & Embeddings:** Azure OpenAI (`gpt-4.1-nano`, `text-embedding-3-small`)
  * **Retrieval:** Azure AI Search (Vector Search)
  * **Bot Framework:** Azure Bot Service
  * **Data Extraction & Chunking:** Unstructured.io
  * **Language:** Python / TypeScript

-----

## Architecture Overview

The project is divided into two main workflows: an offline **Ingestion Pipeline** and an online **Application Workflow**.

#### 1\. Ingestion Pipeline (Offline)

This process prepares the knowledge base. It uses the `unstructured` library to both partition the source document into elements and then intelligently chunk those elements based on their structure.

`PDF Document` -\> `Unstructured.io (Partition & Chunk)` -\> `Azure Embedding Model` -\> `Azure AI Search Index`

#### 2\. Application Workflow (Online)

This is the live request/response flow when a user asks a question.

`User in Teams` -\> `Azure Bot Service` -\> `Orchestrator API (LangChain)` -\> `Azure AI Search (Retrieve)` -\> `Azure OpenAI (Generate)` -\> `Response to User`

