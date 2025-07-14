# 🧠 Agentic RAG with n8n + pgvector 

This repository provides a local setup for building **Agentic RAG** (Retrieval-Augmented Generation with agents) using:

* 🧩 [n8n](https://n8n.io/) for workflow orchestration

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
| Stirling-PDF | `localhost:8080` | Local PDF text extraction GUI       |

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
├── n8n/                      # n8n workflows
│   ├── subworkflow/          # Sub-agents and tools
|   │   ├── Google_Search_and_Scrape.json  # Tools for searching Google
|   │   └── Retriever_Agent.json           # Retriver Agent with access to vector db
│   └── workflow/
|       └── Document_Parsing_MultiModal.json   # Main Workflow for Document Insertion and RAG
└── README.md                 # Setup & usage guide
```

---

## 🧪 Importing Workflows in n8n

1. Visit [http://localhost:5678](http://localhost:5678)
2. Click menu → **Import from file**
3. Choose any workflow JSON from `workflows/` or `subworkflows/`
