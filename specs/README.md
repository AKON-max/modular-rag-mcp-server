# Specifications

本目录是 Modular RAG MCP Server 的行为契约与实现规格，分成两层：

```text
specs/
├── DEV_SPEC.md              项目级设计规格：目标、原则、选型、架构、数据契约、链路设计、测试与演进
├── README.md                本文件：目录约定与状态索引
├── _template/               新建能力规格时的骨架
└── <nnn>-<capability>/
    ├── spec.md              对外可观察行为、契约、失败语义、验收标准
    ├── plan.md              实现路径、组件边界、风险与回滚
    └── tasks.md             工作拆分与需求追溯
```

## 当前能力

| ID | 能力 | 状态 | 备注 |
|---|---|---|---|
| 001 | Ingestion Pipeline | implemented | SHA256 幂等 + 确定性 chunk id；跨存储无事务 |
| 002 | Hybrid Retrieval | implemented | Dense + BM25 + RRF(k=60)；重排默认关闭 |
| 003 | MCP Interface | implemented | stdio transport；stdout 只允许 JSON-RPC |
| 004 | Trace and Evaluation | implemented | 双链路 Trace；Golden Set 缺标准 chunk id |

## 约定

1. 一个 spec 只覆盖一个对外可观察的能力。
2. 需求 ID 稳定不复用：`R-<域>-<序号>`，删除的需求保留编号并标记 superseded。
3. 每条 P0 需求必须在 `tasks.md` 里有对应任务、在 `spec.md` 验收标准里有对应方式。
4. 验收方式必须是一条命令、一个测试或一段可复现的手工步骤。
5. 指标必须带语料、样本量、Provider 与运行口径，否则数字没有解释力。
6. 依赖真实模型的验证必须打 `llm` 标记，CI 只跑 `pytest -m unit` 与 `ruff check .`。
7. 已知边界保留在 `spec.md` 里，直到它被真正移除。
8. 工具契约（名称、必需参数、返回结构）属于对外契约，变更必须在 spec 中显式声明。
