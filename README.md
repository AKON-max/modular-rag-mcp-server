# Modular RAG MCP Server

A modular Retrieval-Augmented Generation service that exposes knowledge retrieval through the Model Context Protocol (MCP). The project separates ingestion, retrieval, response generation, tracing, and evaluation so each component can be replaced or tested independently.

## Capabilities

- PDF / Markdown ingestion and semantic chunking
- LLM-assisted chunk refinement and metadata enrichment
- Vision captioning for images inside documents
- Dense, sparse, and hybrid retrieval
- RRF fusion and configurable reranking
- MCP tools for knowledge retrieval
- Trace records for ingestion and query paths
- Ragas and custom evaluation with fixed regression sets
- Streamlit dashboard for inspecting documents, traces, and metrics

## Architecture

```text
MCP Client / Streamlit
        │
        ▼
Query Engine
  ├── query rewrite
  ├── dense retrieval
  ├── sparse retrieval
  ├── RRF fusion
  ├── reranker
  └── response assembly

Ingestion Pipeline
  ├── document loader
  ├── semantic splitter
  ├── chunk refinement
  ├── metadata enrichment
  ├── image captioning
  └── vector / keyword index writers

Storage
  ├── Chroma vector store
  ├── sparse index
  ├── SQLite ingestion history
  └── trace store
```

## Repository layout

| Path | Responsibility |
|---|---|
| `src/core/` | configuration, retrieval, fusion, reranking, response, tracing |
| `src/ingestion/` | loaders, chunking, enrichment, multimodal processing, index writes |
| `src/mcp_server/` | MCP server, protocol tools, resources, prompts |
| `src/evaluation/` | Ragas and custom evaluation |
| `src/dashboard/` | Streamlit inspection UI |
| `config/` | settings, prompts, credential templates |
| `scripts/` | ingest, query, evaluate, dashboard entry points |
| `tests/` | unit, integration and end-to-end tests |
| `specs/` | maintained behavior contracts |
| `docs/` | architecture, operations and testing notes |

## Setup

```bash
python -m venv .venv
# Windows: .venv\Scripts\activate
pip install -e ".[dev]"
cp .env.example .env
```

Configure the selected provider in `config/settings.yaml`. Real API keys belong in environment variables or local credential files; never commit them.

## Run

```bash
# Ingest a document
python scripts/ingest.py path/to/document.pdf

# Query the retrieval pipeline
python scripts/query.py "How does hybrid retrieval work?"

# Run evaluation
python scripts/evaluate.py

# Start the dashboard
python scripts/start_dashboard.py

# Start the MCP server
python main.py
```

## Tests

```bash
pytest -m unit
pytest -m "not llm"
ruff check .
```

Tests marked `llm` require real provider credentials and are intentionally excluded from normal local verification.

## Evaluation

The evaluation suite covers retrieval quality, answer faithfulness, context precision, latency, and trace completeness. Golden cases and thresholds are maintained as versioned regression inputs rather than one-off notebook results.

## Known limitations

- Provider availability and rate limits affect evaluation runs.
- Dense retrieval and reranking quality depend on the configured embedding and reranker models.
- The dashboard is an inspection tool, not a production observability platform.
- Local Chroma and SQLite are suitable for development and portfolio-scale corpora; larger deployments need separate storage and operational controls.
- Mypy is configured but the legacy codebase still has unresolved type errors.