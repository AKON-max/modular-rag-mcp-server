# Feature Specification: Trace and Evaluation

- Status: implemented
- Last reviewed: 2026-10-15

## Problem

Every ingestion and query path must be inspectable, and quality changes must be measured by regression evaluation.

## Requirements

R1: record stage timing and intermediate state. R2: expose traces to dashboard. R3: use Ragas and custom checks. R4: mark LLM-dependent tests.

## Acceptance criteria

- A regression run reports retrieval quality, faithfulness, latency and failed cases.
- pytest -m "not llm" and scripts/evaluate.py

## Out of scope

This specification does not claim production-grade distributed storage, provider SLA, or a full observability platform.