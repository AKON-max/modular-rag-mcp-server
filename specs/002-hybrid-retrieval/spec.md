# Feature Specification: Hybrid Retrieval

- Status: implemented

## Problem

The query path must combine dense and sparse retrieval, fuse rankings, rerank candidates, and return citations.

## Requirements

R1: dense and sparse retrieval run independently. R2: RRF fuses rankings. R3: reranker is replaceable. R4: responses include citation metadata.

## Acceptance criteria

- A query returns both semantic and exact-term candidates when appropriate.
- pytest -m unit and evaluation scripts

## Out of scope

This specification does not claim production-grade distributed storage, provider SLA, or a full observability platform.
