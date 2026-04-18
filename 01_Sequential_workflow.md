# Sequential Workflow

This file documents the Sequential Workflow implemented in `01_Sequential_workflow.ipynb`.

## Overview
This notebook demonstrates a simple LangGraph workflow using a sequential design. It uses a StateGraph to connect a start node to an end node via a single Large Language Model (LLM) execution node.

## Architecture
- **State**: The state is defined using a `TypedDict` containing a `question` (string) and an `ans` (string).
- **Nodes**:
  - `LLM_Q`: Takes the input question, prompts the LLM to answer it, and saves the answer back into the state.
- **Edges**: 
  - `START` -> `LLM_Q`
  - `LLM_Q` -> `END`

## Model Used
- Hugging Face Endpoint: `Qwen/Qwen2.5-7B-Instruct`
- Task: conversational
