# UI Panel Generator with RAG

## Overview
This project implements a Retrieval-Augmented Generation (RAG) pipeline for UI panel generation and design assistance. The system uses Google Gemini for content generation, LangChain for orchestration, HuggingFace embeddings for semantic vectorization, and FAISS for similarity search over local HTML component snippets.

The goal is to enable users to generate complete HTML layouts or get UI-related answers based on a small library of reusable HTML components.

---

## Features
- Panel generation: create complete HTML pages using existing component snippets.  
- UI question answering: retrieve relevant components and provide contextual responses.  
- Intent classification: distinguish between panel generation, UI-related questions, and irrelevant queries.  
- Retrieval-Augmented Generation (RAG): ensures that generated output is grounded in available components.  

---

## Architecture
1. Local HTML files are read and stored as LangChain `Document` objects.  
2. Each document is converted into embeddings using HuggingFace `sentence-transformers/all-MiniLM-L6-v2`.  
3. The embeddings are stored in a FAISS vector database for similarity search.  
4. User input is classified into three categories:  
   - Panel generation  
   - UI-related question  
   - Irrelevant query  
5. For panel generation, the top-k most relevant snippets are retrieved and passed to Gemini along with the user prompt.  
6. For questions, retrieved snippets are used as context for Gemini’s answer generation.  
7. The system runs as a simple command-line chatbot loop.  

---

## Tech Stack
- Google Generative AI (Gemini-2.5-Pro) – for content generation  
- LangChain – document abstraction, embeddings, and vector store integration  
- HuggingFace Sentence Transformers – embeddings model (`all-MiniLM-L6-v2`)  
- FAISS (Facebook AI Similarity Search) – similarity search over embeddings  
- Python 3.9+  

---

## Installation

Clone the repository and install dependencies:

```bash
pip install google-generativeai
pip install langchain_community
pip install faiss-cpu
pip install sentence-transformers
```

---

## Configuration

Set up your Gemini API key in your script:

```python
import google.generativeai as genai
genai.configure(api_key="AIzaSyCrffA_YtD8H8ak4nm4jfpUUkDLAkbixWs")
```


## Usage

1. Place your HTML component snippets in the same directory (e.g., `b.html`, `c.html`, `t.html`).  
2. Run the script.  
3. Enter your prompt in the terminal when asked.

Example:

```
💬 You: generate a login panel with username and password fields
🤖 Bot: Panel generated
```

The generated HTML is saved in `panel.html`.

---

## Future Improvements
- Replace rule-based intent classification with an ML-based model  
- Add support for larger and dynamic component libraries  
- Build a web-based frontend for more intuitive interaction  
- Support additional vector stores like Pinecone or Weaviate  
- Add evaluation metrics for measuring retrieval and generation quality
