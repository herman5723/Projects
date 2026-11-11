# Enterprise Multi-Document RAG Assistant

A beginner-friendly Retrieval-Augmented Generation (RAG) project that lets users ask questions about a collection of documents. It retrieves relevant passages from the uploaded files and uses Google Gemini to generate an answer grounded in those passages.

> **Learning project:** This repository demonstrates a basic RAG pipeline. It has not been benchmarked or security-reviewed for production deployment.

## Features

- Load multiple **PDF, DOCX, TXT, and CSV** files.
- Extract and clean document text.
- Split text into overlapping chunks.
- Generate local text embeddings with `sentence-transformers/all-MiniLM-L6-v2`.
- Store and search vectors with persistent ChromaDB.
- Retrieve the top 3 relevant chunks for a question.
- Generate document-grounded answers with Google Gemini.
- Display source labels and available page/row/paragraph metadata.
- Includes an abstention instruction when the retrieved context does not contain the answer.
- Built without **LangChain** or **LlamaIndex**.

## Architecture

```text
PDF / DOCX / TXT / CSV
          |
          v
   Text extraction
          |
          v
    Text cleaning
          |
          v
  Chunking + overlap
          |
          v
 MiniLM embeddings (local)
          |
          v
     ChromaDB
          |
          v
 Retrieve top 3 chunks
          |
          v
 Gemini answer generation
          |
          v
 Answer + source references
```

## Technology stack

- Python
- Jupyter Notebook / Google Colab
- Sentence Transformers (`all-MiniLM-L6-v2`)
- ChromaDB
- Google Gemini API (`google-genai`)
- pypdf, python-docx, pandas, NumPy

## Repository structure

```text
.
├── Beginner_Enterprise_Multi_Document_RAG_Assistant.ipynb
├── README.md
├── requirements.txt
├── .gitignore
└── LINKEDIN_POST.md
```

Create a `knowledge_base/` folder when running the notebook and add your own documents there. Do not commit confidential company documents, personal data, API keys, or the generated `chroma_db/` database.

## Getting started

### Option 1: Google Colab

1. Upload the notebook to Google Colab.
2. Create a folder named `knowledge_base` in the Colab session and upload sample documents (PDF, DOCX, TXT, or CSV).
3. Add your Gemini API key to Colab **Secrets** with the name `GEMINI_API_KEY` and enable notebook access to it.
4. Run notebook cells from top to bottom.
5. After indexing completes, go to the final RAG function section and run a question, for example:

```python
result = ask_rag("What is the employee leave policy?")
print(result["answer"])
```

The function also prints the retrieved sources. `result` contains the question, answer, and retrieved chunks.

### Option 2: Local Jupyter

1. Clone or download this repository.
2. Install Python dependencies:

```bash
python -m pip install -r requirements.txt
```

3. Create a `knowledge_base/` folder next to the notebook and add your documents.
4. Set your Gemini API key as an environment variable. For example, in macOS/Linux:

```bash
export GEMINI_API_KEY="your_api_key_here"
```

On Windows PowerShell:

```powershell
$env:GEMINI_API_KEY="your_api_key_here"
```

5. Start Jupyter, open the notebook, and run all cells in order.
6. Ask a question:

```python
result = ask_rag("How can I reset my password?")
print(result["answer"])
```

**Never hard-code or commit your API key.** If a key is accidentally exposed, revoke it and create a new one.

## Example questions

Use questions that can be answered from the documents you indexed:

- What is the employee leave policy?
- How can an employee reset their password?
- What is the laptop warranty period?
- What is the work-from-home policy?

These are example prompts only; the notebook can answer them only if the uploaded documents contain the relevant information.

## Current implementation choices

- Chunk size: 800 characters.
- Chunk overlap: 120 characters.
- Retrieval: top 3 vector-similarity results.
- Embeddings: local MiniLM model.
- Vector store: persistent local ChromaDB.
- Answer generation: Gemini `gemini-2.5-flash`.

These are starter settings, not universally optimal values. Tune and evaluate them against your own documents and questions.

## Limitations and next improvements

- Scanned/image-only PDFs need OCR before their text can be retrieved.
- The basic version uses vector retrieval only; it does not include BM25 hybrid retrieval or cross-encoder reranking.
- Source labels help trace retrieved context, but do not guarantee that every generated statement is correct.
- Retrieval quality depends on document extraction, chunking, embedding quality, and the questions asked.
- The notebook is a learning prototype, not a hardened multi-user enterprise service. Add authentication, access controls, document-level permissions, monitoring, evaluation, and secure deployment before real enterprise use.

## Learning objectives

This project provides hands-on practice with document ingestion, text preprocessing, chunking, embeddings, vector databases, semantic retrieval, prompt design, source attribution, and RAG evaluation basics.

## License

No license has been assigned yet. Add a license if you want to specify how others may reuse this repository.
