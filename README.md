<div align="center">

<!-- ═══════════════════════════════════════════════════════════
     HEADER — capsule-render (reliable GitHub SVG renderer)
════════════════════════════════════════════════════════════ -->
<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6,11,20&height=200&section=header&text=Intelligent%20PDF%20Q%26A%20System&fontSize=40&fontColor=ffffff&animation=fadeIn&fontAlignY=38&desc=Powered%20by%20LangChain%20%7C%20RAG%20%7C%20ChromaDB%20%7C%20Sentence%20Transformers&descAlignY=58&descSize=16&descColor=dddddd" />

<br/>

<!-- Author & Repo -->
<a href="https://github.com/saifullah857">
  <img src="https://img.shields.io/badge/Author-saifullah857-6C63FF?style=for-the-badge&logo=github&logoColor=white" />
</a>
&nbsp;
<a href="https://github.com/saifullah857/Intelligent-PDF-question-answering-system-with-LangChain-">
  <img src="https://img.shields.io/badge/Repo-Intelligent--PDF--QA-FF6B35?style=for-the-badge&logo=github&logoColor=white" />
</a>

<br/><br/>

<!-- Tech Stack -->
![Python](https://img.shields.io/badge/Python-3.9%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)
![LangChain](https://img.shields.io/badge/LangChain-0.3+-1C3C3C?style=for-the-badge&logo=chainlink&logoColor=white)
![ChromaDB](https://img.shields.io/badge/ChromaDB-Vector%20Store-FF6B35?style=for-the-badge&logo=databricks&logoColor=white)
![HuggingFace](https://img.shields.io/badge/HuggingFace-Embeddings-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black)

<br/>

<!-- Status -->
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=flat-square)](https://opensource.org/licenses/MIT)
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=flat-square)
![PRs Welcome](https://img.shields.io/badge/PRs-Welcome-blueviolet?style=flat-square)
![Maintained](https://img.shields.io/badge/Maintained-Yes-success?style=flat-square)
[![GitHub Stars](https://img.shields.io/github/stars/saifullah857/Intelligent-PDF-question-answering-system-with-LangChain-?style=flat-square&color=yellow)](https://github.com/saifullah857/Intelligent-PDF-question-answering-system-with-LangChain-/stargazers)
[![GitHub Forks](https://img.shields.io/github/forks/saifullah857/Intelligent-PDF-question-answering-system-with-LangChain-?style=flat-square&color=orange)](https://github.com/saifullah857/Intelligent-PDF-question-answering-system-with-LangChain-/network)

<br/><br/>

<blockquote>
💡 <b>Upload any PDF. Ask anything. Get precise, context-aware answers.</b><br/>
A full RAG pipeline — chunk, embed, store, retrieve — built with LangChain, ChromaDB & Sentence Transformers.
</blockquote>

<br/>

[🏗️ Architecture](#️-pipeline-architecture) &nbsp;·&nbsp;
[🚀 Quick Start](#-quick-start) &nbsp;·&nbsp;
[💡 Usage](#-usage) &nbsp;·&nbsp;
[🔧 Configuration](#-configuration) &nbsp;·&nbsp;
[🤝 Contributing](#-contributing)

</div>

---

## 📌 Table of Contents

- [✨ Features](#-features)
- [🏗️ Pipeline Architecture](#️-pipeline-architecture)
- [📁 Project Structure](#-project-structure)
- [⚙️ Tech Stack](#️-tech-stack)
- [🚀 Quick Start](#-quick-start)
- [💡 Usage](#-usage)
- [🔧 Configuration](#-configuration)
- [📊 How It Works](#-how-it-works)
- [🙋 FAQ](#-faq)
- [🤝 Contributing](#-contributing)
- [👤 Author](#-author)
- [📄 License](#-license)

---

## ✨ Features

<div align="center">

| 🚀 Feature | 📝 Description |
|:---|:---|
| 📄 **Multi-PDF Ingestion** | Batch-load entire folders of PDFs automatically in one pipeline call |
| ✂️ **Intelligent Chunking** | Recursive character splitting that preserves semantic boundaries with overlap |
| 🧠 **Semantic Embeddings** | `all-MiniLM-L6-v2` dense vectors for meaning-based retrieval, not keyword matching |
| 💾 **Persistent Vector Store** | ChromaDB stores embeddings on disk — no re-processing on restart |
| 🔍 **Cosine Similarity Search** | Score-filtered, ranked top-k retrieval for the most relevant context |
| 🤖 **Natural Language Q&A** | Ask plain-English questions — get context-grounded, source-attributed answers |
| 🔌 **Fully Modular Design** | Swap any component: loader, embedder, vector store, or LLM |
| 📊 **Source Attribution** | Every result traces back to the originating PDF page and document |

</div>

---

## 🏗️ Pipeline Architecture

```
╔═══════════════════════════════════════════════════════════════════════╗
║                  📥  INGESTION PIPELINE                              ║
╠═══════════════════════════════════════════════════════════════════════╣
║                                                                       ║
║   📂 PDF Folder                                                       ║
║       │                                                               ║
║       ▼                                                               ║
║   📄 PyPDFLoader          →   Load pages as Document objects          ║
║       │                                                               ║
║       ▼                                                               ║
║   ✂️  RecursiveTextSplitter →  Chunk into 500-char segments           ║
║       │                                                               ║
║       ▼                                                               ║
║   🧠 SentenceTransformer   →  Encode chunks into 384-dim vectors      ║
║       │                                                               ║
║       ▼                                                               ║
║   💾 ChromaDB (Persistent) →  Store embeddings + metadata on disk    ║
║                                                                       ║
╠═══════════════════════════════════════════════════════════════════════╣
║                  🔍  RETRIEVAL & Q&A PIPELINE                        ║
╠═══════════════════════════════════════════════════════════════════════╣
║                                                                       ║
║   ❓ User Question                                                    ║
║       │                                                               ║
║       ▼                                                               ║
║   🧠 Embed Query           →  Same model, same vector space           ║
║       │                                                               ║
║       ▼                                                               ║
║   📐 Cosine Similarity     →  Top-K nearest chunks from ChromaDB      ║
║       │                                                               ║
║       ▼                                                               ║
║   📋 Ranked Context Chunks →  Filtered by similarity score threshold  ║
║       │                                                               ║
║       ▼                                                               ║
║   💬 Grounded Answer       →  Answer with source & page attribution   ║
║                                                                       ║
╚═══════════════════════════════════════════════════════════════════════╝
```

---

## 📁 Project Structure

```
📦 Intelligent-PDF-question-answering-system-with-LangChain/
│
├── 📂 data/
│   ├── 📂 pdfs/                   ← 📥 Place your PDF documents here
│   ├── 📂 vector_store/           ← 🗃️  Auto-generated ChromaDB storage
│   └── 📄 Python.txt              ← 📝 Sample text for quick testing
│
├── 📓 main.ipynb                  ← 🚀 End-to-end pipeline notebook
├── 📄 requirements.txt            ← 📦 All Python dependencies
├── 📄 .gitignore                  ← 🙈 Ignore venv, __pycache__, etc.
└── 📘 README.md
```

---

## ⚙️ Tech Stack

<div align="center">

| Layer | Badge | Library | Role |
|:---:|:---:|:---:|:---|
| **Orchestration** | ![LangChain](https://img.shields.io/badge/-LangChain-1C3C3C?style=flat-square&logo=chainlink&logoColor=white) | `langchain-community` | Pipeline orchestration & document loaders |
| **Text Splitting** | ![Split](https://img.shields.io/badge/-TextSplitter-6C63FF?style=flat-square) | `langchain-text-splitters` | Recursive character-based chunking |
| **Embeddings** | ![HF](https://img.shields.io/badge/-SentenceTransformers-FFD21E?style=flat-square&logo=huggingface&logoColor=black) | `sentence-transformers` | Semantic dense vector encoding |
| **Vector Store** | ![Chroma](https://img.shields.io/badge/-ChromaDB-FF6B35?style=flat-square&logo=databricks&logoColor=white) | `chromadb` | Persistent vector database |
| **PDF Parsing** | ![PDF](https://img.shields.io/badge/-PyMuPDF-00897B?style=flat-square) | `pymupdf` / `pypdf` | High-fidelity PDF text extraction |
| **Similarity** | ![SK](https://img.shields.io/badge/-Scikit--Learn-F7931E?style=flat-square&logo=scikit-learn&logoColor=white) | `scikit-learn` | Cosine similarity computation |

</div>

---

## 🚀 Quick Start

### 1️⃣ &nbsp;Clone the Repository

```bash
git clone https://github.com/saifullah857/Intelligent-PDF-question-answering-system-with-LangChain-.git
cd RAG_Project
```

### 2️⃣ &nbsp;Create & Activate Virtual Environment *(recommended)*

```bash
python -m venv venv

# ── Windows ───────────────────────────
venv\Scripts\activate

# ── macOS / Linux ─────────────────────
source venv/bin/activate
```

### 3️⃣ &nbsp;Install All Dependencies

```bash
pip install -r requirements.txt
```

<details>
<summary>📋 <b>Or install packages manually</b></summary>

<br/>

```bash
pip install langchain langchain-core langchain-community \
            pypdf pymupdf sentence-transformers          \
            chromadb scikit-learn langchain-text-splitters
```

</details>

### 4️⃣ &nbsp;Add Your PDF Documents

```
📂 data/pdfs/
  ├── research_paper.pdf
  ├── company_handbook.pdf
  └── any_document.pdf       ← Drop any PDFs here
```

### 5️⃣ &nbsp;Launch the Notebook

```bash
# Option A — VS Code (recommended)
code .
# Open main.ipynb → click "Run All"

# Option B — Jupyter
jupyter notebook main.ipynb
```

---

## 💡 Usage

### 🔧 Initialize All Components

```python
# ── Embeddings ────────────────────────────────────────────────
embedding_manager = EmbeddingManager(model_name="all-MiniLM-L6-v2")

# ── Vector Store ──────────────────────────────────────────────
vector_store = VectorStoreManager(
    persist_directory="data/vector_store",
    collection_name="pdf_documents"
)

# ── Retriever ─────────────────────────────────────────────────
rag_retriever = RAGRetriever(embedding_manager, vector_store)
```

### 📥 Ingest Your PDFs

```python
# Step 1 — Load
all_docs = load_all_pdfs()
print(f"✅ Loaded {len(all_docs)} pages")

# Step 2 — Chunk
chunks = split_docs(all_docs, chunk_size=500, chunk_overlap=50)
print(f"✅ Created {len(chunks)} chunks")

# Step 3 — Embed
texts = [doc.page_content for doc in chunks]
embeddings = embedding_manager.generate_embeddings(texts)
print(f"✅ Generated embeddings: {embeddings.shape}")

# Step 4 — Store
vector_store.add_documents(chunks, embeddings)
print(f"✅ Stored in ChromaDB — ready to query!")
```

### ❓ Ask Questions About Your PDFs

```python
query = "What is the encoder-decoder architecture?"

results = rag_retriever.retrieve(query=query, top_k=5, score_threshold=0.3)

print(f"\n🔍 Query : {query}")
print("=" * 65)

for doc in results:
    print(f"\n  📌 Rank #{doc['rank']}  |  Similarity: {doc['similarity_score']:.4f}")
    print(f"  📄 Source : {doc['metadata'].get('source', 'N/A')}")
    print(f"  📃 Page   : {doc['metadata'].get('page', 'N/A')}")
    print(f"\n  {doc['document'][:300]}...")
    print("─" * 65)
```

**Sample Output:**

```
🔍 Query : What is the encoder-decoder architecture?
═════════════════════════════════════════════════════════════════

  📌 Rank #1  |  Similarity: 0.8742
  📄 Source   : data/pdfs/attention_paper.pdf
  📃 Page     : 3

  The encoder maps an input sequence to a sequence of continuous
  representations z. Given z, the decoder generates an output
  sequence of symbols one element at a time...
─────────────────────────────────────────────────────────────────
```

---

## 🔧 Configuration

```python
# ╔══════════════════════════════════════════════════════════╗
# ║              ⚙️  PIPELINE CONFIGURATION                 ║
# ╠══════════════════════════════════════════════════════════╣

# ── Document Chunking ─────────────────────────────────────
CHUNK_SIZE      = 500    # Max characters per chunk
CHUNK_OVERLAP   = 50     # Overlap to preserve cross-boundary context

# ── Embedding Model ───────────────────────────────────────
EMBEDDING_MODEL = "all-MiniLM-L6-v2"   # 384-dim | CPU-friendly | Fast

# ── ChromaDB Vector Store ─────────────────────────────────
PERSIST_DIR     = "data/vector_store"
COLLECTION_NAME = "pdf_documents"

# ── Retrieval Parameters ──────────────────────────────────
TOP_K           = 5      # Number of chunks to retrieve per query
SCORE_THRESHOLD = 0.0    # Min cosine similarity — raise to 0.3–0.5 for precision

# ╚══════════════════════════════════════════════════════════╝
```

> 💡 **Pro Tip:** Start with `score_threshold=0.0` to inspect all results, then raise it to `0.4` for tighter, higher-quality answers on technical documents.

---

## 📊 How It Works

<details>
<summary><b>📄 Step 1 — Document Loading</b></summary>
<br/>
<code>PyPDFLoader</code> reads every <code>.pdf</code> in <code>data/pdfs/</code>. Each page becomes a LangChain <code>Document</code> with <code>page_content</code> (raw text) and <code>metadata</code> (source path, page number). Multiple PDFs are merged into a single document list automatically.
</details>

<details>
<summary><b>✂️ Step 2 — Intelligent Chunking</b></summary>
<br/>
<code>RecursiveCharacterTextSplitter</code> splits text using a separator hierarchy: <code>\n\n</code> → <code>\n</code> → <code>" "</code>. This preserves paragraph and sentence structure far better than naive character splitting. The 50-character overlap ensures context is never lost at a boundary.
</details>

<details>
<summary><b>🧠 Step 3 — Semantic Embedding</b></summary>
<br/>
Each chunk is encoded into a 384-dimensional dense vector by <code>all-MiniLM-L6-v2</code>. Trained for semantic textual similarity, this model places related chunks geometrically close in vector space — regardless of exact word matches — enabling true meaning-based retrieval.
</details>

<details>
<summary><b>💾 Step 4 — Persistent Vector Storage</b></summary>
<br/>
ChromaDB persists each vector with its raw text and metadata (source file, page, content length) to a local database. UUIDs prevent duplicate entries. The store survives session restarts — no re-embedding required on subsequent runs.
</details>

<details>
<summary><b>🔍 Step 5 — Retrieval & Ranking</b></summary>
<br/>
The user's question is embedded with the same model. ChromaDB performs approximate nearest-neighbor search to find top-k candidates. Cosine similarity re-scores results, which are then filtered by threshold and returned ranked — most relevant chunk first.
</details>

---

## 🙋 FAQ

<details>
<summary><b>❓ Do I need a GPU to run this?</b></summary>
<br/>
No — <code>all-MiniLM-L6-v2</code> runs efficiently on CPU. A GPU will significantly speed up embedding for large-scale ingestion (thousands of pages).
</details>

<details>
<summary><b>❓ Can I swap the embedding model?</b></summary>
<br/>
Yes. Pass any HuggingFace sentence-transformers model to <code>EmbeddingManager(model_name="...")</code>. Alternatives: <code>all-mpnet-base-v2</code> (higher accuracy, slower) or <code>multi-qa-MiniLM-L6-cos-v1</code> (optimized for Q&A).
</details>

<details>
<summary><b>❓ Will my vector store persist between sessions?</b></summary>
<br/>
Yes — ChromaDB's <code>PersistentClient</code> saves everything to <code>data/vector_store/</code>. Just re-initialize <code>VectorStoreManager</code> and your embeddings are immediately ready to query.
</details>

<details>
<summary><b>❓ How do I add more PDFs after initial ingestion?</b></summary>
<br/>
Drop new PDFs into <code>data/pdfs/</code> and re-run the ingestion cells. ChromaDB assigns new UUIDs — existing documents are not duplicated, only new ones are added.
</details>

---

## 🤝 Contributing

Contributions, issues and feature requests are welcome!

```bash
# 1. Fork the project on GitHub
# 2. Create your feature branch
git checkout -b feature/AmazingFeature

# 3. Commit your changes
git commit -m "feat: add AmazingFeature"

# 4. Push to the branch
git push origin feature/AmazingFeature

# 5. Open a Pull Request
```

> Please follow [Conventional Commits](https://www.conventionalcommits.org/) and open an issue to discuss large changes before submitting a PR.

---

## 👤 Author

<div align="center">

<a href="https://github.com/saifullah857">
  <img src="https://github.com/saifullah857.png" width="100" style="border-radius:50%;" alt="saifullah857" />
</a>

<br/><br/>

**Saifullah**

[![GitHub](https://img.shields.io/badge/GitHub-saifullah857-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/saifullah857)

<br/>

*If you found this helpful, please consider giving it a ⭐ — it really helps!*

[![Star](https://img.shields.io/github/stars/saifullah857/Intelligent-PDF-question-answering-system-with-LangChain-?style=social)](https://github.com/saifullah857/Intelligent-PDF-question-answering-system-with-LangChain-)

</div>

---

## 📄 License

Distributed under the **MIT License**.
See [`LICENSE`](./LICENSE) for full details.

---

<!-- Footer Wave -->
<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6,11,20&height=100&section=footer" />

<div align="center">
<sub>Built with ❤️ by <a href="https://github.com/saifullah857">saifullah857</a> · LangChain · ChromaDB · Sentence Transformers · Python</sub>
</div>