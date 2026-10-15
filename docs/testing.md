# Testing

The project uses a three-layer test strategy:

| Layer | Marker | Purpose |
|---|---|---|
| Unit | `unit` | Fast contracts, factories, parsers and pure algorithms |
| Integration | `integration` | Component boundaries and storage adapters |
| End-to-end | `e2e` | Complete ingestion and query paths |

Additional markers:

- `llm`: requires a real provider key
- `slow`: should not run on every local edit

Commands:

```bash
pytest -m unit
pytest -m "not llm"
pytest --cov=src
ruff check .
```

LLM calls must be mocked in unit tests. Real provider runs belong in explicitly marked integration or evaluation tests.