# Employee Vector Search with ChromaDB

A hands-on Python script that shows how to:

1. **Create** a vector collection in [Chroma DB](https://www.trychroma.com/).  
2. **Embed** rich employee profiles with the **Sentence-Transformers** model `all-MiniLM-L6-v2`.  
3. **Query** the data three ways:
   - **Semantic similarity** (natural-language search).
   - **Metadata filtering** (SQL-like filters on fields such as department, experience, or location).
   - **Combined searches** (similarity + metadata for pinpoint accuracy).

It’s a quick reference for anyone learning modern vector databases, HNSW indexes, and hybrid filtering.

---

## 🔧 Requirements

| Tool | Version (tested) |
|------|------------------|
| Python | 3.9 or newer |
| chromadb | ^0.5 |
| sentence-transformers | ^2.7 |

> **Tip:** GPU is **not** required; CPU is fine for the small demo set.

---

## 🏃‍♂️ Quick Start

### 1. Clone the repo

```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
```

### 2. (Optional) Create & activate a virtual env
```bash
python -m venv venv
# macOS/Linux
source venv/bin/activate
# Windows
venv\Scripts\activate
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Run the script
```bash
python similarity_employeedata.py
```
- You will see console output similar to:
```console
Collection created: employee_collection
Collection contents:
Number of documents: 15
=== Similarity Search Examples ===

1. Searching for Python developers:
Query: 'Python developer with web development experience'
  1. Alex Rodriguez (employee_10) - Distance: 0.0483
  2. John Doe (employee_1)       - Distance: 0.1037
  3. Matthew Garcia (employee_14) - Distance: 0.2126
```

---

## 🧩 How the Script Works (High Level)

| Step | Code Section                              | What Happens                                                                 |
|------|-------------------------------------------|------------------------------------------------------------------------------|
| 1    | `SentenceTransformerEmbeddingFunction`    | Loads `all-MiniLM-L6-v2` for 384-dimensional embeddings.                    |
| 2    | `chromadb.Client()`                       | Starts an in-process Chroma server.                                         |
| 3    | `create_collection(...)`                  | Creates an HNSW index (`space="cosine"`) with the custom embedder.         |
| 4    | Loop over `employees`                     | Generates natural-language blurbs per employee.                            |
| 5    | `collection.add(...)`                     | Adds IDs, documents, and rich metadata rows to the collection.             |
| 6    | `collection.query(...)` & `collection.get(...)` | Performs six demo queries (semantic, filtered, hybrid).              |

---

### ✏️ Feel Free to Tweak

- **`employees` list** → Replace with your own data source (e.g., from a CSV, JSON, or database).
- **`query_text` examples** → Try custom search prompts like `"DevOps manager with AWS"` or `"HR specialist in Boston"`.
- **Metadata schema** → Extend with fields like `salary`, `skills` (as lists), `certifications`, `projects`, etc.

---

## 🙌 Acknowledgements
- Chroma DB team for the blazing-fast vector store
- Sentence-Transformers by UKP Lab
- Example employees are fictitious; any resemblance to real persons is coincidental.