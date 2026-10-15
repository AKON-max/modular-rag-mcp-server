# Runtime Topology

```mermaid
flowchart LR
    Client[MCP Client / Dashboard] --> API[MCP and Query APIs]
    API --> QE[Query Engine]
    QE --> Dense[Dense Retriever]
    QE --> Sparse[Sparse Retriever]
    Dense --> Fusion[RRF Fusion]
    Sparse --> Fusion
    Fusion --> Rerank[Reranker]
    Rerank --> Response[Response Builder]
    Ingest[Ingestion Pipeline] --> Store[(Chroma + Sparse Index)]
    Dense --> Store
    Sparse --> Store
    API --> Trace[Trace Store]
    Ingest --> Trace
```

## Query path

1. Query preprocessing and optional rewrite
2. Dense and sparse retrieval
3. RRF fusion
4. Reranking
5. Citation and multimodal response assembly
6. Trace persistence

## Ingestion path

1. Load document
2. Semantic chunking
3. Chunk refinement and metadata enrichment
4. Image captioning when required
5. Vector and keyword index writes
6. Ingestion history persistence