# Modular RAG MCP Server

这是一个模块化 RAG 服务，通过 MCP（Model Context Protocol）向 AI 工具暴露知识检索能力。项目把摄取、检索、响应组装、Trace 和评估拆成独立模块，便于替换组件、定位问题和单独测试。

## 核心能力

- PDF / Markdown 文档加载与语义分块
- LLM 辅助 Chunk 精炼和元数据增强
- 文档图片 Vision Caption
- Dense、Sparse 和 Hybrid Retrieval
- RRF 融合与可配置 Reranker
- MCP 知识检索工具
- 摄取与查询链路 Trace
- Ragas + 自定义评估和固定回归集
- Streamlit Dashboard，用于查看文档、Trace 和评估结果

## 架构

```text
MCP Client / Streamlit
          │
          ▼
      Query Engine
  ├── Query Rewrite
  ├── Dense Retrieval
  ├── Sparse Retrieval
  ├── RRF Fusion
  ├── Reranker
  └── Response Assembly

    Ingestion Pipeline
  ├── Document Loader
  ├── Semantic Splitter
  ├── Chunk Refinement
  ├── Metadata Enrichment
  ├── Image Captioning
  └── Vector / Keyword Index Writers

          Storage
  ├── Chroma Vector Store
  ├── Sparse Index
  ├── SQLite Ingestion History
  └── Trace Store
```

## 仓库结构

| 路径 | 职责 |
|---|---|
| `src/core/` | 配置、检索、融合、重排、响应和 Trace |
| `src/ingestion/` | 加载、分块、增强、多模态处理和索引写入 |
| `src/mcp_server/` | MCP Server、Tools、Resources 和 Prompts |
| `src/evaluation/` | Ragas 和自定义评估 |
| `src/dashboard/` | Streamlit 调试界面 |
| `config/` | 配置、Prompt 和凭据模板 |
| `scripts/` | ingest、query、evaluate、dashboard 入口 |
| `tests/` | Unit、Integration 和 E2E 测试 |
| `specs/` | 功能规格和验收标准 |
| `docs/` | 架构、AI 工程和测试说明 |

## 环境准备

```bash
python -m venv .venv
# Windows: .venv\Scripts\activate
pip install -e ".[dev]"
cp .env.example .env
```

在 `config/settings.yaml` 中选择 Provider。真实 API Key 只放在环境变量或本地凭据文件中，不要提交到仓库。

## 运行

```bash
# 摄取文档
python scripts/ingest.py path/to/document.pdf

# 执行查询
python scripts/query.py "Hybrid Retrieval 是怎么工作的？"

# 运行评估
python scripts/evaluate.py

# 启动 Dashboard
python scripts/start_dashboard.py

# 启动 MCP Server
python main.py
```

## 测试

```bash
pytest -m unit
pytest -m "not llm"
ruff check .
```

标记为 `llm` 的测试需要真实模型服务，默认不参与本地快速验证。

## 评估

评估覆盖检索质量、答案忠实度、上下文精度、延迟和 Trace 完整性。Golden Case 和阈值作为版本化回归输入维护，不使用一次性 Notebook 结果代替工程评估。

## 当前边界

- Provider 的可用性和限流会影响评估结果。
- 检索和重排质量依赖配置的 Embedding 与 Reranker 模型。
- Dashboard 是调试工具，不是生产级可观测平台。
- 本地 Chroma 和 SQLite 适合开发及作品集规模语料；更大规模需要独立存储、并发控制和运维体系。
- Mypy 已配置，但旧代码仍存在类型错误，尚未设为 CI 阻断项。