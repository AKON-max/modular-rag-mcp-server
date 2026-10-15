# Feature Specification: MCP Interface

- Status: implemented

## Problem

MCP clients must be able to discover and call knowledge retrieval tools without a custom frontend.

## Requirements

R1: register stable tools. R2: validate JSON input. R3: return structured content. R4: keep stdout clean for stdio transport.

## Acceptance criteria

- A new tool can be added without changing query-engine internals.
- MCP smoke tests

## Out of scope

This specification does not claim production-grade distributed storage, provider SLA, or a full observability platform.
