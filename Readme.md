# Agentic AI Workflows Using LangGraph

This repository demonstrates three distinct AI workflows—Sequential, Parallel, and Conditional—using LangGraph. The project showcases how to orchestrate Large Language Models (LLMs) into capable agents using directed graphs and state tracking.

---

## 1. Sequential Workflow
**File:** `01_Sequential_workflow.ipynb`

### Overview
Demonstrates a simple linear LangGraph workflow. It uses a StateGraph to connect a start node to an end node via a single LLM execution node.

### Architecture
- **State**: A `TypedDict` containing a `question` and an `ans`.
- **Nodes**:
  - `LLM_Q`: Takes the input question, prompts the LLM, and saves the answer.
- **Edges**: `START` -> `LLM_Q` -> `END`
- **Model Used**: Hugging Face Endpoint (`Qwen/Qwen2.5-7B-Instruct`)

---

## 2. Parallel Workflow
**File:** `02_Parallel_Workflow.ipynb`

### Overview
Demonstrates parallel execution where multiple specialized nodes run simultaneously to aggregate results. It features an automated essay evaluator that tests different aspects of an essay at once.

### Architecture
- **State**: Tracks the essay text, specific feedback outputs, and aggregates an `individual_score` using `operator.add`.
- **Nodes**:
  - `evaluate_lang`: Grader for language and grammar.
  - `evaluate_analysis`: Grader for critical thinking and analysis.
  - `evaluate_clarity`: Grader for structural clarity.
  - `final_evaluation`: Aggregates the parallel feedback into a final summary.
- **Edges**: 
  - `START` branches out simultaneously to all three graders.
  - All three graders converge into `final_evaluation`.
- **Model Used**: Groq API (`llama-3.3-70b-versatile`) with strict JSON structured formatting (`with_structured_output`).

---

## 3. Conditional Workflow
**File:** `03_Conditional_Workflow.ipynb`

### Overview
Showcases conditional branching (`add_conditional_edges`) where a "Router" dynamically decides the path of execution based on user input. Designed as an automated Customer Support router.

### Architecture
- **State**: Tracks `question`, `category`, and `response`.
- **Nodes**:
  - `router`: Determines if the question pertains to `billing`, `technical`, or `general` and outputs a predictably structured category.
  - `billing`, `technical`, `general`: Specialized agent nodes that handle the specific queries.
- **Edges**: 
  - `START` -> `router`
  - *Conditional Edge*: `router` uses a path map to dynamically route execution to `billing`, `technical`, or `general`.
  - All specialized nodes -> `END`
- **Model Used**: Groq API (`llama-3.3-70b-versatile`) leveraging `with_structured_output` capabilities for rigid routing schema constraints.

---

## 4. Iterative Workflow
**File:** `04_Iterative_Workflow.ipynb`

### Overview
Demonstrates an iterative "human-in-the-loop" style cyclic workflow where a generator node and a reviewer node loop repeatedly until criteria are met or a loop threshold triggers an exit. 

### Architecture
- **State**: Tracks `topic`, `draft`, `feedback`, `loop_count`, and `status`.
- **Nodes**:
  - `copywriter`: Generates and revises a draft based on editor feedback. Increments `loop_count`.
  - `editor`: Reviews the draft strictly for tone and conciseness, yielding an `approved` or `rejected` status along with specific feedback.
- **Edges**: 
  - `START` -> `copywriter`
  - `copywriter` -> `editor`
  - *Conditional Edge*: `editor` checks if `status` is `approved` or if `loop_count` >= 3. If yes, routes to `END`. Otherwise, loops back to `copywriter`.
- **Model Used**: Groq API (`llama-3.3-70b-versatile`) leveraging `with_structured_output` for strict review classification without parsing errors.
