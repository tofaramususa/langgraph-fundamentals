# LangGraph Fundamentals

A comprehensive course on LangGraph fundamentals, covering core concepts from basic graph construction to advanced patterns like memory management, parallelization, and deployment.

## Overview

This repository contains progressive learning modules (0-6) focused on foundational concepts within the LangGraph ecosystem. Each module includes Jupyter notebooks for hands-on learning and a `studio/` subdirectory with deployable graph implementations for use with LangGraph Studio.

## Module Structure

### Module 0: Python Basics
- `basics.ipynb` - Python fundamentals and setup

### Module 1: LangGraph Foundations
- `simple-graph.ipynb` - Building basic graphs with nodes, edges, and state
- `chain.ipynb` - Creating sequential chains
- `router.ipynb` - Implementing conditional routing logic
- `agent.ipynb` - Building agents with tool calling
- `agent-memory.ipynb` - Adding memory to agents
- `deployment.ipynb` - Deployment basics

**Studio Graphs:** `simple_graph`, `router`, `agent`

### Module 2: State Management
- `state-schema.ipynb` - Defining and using state schemas
- `state-reducers.ipynb` - Custom state reduction logic
- `multiple-schemas.ipynb` - Working with multiple state types
- `chatbot-summarization.ipynb` - Building chatbots with conversation summarization
- `chatbot-external-memory.ipynb` - External memory integration
- `trim-filter-messages.ipynb` - Message management strategies

**Studio Graphs:** `chatbot`

### Module 3: Debugging & Human-in-the-Loop
- `breakpoints.ipynb` - Setting and using breakpoints
- `dynamic-breakpoints.ipynb` - Conditional breakpoint logic
- `edit-state-human-feedback.ipynb` - Incorporating human feedback
- `streaming-interruption.ipynb` - Handling interruptions during streaming
- `time-travel.ipynb` - State replay and debugging

**Studio Graphs:** `agent`, `dynamic_breakpoints`

### Module 4: Advanced Patterns
- `parallelization.ipynb` - Concurrent node execution
- `sub-graph.ipynb` - Composing graphs with sub-graphs
- `map-reduce.ipynb` - Map-reduce patterns for batch processing
- `research-assistant.ipynb` - Building a research assistant with web search (Tavily)

**Studio Graphs:** `parallelization`, `sub_graphs`, `map_reduce`, `research_assistant`

### Module 5: Memory & Persistence
- `memory_store.ipynb` - Core memory store concepts
- `memory_agent.ipynb` - Agents with persistent memory
- `memoryschema_profile.ipynb` - User profile memory schemas
- `memoryschema_collection.ipynb` - Collection-based memory organization

**Studio Graphs:** `chatbot_memory`, `chatbot_memory_profile`, `chatbot_memory_collection`, `memory_agent`

### Module 6: Deployment
- `creating.ipynb` - Creating deployments
- `connecting.ipynb` - Connecting to deployed graphs
- `assistant.ipynb` - Building production assistants
- `double-texting.ipynb` - Handling concurrent requests

**Deployment Examples:** `configuration.py`, `task_maistro.py`, `docker-compose-example.yml`

## Setup

### Prerequisites

Python 3.10 or later is required (Python 3.11+ recommended for best compatibility):
```bash
python3 --version
```

### Installation

1. Clone this repository:
```bash
git clone <your-repo-url>
cd langgraph-fundamentals
```

2. Create a virtual environment and install dependencies:

**Mac/Linux/WSL:**
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

**Windows PowerShell:**
```bash
python3 -m venv .venv
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process
.venv\Scripts\activate
pip install -r requirements.txt
```

### Environment Variables

Set the following environment variables (or create a `.env` file):

**Required for all modules:**
```bash
export OPENAI_API_KEY="your-openai-api-key"
```

**Optional but recommended:**
```bash
export LANGCHAIN_API_KEY="your-langsmith-api-key"
export LANGCHAIN_TRACING_V2=true
```

**Required for Module 4 (research assistant):**
```bash
export TAVILY_API_KEY="your-tavily-api-key"
```

**Get API Keys:**
- OpenAI: [https://platform.openai.com/api-keys](https://platform.openai.com/api-keys)
- LangSmith: [https://smith.langchain.com/](https://smith.langchain.com/)
- Tavily: [https://tavily.com/](https://tavily.com/)

### Running Notebooks

Start Jupyter Notebook:
```bash
jupyter notebook
```

Navigate to any module directory and open the notebooks to begin learning.

## LangGraph Studio

LangGraph Studio is an IDE for visualizing, debugging, and testing LangGraph applications.

### Starting Studio

Navigate to any module's studio directory and start the development server:

```bash
cd module-1/studio
langgraph dev
```

This will start:
- **API Server:** http://127.0.0.1:2024
- **Studio UI:** https://smith.langchain.com/studio/?baseUrl=http://127.0.0.1:2024
- **API Docs:** http://127.0.0.1:2024/docs

### Studio Environment Setup

Each studio directory needs a `.env` file with your API keys. You can set them up all at once:

```bash
# From the repository root
for i in {1..5}; do
  cp module-$i/studio/.env.example module-$i/studio/.env
  echo "OPENAI_API_KEY=\"$OPENAI_API_KEY\"" > module-$i/studio/.env
done

# Add Tavily API key for module 4
echo "TAVILY_API_KEY=\"$TAVILY_API_KEY\"" >> module-4/studio/.env
```

## Project Structure

```
langgraph-fundamentals/
├── module-0/          # Python basics
├── module-1/          # LangGraph foundations
│   ├── *.ipynb        # Jupyter notebooks
│   └── studio/        # Deployable graphs
├── module-2/          # State management
├── module-3/          # Debugging & HITL
├── module-4/          # Advanced patterns
├── module-5/          # Memory & persistence
├── module-6/          # Deployment
├── requirements.txt   # Python dependencies
├── pyproject.toml     # Project metadata
└── CLAUDE.md          # Claude Code guidance
```

## Resources

- **LangGraph Documentation:** [https://langchain-ai.github.io/langgraph/](https://langchain-ai.github.io/langgraph/)
- **LangGraph Studio Docs:** [https://langchain-ai.github.io/langgraph/concepts/langgraph_studio/](https://langchain-ai.github.io/langgraph/concepts/langgraph_studio/)
- **LangSmith:** [https://smith.langchain.com/](https://smith.langchain.com/)
- **LangChain:** [https://python.langchain.com/](https://python.langchain.com/)
