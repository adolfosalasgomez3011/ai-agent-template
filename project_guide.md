
# 🧭 AI Agent Project Guide

This document serves as a structured cheat sheet and planning canvas for your AI agent-based projects.

---

## 0. Context  Description
Describe your project of accurate as posible this will give ocntext to the rest of section to be clear for AI during the code creation.

---
## 1. 🎯 Project Goals

Clearly define the high-level objectives of your AI agent system.

- What problem does it solve?
- What are the success criteria?
- Who are the end users?

---

## 2. 👥 Agent Definitions

Define each agent’s role and capabilities using Autogen (or CrewAI):

```yaml
agents:
  - name: assistant_agent
    role: Executes main tasks using tools and LLM
    tools: [llm_router, pinecone_tool, output_writer]
  - name: reviewer_agent
    role: Validates outputs, applies guardrails, simulates human oversight
    tools: [llm_router]
```

---

## 3. ✅ Tasks & Workflows

```yaml
tasks:
  - name: Generate Behavior Suggestions
    assigned_to: assistant_agent
    input: Baseline behaviors
    output: Structured JSON
  - name: Review & Compress Behaviors
    assigned_to: reviewer_agent
    depends_on: Generate Behavior Suggestions
```

---

## 4. 🧰 Tools Inventory

| Tool Name       | Purpose                         | File Location              |
|------------------|----------------------------------|-----------------------------|
| `llm_router`     | Route prompts to OpenAI/Ollama   | `tools/llm_router.py`       |
| `output_writer`  | Save outputs to JSON, XLSX, DOCX | `tools/output_writer.py`    |
| `pinecone_tool`  | Query Pinecone vector database   | `tools/pinecone_tool.py`    |
| `airtable_tool`  | Pull/push Airtable data          | `tools/airtable_tool.py`    |

---

## 5. 🔐 LLM Guardrails & Prompt Hygiene

- Keep prompts **clear, constrained, and grounded**
- Avoid open-ended instructions without structure
- Use this format for reliability:

```text
You are a [role]. Your job is to take the following input and produce [output].
Input:
[insert baseline or context]

Instructions:
- Return only [format]
- Do not hallucinate
```

---

## 6. 🗂️ Recommended Directory Structure

```
project_root/
├── agents/
├── tools/
├── workflows/
├── data/
├── outputs/
├── utils/
├── frontend/
├── tests/
├── .env.example
├── requirements.txt
├── README.md
└── project_guide.md
```

---

## 7. 🧪 Environment Setup Checklist

- [ ] Clone repo
- [ ] Create Conda env: `conda create -n my_ai_env python=3.12`
- [ ] Activate: `conda activate my_ai_env`
- [ ] Install deps: `pip install -r requirements.txt`
- [ ] Copy `.env.example` to `.env`
- [ ] Run: `python main.py`

---

## 8. 🧠 Starter Prompt Patterns

```
"Act as a competency evaluator. Based on the following behaviors, generate one advanced and one beginner version for each..."
```

```
"You are a summarization agent. Convert the text into 3 bullet points max. Output only JSON format."
```

---
