<img width="1680" height="1050" alt="Screenshot 2026-05-10 at 12 17 52 PM" src="https://github.com/user-attachments/assets/a3db29a7-077c-4b0b-8e8c-0e61d16c3d6f" />
<img width="1680" height="1050" alt="Screenshot 2026-05-10 at 12 17 45 PM" src="https://github.com/user-attachments/assets/b4633d4d-d3c9-48ab-b978-cd49e7dc07e1" />
<img width="1680" height="1050" alt="Screenshot 2026-05-10 at 12 17 45 PM" src="https://github.com/user-attachments/assets/ade8748e-14f8-4e6f-981e-e7c3df3b48c7" />
# 🤖 Multi-Agent Autonomous Research System

> An end-to-end AI system where 5 specialized agents collaborate to autonomously research any topic — searching academic papers, verifying citations, and generating publication-ready technical reports.

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python)
![LangGraph](https://img.shields.io/badge/LangGraph-Orchestration-orange)
![Groq](https://img.shields.io/badge/Groq-Llama%203.3%2070B-green)
![Qdrant](https://img.shields.io/badge/Qdrant-Vector%20DB-red)
![Streamlit](https://img.shields.io/badge/Streamlit-UI-ff4b4b)

---

## 🎯 What This Does

Enter any research question. The system automatically:

1. **Plans** — breaks the question into sub-questions and a search strategy
2. **Researches** — searches Arxiv and the web for relevant papers and articles
3. **Summarizes** — compresses findings into a dense, structured summary
4. **Verifies** — cross-checks every claim against real sources to reduce hallucination
5. **Reports** — generates a full technical report in Markdown with citations

If you ask a similar question again, it retrieves the answer from vector memory instantly — no redundant searches.

---

## 🏗️ System Architecture

```
User Question
      │
      ▼
┌─────────────────────────────────────────┐
│           LangGraph Orchestrator         │
│                                         │
│  ┌──────────┐    ┌──────────────────┐   │
│  │ Planner  │───▶│   Researcher     │   │
│  │  Agent   │    │ Arxiv + Web Tool │   │
│  └──────────┘    └────────┬─────────┘   │
│                           │             │
│  ┌────────────┐    ┌──────▼──────────┐  │
│  │  Citation  │◀───│  Summarizer     │  │
│  │  Verifier  │    │    Agent        │  │
│  └─────┬──────┘    └─────────────────┘  │
│        │                                │
│  ┌─────▼──────┐                         │
│  │   Report   │                         │
│  │   Writer   │                         │
│  └────────────┘                         │
└─────────────────────────────────────────┘
      │                    ▲
      │              ┌─────┴──────┐
      │              │   Qdrant   │
      └─────────────▶│  Vector DB │
     Save & Retrieve │  (Memory)  │
                     └────────────┘
```

---

## ⚙️ Tech Stack

| Component | Technology |
|---|---|
| LLM | Llama 3.3 70B via Groq API (free) |
| Agent Orchestration | LangGraph |
| Vector Database | Qdrant (in-memory) |
| Embeddings | `all-MiniLM-L6-v2` via sentence-transformers |
| Paper Search | Arxiv API (no key needed) |
| Web Search | DuckDuckGo API (free) |
| UI | Streamlit |
| Deployment | Google Colab + ngrok |

---

## 🧠 Advanced Concepts Implemented

- **Multi-agent orchestration** — LangGraph `StateGraph` with shared state across all agents
- **Tool calling** — agents decide which tool (Arxiv vs web) to use and when
- **RAG (Retrieval-Augmented Generation)** — Qdrant vector memory with cosine similarity search
- **Hallucination reduction** — Citation Verifier cross-checks every claim against real sources
- **Long-context management** — structured compression at each agent stage
- **Prompt engineering** — role-specific system prompts with enforced output formats
- **Exponential backoff** — robust retry logic for external API calls

---

## 🚀 Quick Start (Google Colab)

### 1. Get a free Groq API key
Go to [console.groq.com](https://console.groq.com) → Create API Key (free, no credit card)

### 2. Get a free ngrok token
Go to [dashboard.ngrok.com](https://dashboard.ngrok.com) → Your Authtoken (free)

### 3. Open the notebook in Colab
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com)

Add both keys to **Colab Secrets** (🔑 icon in sidebar):
- `GROQ_API_KEY` — your Groq key
- `NGROK_TOKEN` — your ngrok token

### 4. Run all cells
`Runtime → Run all` (Ctrl+F9)

A public URL will appear. Open it to use the app.

---

## 📁 Project Structure

```
multi-agent-research-system/
├── notebook/
│   └── Multi_Agent_Research_System.ipynb   # Full notebook (all phases)
├── app.py                                   # Streamlit UI
├── requirements.txt                         # Dependencies
└── README.md
```

---

## 📦 Requirements

```
groq
langchain
langchain-groq
langgraph
langchain-community
qdrant-client
sentence-transformers
arxiv
duckduckgo-search
pymupdf
streamlit
pyngrok
```

---

## 💡 Key Design Decisions

**Why Groq instead of OpenAI?**
Groq's free tier runs Llama 3.3 70B on LPU hardware — extremely fast and completely free. No credit card required.

**Why LangGraph instead of CrewAI?**
LangGraph gives explicit control over the state machine. Every agent's input and output is typed and traceable — better for debugging and extending.

**Why Qdrant in-memory instead of a hosted vector DB?**
Zero setup. For a research demo, in-memory is sufficient. Switching to hosted Qdrant Cloud requires changing one line: `QdrantClient(":memory:")` → `QdrantClient(url="...", api_key="...")`.

**Why separate Citation Verifier agent?**
LLMs hallucinate citations. Separating verification from generation forces the system to cross-check claims against real sources before the report is written — a critical pattern for any production AI system.

---

## 🔭 Future Improvements

- [ ] PDF upload — research your own documents
- [ ] Code Executor agent — runs Python from the report
- [ ] Persistent Qdrant Cloud storage — memory survives session resets
- [ ] Deploy to Hugging Face Spaces — permanent public URL
- [ ] Agent debate — agents critique each other's findings before the report
- [ ] Email delivery — send the report to your inbox

---

## 👤 Author

Built as part of an end-to-end AI/ML engineering portfolio.

**Skills demonstrated:** LangGraph · Multi-agent systems · RAG · Vector databases · Prompt engineering · LLM APIs · Streamlit · Python

---

## 📄 License

MIT
