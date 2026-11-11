I’m excited to share a hands-on Generative AI project I’ve been building: **Enterprise Multi-Document RAG Assistant** 🚀

The goal was to build a document question-answering system that can retrieve relevant information from multiple files and generate answers grounded in the provided content.

**What it does:**
- Loads PDF, DOCX, TXT, and CSV documents
- Extracts, cleans, and splits text into overlapping chunks
- Creates embeddings using Sentence Transformers (all-MiniLM-L6-v2)
- Stores and retrieves document chunks using ChromaDB
- Uses Google Gemini to generate answers from retrieved context
- Displays source references to help trace the answer

**Tech stack:** Python | Sentence Transformers | ChromaDB | Google Gemini API | Jupyter Notebook

One important design choice: I implemented the RAG workflow directly, without using LangChain or LlamaIndex, to understand the core components step by step.

This beginner-friendly version helped me strengthen my understanding of document ingestion, embeddings, vector search, prompt design, and retrieval-augmented generation. It is a learning prototype, and I’m looking forward to improving it with hybrid search, reranking, evaluation, and a user interface.

🔗 GitHub: [Add your repository URL here]

I’d appreciate feedback and suggestions from the Generative AI and Data Science community!

#GenerativeAI #RAG #Python #ChromaDB #GoogleGemini #MachineLearning #AIProjects #LearningInPublic
