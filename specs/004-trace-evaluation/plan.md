# Technical Plan: Trace and Evaluation

## Affected modules

- src/
- config/
- 	ests/

## Approach

Components are created through factories and connected by the ingestion and query pipelines. Provider-specific behavior stays behind interfaces.

## Risks

- External model providers may be unavailable.
- Quality changes can be caused by chunking, retrieval, fusion, reranking, or generation.
- Evaluation must separate retrieval metrics from answer metrics.

## Verification

pytest -m "not llm" and scripts/evaluate.py
