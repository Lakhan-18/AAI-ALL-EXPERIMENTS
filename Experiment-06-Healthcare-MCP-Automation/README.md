# Experiment 6: Healthcare Records Automation using MCP (Model Context Protocol)

**Domain:** Healthcare Records Automation & Clinical Orchestration  
**Platform:** Google Colab / Local Python / Streamlit  
**Protocol:** Anthropic Model Context Protocol (FastMCP)  
**Architecture:** Multi-Agent MCP Workflow (Planner, Supervisor, Validator, Orchestrator)  
**Safety & Compliance:** PHI (Protected Health Information) Clinician Approval Gate  
**Observability:** Structured JSONL Tracing & Streamlit Interactive UI  

---

## 📌 Overview

This experiment demonstrates an enterprise-grade **Healthcare Records Automation System** built on top of the **Model Context Protocol (FastMCP)**. A FastMCP server exposes six specialized clinical tools over stdio. A persistent client manages discovery and execution. The system coordinates four autonomous agents (**Planner**, **Supervisor**, **Validator**, and **Orchestrator**) to execute clinical analysis plans, benchmark sequential vs. DAG parallel execution, enforce strict PHI access controls, and provide interactive clinician dashboards via Streamlit.

---

## 🏗️ System Architecture

```mermaid
flowchart TD
    A["Clinician / Medical Request"] --> B["Planner Agent"]
    B --> C["DAG Plan Generation (Layers & Dependencies)"]
    C --> D["Supervisor Agent (Schema & Dependency Validation)"]
    
    D --> E["Orchestrator"]
    E --> F{"Policy & PHI Approval Gate"}
    F -->|High Risk / PHI (Blocked without clinician)| G["Pause / Partial Execution"]
    F -->|Approved / Routine Risk| H["MCP Client (Persistent Session)"]
    
    H --> I["FastMCP Server (stdio)"]
    subgraph FastMCP Server Tools
        T1["get_patient_vitals"]
        T2["assess_vitals_rules"]
        T3["triage_classification"]
        T4["calculate_bmi"]
        T5["patient_summary (PHI Protected)"]
        T6["list_high_risk_patients"]
    end
    I --> T1 & T2 & T3 & T4 & T5 & T6
    
    T1 & T2 & T3 & T4 & T5 & T6 --> J["Failure Classifier & Auto-Retry Loop"]
    J --> K["Validator Agent (Clinical Boundary Checks)"]
    K --> L["Observability Layer (JSONL Traces & Audit Logs)"]
    L --> M["Streamlit Dashboard & Triage View"]
```

---

## 🔑 Key Features & Technical Modules

1. **FastMCP Server & Tool Definitions:**
   - Async endpoints decorated with `@mcp.tool()`.
   - Security wrapper (`@safe_tool`) providing path traversal protection and typed parameter validation.
   - Tools include patient record retrieval, vitals evaluation, triage rating, BMI calculations, and cohort filtering.

2. **Persistent MCP Client:**
   - Single persistent `ClientSession` preventing repeated connection overhead.
   - Standardized envelope format: `{tool, status, error_type, message, data, execution_time_ms}`.

3. **Multi-Agent Orchestration Team:**
   - **Planner Agent:** Converts unstructured clinician requests into modular execution plans with explicit task dependency declarations.
   - **Supervisor Agent:** Inspects plans against live MCP tool manifests to catch illegal parameters before execution.
   - **Validator Agent:** Performs secondary checks on tool outputs (verifying heart rate bounds, systolic/diastolic ratios, SpO2 levels).
   - **Orchestrator:** Constructs execution layers for Sequential vs. Parallel (DAG) task dispatch.

4. **Security & Human-in-the-Loop PHI Gate:**
   - Tools accessing Protected Health Information (`patient_summary`) require explicit human clinician sign-off.
   - Without authorization, the policy engine safely isolates and halts the sensitive task while continuing unprivileged tasks.

5. **Failure Classification & Self-Healing:**
   - Distinguishes transient execution glitches (which trigger retries) from input validation and security violations (which fail fast).

6. **Performance Benchmarking:**
   - Directly compares Sequential execution vs. DAG Parallel execution.
   - Calculates **Degree of Parallelism (DOP)** and **Depth of Sequentiality (DOS)**.

7. **Interactive Streamlit Web Dashboard (`app.py`):**
   - Web application featuring request submission, clinician approval toggle, patient triage overview, latency graphs, and trace inspections.
   - Includes Cloudflare tunnel integration for Google Colab preview.

---

## 📁 Files in this Directory

- `AiExperiment_06_Healthcare_MCP_Automation_.ipynb`: The primary interactive notebook containing all server scripts, agent codes, DAG benchmarks, and Streamlit launch cells.
- `README.md`: System design, architecture diagrams, and operational guide.

---

## 🚀 How to Run

1. Open `AiExperiment_06_Healthcare_MCP_Automation_.ipynb` in Google Colab or your local machine.
2. Install required packages:
   ```bash
   pip install "mcp>=1.10,<2" pytest pandas matplotlib "streamlit>=1.50"
   ```
3. Run the notebook cells sequentially to:
   - Generate synthetic patient vitals datasets (`patients.csv`).
   - Run unit tests with `pytest`.
   - Start the FastMCP server and observe dynamic tool discovery.
   - Run DAG parallel workflows and compare latency vs. sequential execution.
   - Launch the Streamlit dashboard.
