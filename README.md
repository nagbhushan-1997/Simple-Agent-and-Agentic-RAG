# Simple Agent and Agentic RAG Example

## Overview

This repository demonstrates the transition from a **Simple Tool-Using Agent** to a **full Agentic RAG (Retrieval-Augmented Generation) system** using **LangChain**, **LangGraph**, **ChromaDB**, and **Mistral LLMs**.

The project illustrates:
- How agents can invoke tools instead of solving tasks directly
- How retrieval and structured memory enable **Agentic behavior**
- How multi-turn, multi-user conversations are handled using thread-based memory

---

## Key Concepts Demonstrated

- Tool-based agents (function calling)
- Agent reasoning constrained strictly to tools
- Retrieval-Augmented Generation (RAG)
- Agentic RAG using LangGraph
- Conversation memory with multiple users
- Streaming agent responses

---

## Repository Structure

```text
simple-agentic-rag/
├── README.md
├── simple_agent_and_agentic_rag_example.py
├── requirements.txt
└── data/
    ├── Laptop pricing.csv
    └── Laptop product descriptions.pdf

```

## Technology Stack

| Component            | Technology                     |
|----------------------|--------------------------------|
| LLM                  | Mistral (mistral-large-latest) |
| Agent Framework      | LangChain                      |
| Agent Orchestration  | LangGraph                      |
| Embeddings           | Mistral Embeddings             |
| Vector Store         | ChromaDB                       |
| Document Loader      | PyPDF                          |
| Language             | Python 3.10+                   |


## API Key Setup

This project uses the **Mistral API**.

### Google Colab
```python
from google.colab import userdata
mistral_api_key = userdata.get("Mistral_API")
```

## Part 1: Simple Tool-Based Agent

### Tools Defined
- `find_sum(x, y)` – returns the sum of two integers  
- `find_product(x, y)` – returns the product of two integers  

### Agent Behavior
- The agent does **not** solve math problems directly  
- It must use tools to produce results  
- Behavior is enforced using a strict system prompt  

### Example Capabilities
- Single-step tool invocation  
- Multi-step reasoning using tools  
- Step-by-step execution trace inspection  

---

## Part 2: Agentic RAG – Product Question Answering Agent

### Data Sources
- **Laptop pricing CSV** – structured data  
- **Laptop product description PDF** – unstructured data  

---

## RAG Pipeline

### Document Ingestion
- PDFs loaded using `PyPDFLoader`  
- Chunked using `RecursiveCharacterTextSplitter`  
- Embedded using Mistral embeddings  
- Stored in ChromaDB  

### Retrieval
- Semantic search over product descriptions  
- Retrieval exposed as a tool  

---

## Agentic Tools

| Tool Name              | Purpose |
|------------------------|---------|
| `get_laptop_price`     | Returns laptop price from CSV |
| `get_product_features` | Retrieves product features using vector search |

---

## Agentic RAG Architecture

### Agent Characteristics
- Uses **only tools**, not internal knowledge  
- Maintains conversational memory  
- Supports multi-turn and multi-user conversations  
- Uses LangGraph memory checkpointing  

### Memory Handling
- Each user session uses a unique `thread_id`  
- Multiple conversations are handled independently  
- Context is preserved across turns  

---

## Example Interactions

### Product Queries
- “What are the features and pricing for GammaAir?”  
- “Tell me about the features of SpectraBook”  
- “What is its price?”  

### Conversational Flow
- Greetings and small talk  
- Product discovery  
- Feature comparison  
- Pricing queries  
- Session-specific memory retention  

---

## Multi-User Conversation Support

- Multiple users interact simultaneously  
- Each user maintains isolated memory  
- Demonstrated using separate thread IDs  

