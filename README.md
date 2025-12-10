# Vehicle Specification Extraction – Predii Assignment

## Objective
Build a system that extracts vehicle specifications (such as torque values, part numbers, and other technical specs) from an automotive service manual PDF using a Retrieval-Augmented Generation (RAG) pipeline.

This project follows the official Predii assignment guidelines:
- PDF text extraction  
- Chunking and embeddings  
- Vector-based retrieval  
- Structured specification extraction in JSON format  

---

## Pipeline Overview

The system follows these steps:

1. **PDF Text Extraction**
   - The service manual PDF is parsed using **PyMuPDF**.
   - All readable text is extracted page-by-page.

2. **Text Chunking**
   - The extracted text is split into smaller overlapping chunks for efficient semantic search.

3. **Embeddings Generation**
   - Each chunk is converted into a numerical vector using **Sentence-Transformers (MiniLM)**.

4. **Vector Store (FAISS)**
   - All embeddings are stored inside a **FAISS vector index** for fast similarity search.

5. **Retrieval**
   - For a user query (e.g., *“Torque for brake caliper bolts”*), the most relevant chunks are retrieved using semantic similarity.

6. **Specification Extraction**
   - A **rule-based heuristic extractor** is applied on the retrieved chunks to extract structured specifications.
   - The output is returned in strict JSON format.

---

## Output Format (As Required)

```json
[
  {
    "component": "Brake caliper bolts",
    "spec_type": "Torque",
    "value": "90",
    "unit": "Nm"
  }
]
