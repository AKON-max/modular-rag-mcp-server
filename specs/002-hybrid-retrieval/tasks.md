# Tasks: Hybrid Retrieval

## Phase 1 · 预处理与共享契约

- [x] T-RET-00 定义 `RetrievalResult` / `ProcessedQuery` 共享类型
- [x] T-RET-01 `QueryProcessor`：关键词抽取与 filters 构造

## Phase 2 · 双路召回

- [x] T-RET-02 `DenseRetriever`：通过 `BaseVectorStore` 执行向量检索
- [x] T-RET-03 `SparseRetriever`：BM25 候选 + `get_by_ids` 补文本
- [x] T-RET-04 并行执行（线程池）与可关闭
- [x] T-RET-05 候选文本缺失的降级处理

## Phase 3 · 融合

- [x] T-RET-06 `RRFFusion`：`1/(k+rank)` 计分，`k` 来自配置
- [x] T-RET-07 仅使用名次，不使用原始分数
- [x] T-RET-08 `chunk_id` 稳定 tie-break
- [x] T-RET-09 单路独有文档参与计分
- [x] T-RET-10 空输入返回空列表

## Phase 4 · 降级编排

- [x] T-RET-11 单路失败时用另一路继续并记 Trace
- [x] T-RET-12 两路失败时抛错且包含两路原因
- [x] T-RET-13 `enable_dense` / `enable_sparse` 单路模式

## Phase 5 · 重排

- [x] T-RET-14 `RerankerFactory` 与 `NoneReranker`
- [x] T-RET-15 回退：返回原始顺序并标记 `used_fallback` / `fallback_reason`
- [x] T-RET-16 `RerankResult.original_order` 保留重排前顺序
- [x] T-RET-17 `rerank.top_k` 截断
- [x] T-RET-18 Cross-Encoder 与 LLM 后端接入工厂
- [x] T-RET-27 `RerankConfig.timeout` 超时控制

## Phase 6 · 响应组装

- [x] T-RET-19 `CitationGenerator` 引用结构
- [x] T-RET-20 Markdown `[n]` 标记与 citations 序号一致
- [x] T-RET-21 空结果 `is_empty` 语义
- [x] T-RET-22 `MultimodalAssembler` 图片懒加载
- [x] T-RET-23 MIME 扩展名映射 + 魔数嗅探

## Phase 7 · 可观测性

- [x] T-RET-24 查询链路六阶段打点
- [x] T-RET-25 融合/重排阶段记录计数与回退状态
- [x] T-RET-26 `_snapshot_results` 召回快照

## Phase 8 · 验证

- [x] T-TEST-RET-01 `test_query_processor` / `test_dense_retriever` / `test_sparse_retriever`
- [x] T-TEST-RET-02 `test_fusion_rrf` 确定性、缺失容忍、空输入
- [x] T-TEST-RET-03 `test_reranker_factory` / `test_reranker_fallback`
- [x] T-TEST-RET-04 `test_response_builder` / `test_multimodal_assembler`
- [x] T-TEST-RET-05 `test_hybrid_search` / `test_query_trace` 集成验证
- [x] T-TEST-RET-06 `test_recall` 召回回归
- [x] T-TEST-RET-07 CI 执行 `pytest -m unit` 与 `ruff check .`

## Follow-up

- [ ] T-PROD-RET-01 为 Golden Set 补齐 `expected_chunk_ids`，让 hit_rate / MRR 可用
- [ ] T-PROD-RET-02 Cross-Encoder 效果验证与默认开启评估
- [ ] T-PROD-RET-03 Query Rewrite 与同义词扩展
- [ ] T-PROD-RET-04 检索延迟与回退率指标
- [ ] T-PROD-RET-05 融合权重实验框架（在 RRF 之外做对照）

## Traceability

| 需求 | 任务 | 验证 |
|---|---|---|
| R-RET-01 | T-RET-01 | `test_query_processor.py` |
| R-RET-02 | T-RET-02 | `test_dense_retriever.py` |
| R-RET-03 | T-RET-03 | `test_sparse_retriever.py` |
| R-RET-04 | T-RET-04 | 集成用例 |
| R-RET-05 | T-RET-02 / T-RET-03 | 配置检查 |
| R-RET-06 | T-RET-05 | `test_sparse_retriever.py` |
| R-RET-07 | T-RET-06 | `test_fusion_rrf.py` |
| R-RET-08 | T-RET-07 | `test_fusion_rrf.py` |
| R-RET-09 | T-RET-08 | `test_fusion_rrf.py` |
| R-RET-10 | T-RET-09 | `test_fusion_rrf.py` |
| R-RET-11 | T-RET-06 | 配置检查 |
| R-RET-12 | T-RET-10 | `test_fusion_rrf.py` |
| R-RET-13 | T-RET-11 | 集成用例 |
| R-RET-14 | T-RET-12 | 集成用例 |
| R-RET-15 | T-RET-13 | 单元用例 |
| R-RET-16 | T-RET-14 | `test_reranker_factory.py` |
| R-RET-17 | T-RET-15 | `test_reranker_fallback.py` |
| R-RET-18 | T-RET-16 | 契约检查 |
| R-RET-19 | T-RET-27 | 契约检查 |
| R-RET-20 | T-RET-17 | `test_reranker_fallback.py` |
| R-RET-21 | T-RET-18 | `test_reranker_factory.py` |
| R-RET-22 | T-RET-19 | `test_response_builder.py` |
| R-RET-23 | T-RET-20 | `test_response_builder.py` |
| R-RET-24 | T-RET-21 | `test_response_builder.py` |
| R-RET-25 | T-RET-22 | `test_multimodal_assembler.py` |
| R-RET-26 | T-RET-23 | `test_multimodal_assembler.py` |
| R-RET-27 | T-RET-19 | 契约检查 |
| R-RET-28 | T-RET-24 | `test_query_trace.py` |
| R-RET-29 | T-RET-25 | Trace 检查 |
| R-RET-30 | T-RET-26 | Trace 检查 |
