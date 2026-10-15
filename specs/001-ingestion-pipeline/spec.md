# Feature Specification: Ingestion Pipeline

- Status: implemented
- Last reviewed: 2026-10-15

## Problem

Documents must be loaded, split, enriched, embedded, indexed, and recorded with reproducible metadata.

## Requirements

R1: support PDF and Markdown. R2: preserve source metadata. R3: write vector and sparse indexes. R4: persist ingestion history and trace.

## Acceptance criteria

- A repeated ingest uses deterministic ids and upserts rather than duplicating chunks.
- pytest -m unit

## Out of scope

This specification does not claim production-grade distributed storage, provider SLA, or a full observability platform.