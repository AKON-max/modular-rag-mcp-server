# AI Engineering

## Ingestion

The pipeline separates document loading, chunking, refinement, metadata enrichment, multimodal captioning, and index writes. Each step emits trace data and can be replaced independently.

## Retrieval

Dense and sparse retrieval run as separate paths. RRF combines rankings without requiring score normalization. The reranker produces the final ordered candidate list, and the response builder adds citations and multimodal context.

## Provider abstraction

LLM, embedding, reranker, splitter, vector-store, and vision components are created through factories. Switching provider should be a configuration change rather than a code rewrite.

## Evaluation

Evaluation combines Ragas metrics with project-specific checks. Fixed golden cases act as regression tests. LLM-dependent tests are marked so deterministic verification remains fast and offline.