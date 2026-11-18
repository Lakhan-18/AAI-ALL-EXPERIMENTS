# Applied Artificial Intelligence & Agentic Systems Experiments (AAI)

A curated collection of production-grade experiments in **Applied AI**, **Autonomous Agentic Systems**, **Retrieval-Augmented Generation (RAG)**, and **Model Context Protocol (MCP)** architectures.

---

## 📚 Repository Overview

This repository contains end-to-end implementations of intelligent agent systems spanning multiple high-stakes domains including Healthcare, Financial Technology, Legal Intelligence, Education, and E-Commerce. Each experiment is housed in its own dedicated directory with complete source code, interactive notebooks, and comprehensive documentation.

```
AAI-ALL-EXPERIMENTS/
├── Experiment-01-Tutor-Agent/
│   ├── Experiment1_Tutor_Agent_AAiea_lab_1.ipynb
│   └── README.md
├── Experiment-02-Financial-Advisory-Agent/
│   ├── AAIEA_LAB_2.ipynb
│   └── README.md
├── Experiment-03-Clinical-Research-Assistant/
│   ├── AAIEA_LAB_3.ipynb
│   └── README.md
├── Experiment-04-Legal-Document-Retrieval/
│   ├── AAI_EXP4.ipynb
│   └── README.md
├── Experiment-05-Ecommerce-Agent-Pipeline/
│   ├── LAB_5_ecommerce_agent_pipeline.ipynb
│   └── README.md
├── Experiment-06-Healthcare-MCP-Automation/
│   ├── AiExperiment_06_Healthcare_MCP_Automation_.ipynb
│   └── README.md
├── .gitignore
└── README.md
```

---

## 🧪 Experiments Matrix

| # | Experiment Folder | Domain | Core Technologies & Concepts | Key Capabilities |
|---|-------------------|--------|------------------------------|------------------|
| **01** | [Experiment-01-Tutor-Agent](./Experiment-01-Tutor-Agent) | **Education** | Google Gemini, Pydantic, Prompt Engineering | Structured output validation, intent classification, multi-level adaptive instruction, 10 optimization prompts. |
| **02** | [Experiment-02-Financial-Advisory-Agent](./Experiment-02-Financial-Advisory-Agent) | **FinTech / Forex** | Yahoo Finance (`yfinance`), Gemini API, Matplotlib | Real-time market data ingestion, multi-indicator momentum & MA rules, deterministic BUY/SELL signals, prompt injection security testing. |
| **03** | [Experiment-03-Clinical-Research-Assistant](./Experiment-03-Clinical-Research-Assistant) | **Healthcare** | Tool Contracts, Synthetic Benchmarks, Fault Tolerance | Standardized tool contract envelopes, controlled healthcare databases, transient fault retries, 1,000-sample reliability benchmark. |
| **04** | [Experiment-04-Legal-Document-Retrieval](./Experiment-04-Legal-Document-Retrieval) | **Legal & Compliance** | FAISS, SentenceTransformers, Reciprocal Rank Fusion | Hybrid retrieval (dense semantic + keyword BM25), sliding-window chunking, cross-clause conflict detection, adversarial injection defenses. |
| **05** | [Experiment-05-Ecommerce-Agent-Pipeline](./Experiment-05-Ecommerce-Agent-Pipeline) | **E-Commerce** | Multi-Agent Coordination, Transactional Workflows | Specialized agent topology (Discovery, Cart & Pricing, Customer Support, Checkout Policy Gate), transactional state management. |
| **06** | [Experiment-06-Healthcare-MCP-Automation](./Experiment-06-Healthcare-MCP-Automation) | **Healthcare / MCP** | FastMCP, Multi-Agent DAG Orchestration, Streamlit | Anthropic Model Context Protocol, Planner/Supervisor/Validator agents, DAG parallel vs sequential execution benchmarks, PHI clinician approval gate. |

---

## 🛠️ Global Prerequisites & Setup

### Environment Requirements
- Python 3.10+
- Jupyter Notebook or Google Colab
- Git

### Recommended Virtual Environment Setup

```bash
# Clone the repository
git clone https://github.com/Lakhan-18/AAI-ALL-EXPERIMENTS.git
cd AAI-ALL-EXPERIMENTS

# Create and activate virtual environment
python -m venv venv
# On Windows:
.\venv\Scripts\activate
# On Linux/macOS:
source venv/bin/activate

# Install common foundational dependencies
pip install pydantic python-dotenv pandas numpy matplotlib jupyterlab
```

### API Keys
For experiments utilizing LLM reasoning (Experiments 1, 2, 4, 6), configure your Google Gemini API key:
```bash
export GEMINI_API_KEY="your-api-key-here"   # Linux/macOS
set GEMINI_API_KEY="your-api-key-here"      # Windows CMD
$env:GEMINI_API_KEY="your-api-key-here"     # Windows PowerShell
```

---

## 🔒 Security & Reliability Highlights Across Experiments

- **Schema Strictness:** Pydantic models guarantee typed data flow across agent interfaces.
- **Human-in-the-Loop Safety Gates:** Experiment 06 enforces clinician authorization before accessing Protected Health Information (PHI).
- **Adversarial Resilience:** Experiments 02 and 04 embed automated security test suites to evaluate defenses against system prompt leakage, role manipulation, and jailbreak attempts.
- **Deterministic Guardrails:** Financial recommendations and clinical parameters rely on deterministic calculation logic rather than ungrounded LLM completions.

---

## 📄 License
This repository is released under the [MIT License](https://opensource.org/licenses/MIT).
