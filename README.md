# 🧠 Agentic RAG with n8n + pgvector 

This repository provides a local setup for building **Agentic RAG** (Retrieval-Augmented Generation with agents) using:

* 🧩 [n8n](https://n8n.io/) for workflow orchestration
* 🗃️ [pgvector](https://github.com/pgvector/pgvector) for vector storage in PostgreSQL

Everything runs locally using **Docker** and **Node.js**.

---

## 📋 Requirements

Before getting started, install the following tools:

### 🛠️ Tools

* **Node.js (LTS recommended)**
  [https://nodejs.org/](https://nodejs.org/)

* **Docker** *(Docker Engine or Docker Desktop)*
  [https://www.docker.com/get-started](https://www.docker.com/get-started)

> 💡 On macOS/Windows, use **Docker Desktop**. On Linux, the Docker CLI alone is enough.

* **DBeaver (Optional: for visualizing the Postgres DB)**
  [https://dbeaver.io/download/](https://dbeaver.io/download/)

---

## 🚀 Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/Kanisorn-S/n8n-Accounting-Rag.git
cd n8n-Accounting-Rag
```

---

### 2. Start All Services (Postgres + Stirling-PDF)

```bash
docker-compose up -d
```

This will launch:

| Service      | Port             | Purpose                             |
| ------------ | ---------------- | ----------------------------------- |
| PostgreSQL   | `localhost:5555` | Vector DB with `pgvector` extension |
| Stirling-PDF | `localhost:8080` | Local PDF text extraction GUI       |

> pgvector is auto-enabled on startup via `ankane/pgvector`.
> Stirling-PDF lets you upload and extract text from PDF documents using a web UI.
> The Stirling-PDF service is used within n8n

---

### 3. Install n8n (Globally)

```bash
npm install -g n8n
```

---

### 4. Start n8n

```bash
n8n
```

or

```bash
npx n8n
```

Then open: [http://localhost:5678](http://localhost:5678)

---

## 🧱 Folder Structure

```
n8n-Accounting-Rag/
├── docker-compose.yml        # pgvector + Stirling-PDF
├── docs/                     # Regulations Documents for vector database
│   ├── TAS_1_revised_2563.pdf
│   └── ...
├── n8n/                      # n8n workflows
│   ├── subworkflow/          # Sub-agents and tools
|   │   ├── Google_Search_and_Scrape.json  # Tools for searching Google
|   │   └── Retriever_Agent.json           # Retriver Agent with access to vector db
│   └── workflow/
|       └── Document_Parsing_MultiModal.json   # Main Workflow for Document Insertion and RAG
├── pgdata/                   # Data for Postgres Database
└── README.md                 # Setup & usage guide
```

---

## 🧪 Importing Workflows in n8n

1. Visit [http://localhost:5678](http://localhost:5678)
2. Click menu → **Import from file**
3. Choose any workflow JSON from `workflows/` or `subworkflows/`

---

## 🧰 Optional: Visualize Postgres with DBeaver

If you prefer working with a database GUI:

1. Download DBeaver: [https://dbeaver.io/download/](https://dbeaver.io/download/)
2. Connect to:

   * Host: `localhost`
   * Port: `5555`
   * Database: `vector_db`
   * User: `testuser`
   * Password: `testpwd`
