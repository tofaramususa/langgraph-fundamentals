# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a LangChain Academy course repository focused on LangGraph fundamentals. It contains progressive learning modules (0-6) covering LangGraph concepts from basic graph construction to advanced patterns like memory management, parallelization, and deployment.

## Environment Setup

### Prerequisites
- Python 3.11 or later (check: `python3 --version`)
- Jupyter Notebook for running course materials

### Installation

Install dependencies:
```bash
pip install -r requirements.txt
```

Or with uv (if available):
```bash
uv pip install -r requirements.txt
```

### Required API Keys

Set these environment variables (or use `.env` file):
- `OPENAI_API_KEY` - Required for all modules
- `LANGCHAIN_API_KEY` - For LangSmith tracing
- `LANGCHAIN_TRACING_V2=true` - Enable tracing
- `TAVILY_API_KEY` - Required for Module 4 (web search functionality)

### Running Notebooks

Start Jupyter:
```bash
jupyter notebook
```

Navigate to module folders to access lesson notebooks.

## LangGraph Studio

### Starting Studio

Each module has a `studio/` subdirectory with deployable graphs. To run Studio for a specific module:

```bash
cd module-X/studio
langgraph dev
```

This starts:
- API server at `http://127.0.0.1:2024`
- Studio UI at `https://smith.langchain.com/studio/?baseUrl=http://127.0.0.1:2024`
- API docs at `http://127.0.0.1:2024/docs`

### Studio Environment Setup

Each module's studio directory needs a `.env` file. You can create them all at once:

```bash
for i in {1..6}; do
  cp module-$i/studio/.env.example module-$i/studio/.env
  echo "OPENAI_API_KEY=\"$OPENAI_API_KEY\"" > module-$i/studio/.env
done
echo "TAVILY_API_KEY=\"$TAVILY_API_KEY\"" >> module-4/studio/.env
```

## Repository Architecture

### Module Structure

Each module (1-6) contains:
- **Jupyter notebooks** - Learning materials with explanations and runnable code
- **`studio/` directory** - Production-ready graph implementations
  - `langgraph.json` - Defines graph entry points and configuration
  - `*.py` - Graph implementation files
  - `.env.example` - Template for required environment variables

### Module Progression

1. **Module 1**: Basic graph construction (nodes, edges, state, conditional routing)
2. **Module 2**: Chatbots and conversation management (message state, summarization)
3. **Module 3**: Agent patterns with breakpoints and debugging
4. **Module 4**: Advanced patterns (parallelization, sub-graphs, map-reduce, research assistant with Tavily)
5. **Module 5**: Memory and state management (memory stores, schemas, persistence)
6. **Module 6**: Deployment patterns and production considerations

### Graph Definition Pattern

All studio graphs follow this pattern:

```python
from langgraph.graph import StateGraph, START, END
from typing_extensions import TypedDict

# 1. Define State
class State(TypedDict):
    # State fields...
    pass

# 2. Define nodes (functions that operate on state)
def node_function(state: State):
    # Process state
    return {"state_key": updated_value}

# 3. Build graph
builder = StateGraph(State)
builder.add_node("node_name", node_function)
builder.add_edge(START, "node_name")
builder.add_edge("node_name", END)

# 4. Compile
graph = builder.compile()
```

### Key Patterns

- **State Management**: All graphs use TypedDict-based state classes. State updates are merged, not replaced.
- **MessagesState**: Pre-built state type for chat applications, manages message history automatically.
- **Conditional Edges**: Use `Literal` types for routing decisions, returning node names as strings.
- **Tool Calling**: Module 1+ shows agent patterns with tool binding using `llm.bind_tools()` and `ToolNode`.
- **Memory**: Module 5 introduces `BaseStore` for persistent memory with namespace-based organization.
- **Configuration**: Production graphs use `RunnableConfig` with custom configuration classes for runtime parameters.

### Important Files

- `langgraph.json` - Defines which graphs are available in Studio (format: `"graph_name": "./file.py:graph"`)
- `requirements.txt` / `pyproject.toml` - Dependency specifications
- `main.py` - Simple test entry point (not used for course material)

## Development Workflow

When modifying graphs:

1. Edit the graph file in `module-X/studio/*.py`
2. If Studio is running, it will hot-reload changes
3. Test in Studio UI or via API
4. Notebooks provide context and learning materials but are separate from Studio implementations
