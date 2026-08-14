# Orion - Aerospace Launch Services RAG AI Support Agent

![n8n](https://img.shields.io/badge/n8n-Workflow%20Automation-FF6D5A?style=for-the-badge&logo=n8n&logoColor=white)
![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4o%20%26%20Embeddings-412991?style=for-the-badge&logo=openai&logoColor=white)
![Pinecone](https://img.shields.io/badge/Pinecone-Vector%20DB-000000?style=for-the-badge&logo=pinecone&logoColor=white)

This repository contains the backend pipelines, text chunkers, and n8n workflows for **Orion**—an enterprise Retrieval-Augmented Generation (RAG) AI Customer Support Agent developed for a German rocket launch provider.

The agent indexes 50+ pages of technical launch specifications and provides grounded, hallucination-free answers.

---

## 📂 Repository Structure

```
orion-rag-agent/
├── workflows/
│   ├── 01_ingest_pipeline.json       # Sitemap crawler, chunker, and embedding upsert
│   ├── 02_query_retriever.json       # Query vectorizer, similarity search, and LLM synthesis
│   └── 03_widget_api_listener.json  # Web widget receiver and session manager
├── scripts/
│   └── table_to_markdown.js          # Pre-processing script for HTML tables
└── README.md                         # Documentation
```

---

## ⚙️ Core Workflows

### 1. Ingestion Pipeline (`01_ingest_pipeline.json`)
* **Trigger**: Weekly cron job or manual update trigger.
* **Process**: Crawls corporate websites, splits text into 1,000-character chunks with a 200-character overlap, converts text chunks to vector embeddings using OpenAI API, and upserts them to Pinecone.

### 2. Query Retriever (`02_query_retriever.json`)
* **Trigger**: Live query submitted through the website chat widget.
* **Process**: Converts user queries to vectors, queries the vector database for the top 3 most relevant context chunks, and passes the context to GPT-4o to generate grounded, source-referenced responses.

---

## 🗄️ Database Vector Schema

The database tables correspond to the following columns in the primary vector index:

| Field Name | Data Type | Description |
| :--- | :--- | :--- |
| `ID` | `TEXT` | Unique chunk identifier |
| `Values` | `ARRAY [1536]` | OpenAI vector embedding dimensions |
| `Metadata.source_url` | `TEXT` | Source URL page of chunk |
| `Metadata.title` | `TEXT` | Title of source page |
| `Metadata.text` | `TEXT` | Cleaned text content |

---

## 🛡️ Reliability & Security Protocols

* **Hallucination Prevention**: Prompt guardrails prevent the bot from using external knowledge.
* **Similarity Score Threshold**: Discards context matches below 75% to prevent irrelevant answers.
* **Encrypted API Keys**: Secures all integration tokens using encrypted environment variables.
* **HTML Table Formatting**: Pre-processing scripts convert HTML tables to Markdown tables to preserve row and column relationships.


---
---

## Interested in a Similar System?

Want to build something like this? Let's talk.

Whether you want to:
- Replicate this exact system for your own business
- Build a custom automation tailored to your workflow
- Discuss how AI automation can solve your specific problem

**Feel free to reach out — I would love to help.**

[![LinkedIn](https://img.shields.io/badge/Connect_on_LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](http://linkedin.com/in/aina-asim-659b67369)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/AinaAsim)
[![WhatsApp](https://img.shields.io/badge/WhatsApp_Me-25D366?style=for-the-badge&logo=whatsapp&logoColor=white)](https://wa.me/923206455471)

**WhatsApp:** +92 320 6455471
**LinkedIn:** [Aina Asim](http://linkedin.com/in/aina-asim-659b67369)
**GitHub:** [github.com/AinaAsim](https://github.com/AinaAsim)

---

## Workflow Files — Confidential

The n8n workflow JSON for this project is **not published** and is kept private for security purposes.

This includes protecting:
- Real business logic and internal process flows
- Live API endpoint configurations
- Actual database schemas and credentials
- Client data and proprietary automation architecture

> This is a production system. Workflow internals are intentionally kept confidential to maintain security and client trust.
---

## 📜 License & Copyright

© 2024 Aina Asim. All Rights Reserved.

The documentation, architecture diagrams, and system designs presented in this repository are provided for **portfolio demonstration purposes only**. Unauthorized copying, modification, or distribution is prohibited.
