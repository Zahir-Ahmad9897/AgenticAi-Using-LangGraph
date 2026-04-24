# 🤖 Agentic AI Workflows with LangGraph

A high-performance repository demonstrating advanced AI agent orchestration using **LangGraph**. This project covers everything from basic linear chains to complex iterative workflows with persistence and fault tolerance.

---

## 🚀 Workflows Overview

| Workflow | Notebook | Key Features |
| :--- | :--- | :--- |
| **Sequential** | `01_Sequential_workflow.ipynb` | Linear graph: `START` ➔ `Node` ➔ `END`. |
| **Parallel** | `02_Parallel_Workflow.ipynb` | Multi-node execution for rapid feedback aggregation. |
| **Conditional** | `03_Conditional_Workflow.ipynb` | Dynamic routing based on LLM decision making. |
| **Iterative** | `04_Iterative_Workflow.ipynb` | Human-in-the-loop: Generator ➔ Reviewer cycles. |
| **Chatbot** | `Chatbot_using_LangGraph.ipynb` | State-aware conversational agents with message history. |
| **Persistence** | `Persistance_in_ChatBot_Using_LangGraph.ipynb` | Checkpointing, fault tolerance, and state history. |

---

## 🛠️ Tech Stack

- **Framework**: [LangGraph](https://github.com/langchain-ai/langgraph)
- **Orchestration**: [LangChain](https://github.com/langchain-ai/langchain)
- **LLMs**: Groq (Llama 3.3 70B), Hugging Face (Qwen 2.5)
- **Environment**: Python, Jupyter Notebooks

---

## ⚙️ Getting Started

### 1. Installation
```bash
pip install -r requirements.txt
```

### 2. Environment Setup
Create a `.env` file in the root directory:
```env
GROQ_API_KEY=your_key_here
HF_TOKEN=your_token_here
```

---

## 🏗️ Architecture Deep-Dive

### 🔄 Persistence & Fault Tolerance
The project demonstrates how to use `MemorySaver` and `InMemorySaver` to:
- **Save State**: Checkpoints are created after every node execution.
- **Recover**: Resume workflows from the exact point of failure.
- **Time Travel**: Access and re-run workflows from previous state snapshots.

### 🧠 Intelligent Routing
Uses `add_conditional_edges` to create "Routers" that dynamically direct traffic between specialized agent nodes based on intent analysis.

---

## 🤝 Contributing
Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License
MIT License