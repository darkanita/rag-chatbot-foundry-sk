# RAG Chatbot with Azure AI Foundry + Semantic Kernel

This repository implements an **end-to-end Retrieval-Augmented Generation (RAG) chatbot** using:

- **Azure AI Foundry (Copilot SDK)** – resource orchestration, evaluation  
- **Azure AI Agent Services** – agent lifecycle and orchestration  
- **Azure AI Search** – vector search + hybrid retrieval  
- **Semantic Kernel (SK)** – agent and skill orchestration  
- **Streamlit** – user-friendly chatbot interface  
- **GenAIOps practices** – reproducibility, observability, evaluation  

References:  
- [Part 1 – Create resources](https://learn.microsoft.com/en-us/azure/ai-foundry/tutorials/copilot-sdk-create-resources?tabs=windows)  
- [Part 2 – Build RAG](https://learn.microsoft.com/en-us/azure/ai-foundry/tutorials/copilot-sdk-build-rag)  
- [Part 3 – Evaluate](https://learn.microsoft.com/en-us/azure/ai-foundry/tutorials/copilot-sdk-evaluate)  
- [Semantic Kernel integration](https://learn.microsoft.com/en-us/azure/ai-foundry/how-to/develop/semantic-kernel)  

---

## 📂 Repository Structure

```
📦 rag-chatbot-foundry-sk/
├─ README.md
├─ pyproject.toml        # managed by uv
├─ .env.example
├─ data/                 # PDFs to ingest
├─ tests/                # evaluation datasets & scripts
├─ src/
│  ├─ config.py
│  ├─ create_index.py
│  ├─ ingest_pdfs.py
│  ├─ chat_backend.py
│  ├─ sk_orchestrator.py
│  ├─ agent_services.py
│  └─ ui_streamlit.py
└─ assets/
   ├─ prompts/
   └─ samples/
```

---

## ⚙️ Prerequisites

- Azure subscription with:
  - **Azure AI Foundry hub-based project**
  - **Azure OpenAI models** (chat + embeddings)
  - **Azure AI Search** (Basic tier or higher)
- Python **3.10+**
- **Azure CLI** (`az login`)
- [uv](https://docs.astral.sh/uv/) for environment + dependency management
- Streamlit for UI

---

## 🚀 Setup with uv

```bash
# Create and activate environment
uv venv
source .venv/Scripts/activate   # or .venv\Scripts\Activate.ps1 on Windows

# Install dependencies from pyproject.toml
uv pip install -e .
```

> Add new dependencies with:
> ```bash
> uv add streamlit semantic-kernel azure-ai-projects azure-search-documents azure-identity python-dotenv
> ```

---

## 🛠️ Workflow

### 1. Configure environment
Copy `.env.example` → `.env` and fill:
```
AIPROJECT_CONNECTION_STRING=<from AI Foundry>
AISEARCH_INDEX_NAME=pdf-qa-index
CHAT_MODEL=gpt-4o-mini
EMBEDDINGS_MODEL=text-embedding-ada-002
```

### 2. Create index
```bash
uv run python -m src.create_index
```

### 3. Ingest PDFs
```bash
uv run python -m src.ingest_pdfs --pdf-dir data
```

### 4. Run chatbot UI
```bash
uv run streamlit run src/ui_streamlit.py
```

Access at `http://localhost:8501`.

---

## 🔍 Evaluation (GenAIOps)

- Place Q&A test sets under `tests/`
- Run evaluation pipeline:
```bash
uv run pytest tests/
```

---

## 📈 GenAIOps Best Practices

- **Reproducibility** → `uv` + `pyproject.toml` pin dependencies  
- **Observability** → integrate with Application Insights / OpenTelemetry  
- **Evaluation** → Azure AI Foundry eval + local `tests/`  
- **MLOps alignment** → CI/CD for ingestion, SK orchestration, and UI deployment  
- **Governance** → secure connection strings, apply Responsible AI guardrails  

---

## 🔮 Next Steps

- Add SK planner for multi-turn memory  
- Containerize with Docker + `uv`  
- Deploy Streamlit app to Azure App Service / Container Apps  
- Publish agent to Copilot Studio  

---

## 📜 License

MIT (or your organization’s license).

