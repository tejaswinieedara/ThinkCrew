
# 🚀 ThinkCrew — Multi-Agent Orchestration with CrewAI

[![Python](https://img.shields.io/badge/python-3.10%2B-blue)](https://www.python.org/)
[![Notebook](https://img.shields.io/badge/notebook-Jupyter-orange)](#)
[![License: MIT](https://img.shields.io/badge/license-MIT-green)](#)

---

## 🧭 Project Summary

**ThinkCrew** demonstrates a multi-agent orchestration pattern using the CrewAI framework. The repository contains a Jupyter notebook that shows how to define agents, assign tasks, and coordinate execution using LLM backends (Groq, OpenAI, etc.). The focus is clarity and reproducibility: the annotated notebook explains the pipeline step-by-step.

---

## ✅ Features

* Clean, modular notebook showing agent/task/crew setup.
* Examples of integrating search tools (e.g., Tavily) and LLMs.
* Inline comments and structured markdown for easy learning.
* Designed to run in both local Jupyter and Google Colab.

---

## 📁 Repository Structure

```
ThinkCrew/
├─ ThinkCrew.ipynb                # Original notebook
├─ README.md                      # This file
├─ requirements.txt               # (optional — suggested below)

```

---

## 🔧 Quickstart (Local)

1. Clone the repo:

```bash
git clone https://github.com/yourusername/ThinkCrew.git
cd ThinkCrew
```

2. Create & activate a virtual environment (recommended):

```bash
python -m venv .venv
# macOS / Linux
source .venv/bin/activate
# Windows (cmd)
.venv\Scripts\activate
```

3. Install dependencies:

```bash
pip install -r requirements.txt
```

*(If you don’t have `requirements.txt`, install core packages manually: `pip install crewai langchain tavily-search nbformat` — see `requirements.txt` suggestion below.)*

4. Open the notebook:

```bash
jupyter notebook ThinkCrew_Annotated.ipynb
```

---

## 📡 Quickstart (Google Colab)

1. Upload `ThinkCrew_Annotated.ipynb` to Colab or open via GitHub.
2. Use Colab to set secrets (or provide them via `userdata` if using a custom environment):

```python
from google.colab import userdata
GROQ_API_KEY = userdata.get('GROQ_API_KEY')
TAVILY_API_KEY = userdata.get('TAVILY_API_KEY')
```

3. Run cells sequentially. The annotated notebook explains each block.

---

## ⚙️ Configuration & Secrets

Do **not** hard-code credentials. Use one of:

* Environment variables (`export GROQ_API_KEY="..."`).
* Colab `userdata` (as above).
* `.env` + `python-dotenv` (local development).

**Keys used in the notebook**

* `GROQ_API_KEY` — Groq LLM backend key 
* `TAVILY_API_KEY` — Tavily Search API key 

---

## 🧩 Typical Workflow (snippets)

**Imports**

```python
# Standard grouping: stdlib, third-party, local
import os
from datetime import datetime
from crewai import Agent, Task, Crew, Process
from langchain_community.tools.tavily_search import TavilySearchResults
```

**Define an agent**

```python
research_agent = Agent(
    role="Researcher",
    goal="Collect factual references about a topic",
    tools=[TavilySearchResults()]
)
```

**Create a task and assign**

```python
task = Task(
    description="Summarize latest news about CrewAI",
    expected_output="Short bullet-point summary with links",
    agent=research_agent
)
```

**Initialize & run the crew**

```python
crew = Crew(agents=[research_agent], tasks=[task], process=Process.sequential)
result = crew.kickoff()
print(result)
```


## 🧰 Suggested `requirements.txt`

*(Paste this into `requirements.txt` or modify as needed)*

```
crewai>=0.1
langchain>=0.0
langchain-community>=0.0
tavily-search>=0.1
nbformat>=5.0
python-dotenv>=1.0
jupyterlab
```

> Pin exact versions for production or reproducibility.

---

## ⚠️ Troubleshooting

* `ModuleNotFoundError` — ensure virtual environment activated and `pip install -r requirements.txt` run.
* Authentication errors — verify API keys and that keys are set in environment/Colab.
* Long LLM latencies — reduce timeouts or switch model/endpoint in the notebook.

---

## 🤝 Contribution

Contributions are welcome.

* Open an issue to discuss large changes.
* For code contributions, fork → branch → PR.
* Keep changes minimal and add tests or documentation when introducing new features.


---

## 🧾 License

This project uses the **MIT License** — see the `LICENSE` file for details.

---

