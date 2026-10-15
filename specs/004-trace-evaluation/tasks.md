# Tasks: Trace and Evaluation

## Phase 1 · Trace 上下文

- [x] T-EVAL-01 `TraceContext` 字段定义（trace_id / trace_type / 时间戳 / stages / metadata）
- [x] T-EVAL-02 单调时钟耗时计算
- [x] T-EVAL-03 `record_stage(name, data, elapsed_ms)`
- [x] T-EVAL-04 `finish()` 幂等收敛
- [x] T-EVAL-05 `to_dict()` 可序列化输出
- [x] T-EVAL-29 `stage_timer` 上下文管理器

## Phase 2 · 落盘与日志

- [x] T-EVAL-06 `TraceCollector` JSON Lines 追加写
- [x] T-EVAL-07 未结束 Trace 自动补 `finish()`
- [x] T-EVAL-08 写盘失败只记日志
- [x] T-EVAL-09 目标目录自动创建与路径配置化
- [x] T-EVAL-10 结构化日志（JSON Lines）

## Phase 3 · 链路打点

- [x] T-EVAL-11 摄取链路十阶段打点
- [x] T-EVAL-12 查询链路六阶段打点
- [x] T-EVAL-30 阶段记录包含 Provider 与关键计数

## Phase 4 · Dashboard

- [x] T-EVAL-13 六页面骨架与总览页
- [x] T-EVAL-14 `trace_service` 按 `trace_type` 分流
- [x] T-EVAL-15 摄取追踪 / 查询追踪瀑布视图
- [x] T-EVAL-16 评估面板
- [x] T-EVAL-17 Dashboard 冒烟测试
- [x] T-EVAL-31 Dashboard 只读约束

## Phase 5 · 评估器

- [x] T-EVAL-18 `CustomEvaluator`（hit_rate / mrr）
- [x] T-EVAL-19 `RagasEvaluator`（faithfulness / answer_relevancy / context_precision）
- [x] T-EVAL-20 ragas 延迟导入与安装提示
- [x] T-EVAL-21 `CompositeEvaluator` 指标合并
- [x] T-EVAL-22 同名指标覆盖时警告
- [x] T-EVAL-23 子评估器失败隔离
- [x] T-EVAL-32 `EvaluatorFactory` 按配置选择实现

## Phase 6 · Golden Set 与回归

- [x] T-EVAL-24 版本化 Golden Set 文件与 `GoldenTestCase` 契约
- [x] T-EVAL-25 `EvalRunner` 批处理与结构化报告
- [x] T-EVAL-26 `expected_chunk_ids` 为空时优雅跳过 IR 指标
- [x] T-EVAL-27 Recall 回归测试（`tests/e2e/test_recall.py`）
- [x] T-EVAL-28 `llm` 标记与 CI 只跑 `unit`

## Phase 7 · 验证

- [x] T-TEST-EVAL-01 `test_trace_context.py` / `test_trace_service.py`
- [x] T-TEST-EVAL-02 `test_ingestion_trace.py` / `test_query_trace.py`
- [x] T-TEST-EVAL-03 `test_custom_evaluator.py` / `test_ragas_evaluator.py` / `test_composite_evaluator.py`
- [x] T-TEST-EVAL-04 `test_eval_runner.py`
- [x] T-TEST-EVAL-05 `test_dashboard_config.py` / `test_evaluation_panel.py` / `test_dashboard_smoke.py`
- [x] T-TEST-EVAL-06 CI 执行 `pytest -m unit` 与 `ruff check .`

## Follow-up

- [ ] T-PROD-EVAL-01 为 Golden Set 补齐 `expected_chunk_ids` 与 `expected_sources`
- [ ] T-PROD-EVAL-02 扩大 Golden Set 规模并加入跨 chunk 归纳题
- [ ] T-PROD-EVAL-03 Trace 接入 OpenTelemetry 与指标告警
- [ ] T-PROD-EVAL-04 检索延迟、回退率、命中率的趋势视图
- [ ] T-PROD-EVAL-05 Trace 归档与保留策略

## Traceability

| 需求 | 任务 | 验证 |
|---|---|---|
| R-EVAL-01 | T-EVAL-01 | `test_trace_context.py` |
| R-EVAL-02 | T-EVAL-02 | `test_trace_context.py` |
| R-EVAL-03 | T-EVAL-03 | `test_trace_context.py` |
| R-EVAL-04 | T-EVAL-04 | `test_trace_context.py` |
| R-EVAL-05 | T-EVAL-05 | `test_trace_context.py` |
| R-EVAL-06 | T-EVAL-29 | `test_trace_context.py` |
| R-EVAL-07 | T-EVAL-06 | `test_trace_service.py` |
| R-EVAL-08 | T-EVAL-07 | `test_trace_service.py` |
| R-EVAL-09 | T-EVAL-08 | `test_trace_service.py` |
| R-EVAL-10 | T-EVAL-09 | `test_trace_service.py` |
| R-EVAL-11 | T-EVAL-09 | `test_config_loading.py` |
| R-EVAL-12 | T-EVAL-10 | `test_jsonl_logger.py` |
| R-EVAL-13 | T-EVAL-11 | `test_ingestion_trace.py` |
| R-EVAL-14 | T-EVAL-12 | `test_query_trace.py` |
| R-EVAL-15 | T-EVAL-30 | Trace 检查 |
| R-EVAL-16 | T-EVAL-13 | `test_dashboard_config.py` |
| R-EVAL-17 | T-EVAL-14 | `test_trace_service.py` |
| R-EVAL-18 | T-EVAL-31 | 代码审查 |
| R-EVAL-19 | T-EVAL-16 | `test_evaluation_panel.py` |
| R-EVAL-20 | T-EVAL-17 | `test_dashboard_smoke.py` |
| R-EVAL-21 | T-EVAL-18 | `test_custom_evaluator.py` |
| R-EVAL-22 | T-EVAL-19 | `test_ragas_evaluator.py` |
| R-EVAL-23 | T-EVAL-20 | `test_ragas_evaluator.py` |
| R-EVAL-24 | T-EVAL-21 | `test_composite_evaluator.py` |
| R-EVAL-25 | T-EVAL-22 | `test_composite_evaluator.py` |
| R-EVAL-26 | T-EVAL-23 | `test_composite_evaluator.py` |
| R-EVAL-27 | T-EVAL-32 | `test_evaluation_panel.py` |
| R-EVAL-28 | T-EVAL-24 | `test_eval_runner.py` |
| R-EVAL-29 | T-EVAL-24 | `test_eval_runner.py` |
| R-EVAL-30 | T-EVAL-25 | `test_eval_runner.py` |
| R-EVAL-31 | T-EVAL-26 | `test_eval_runner.py` |
| R-EVAL-32 | T-EVAL-27 | 测试文件检查 |
| R-EVAL-33 | T-EVAL-28 | `pytest -m "not llm"` |
| R-EVAL-34 | T-EVAL-25 | 报告检查 |
