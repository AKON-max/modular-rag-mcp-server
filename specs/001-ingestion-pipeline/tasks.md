# Tasks: Ingestion Pipeline

## Phase 1 · 类型与完整性

- [x] T-ING-00 定义 `Document` / `Chunk` / `ChunkRecord` / `PipelineResult`
- [x] T-ING-01 `compute_sha256` 文件哈希
- [x] T-ING-02 `should_skip` 跳过已成功处理的文件
- [x] T-ING-03 失败记录保留且不阻止重试 + WAL 模式

## Phase 2 · 加载与分块

- [x] T-ING-04 Loader 抽象基类与 PDF 加载实现
- [x] T-ING-05 Splitter 抽象基类、三种实现与工厂
- [x] T-ING-06 分块参数（chunk_size / chunk_overlap）与空文档边界

## Phase 3 · Transform

- [x] T-ING-07 `ChunkRefiner`：LLM 路径 + 规则回退
- [x] T-ING-08 `MetadataEnricher`：LLM 路径 + 规则回退
- [x] T-ING-09 `ImageCaptioner`：可选生成 + 失败跳过
- [x] T-ING-24 Prompt 外置到 `config/prompts/`

## Phase 4 · 编码

- [x] T-ING-10 `DenseEncoder` 通过 Embedding Factory
- [x] T-ING-11 `SparseEncoder` 分词与词频统计
- [x] T-ING-12 `BatchProcessor` 分批与顺序一致
- [x] T-ING-13 批次失败定位

## Phase 5 · 写入

- [x] T-ING-14 确定性 `chunk_id` 生成
- [x] T-ING-15 `VectorUpserter` 幂等写入
- [x] T-ING-16 `BM25Indexer` 倒排索引构建与往返查询
- [x] T-ING-17 `ImageStorage` 图片落盘与映射

## Phase 6 · 编排与文档管理

- [x] T-ING-18 `DocumentManager` 列表 / 详情 / 删除
- [x] T-ING-19 删除时按依赖顺序清理三类存储
- [x] T-ING-20 全链路 Trace 打点
- [x] T-ING-21 `on_progress` 进度回调
- [x] T-ING-22 `scripts/ingest.py` 参数解析与目录展开
- [x] T-ING-23 退出码语义（0 / 1 / 2）

## Phase 7 · 验证

- [x] T-TEST-ING-01 单元测试：完整性、分块、Transform、编码、写入
- [x] T-TEST-ING-02 集成测试：Pipeline 全链路与 Trace
- [x] T-TEST-ING-03 E2E：样例文档目录摄取
- [x] T-TEST-ING-04 CI 执行 `pytest -m unit` 与 `ruff check .`

## Follow-up

- [ ] T-PROD-ING-01 跨存储写入的补偿任务，消除中间不一致
- [ ] T-PROD-ING-02 增量更新：文件变更时清理旧 chunk
- [ ] T-PROD-ING-03 OCR 与表格结构还原
- [ ] T-PROD-ING-04 大文件流式处理与内存上限治理
- [ ] T-PROD-ING-05 摄取延迟与失败率指标

## Traceability

| 需求 | 任务 | 验证 |
|---|---|---|
| R-ING-01 | T-ING-01 | `test_file_integrity.py` |
| R-ING-02 | T-ING-02 | 集成用例 |
| R-ING-03 | T-ING-03 | `test_file_integrity.py` |
| R-ING-04 | T-ING-03 | 集成用例 |
| R-ING-05 | T-ING-03 | 实现检查 |
| R-ING-06 | T-ING-04 | `test_loader_pdf_contract.py` |
| R-ING-07 | T-ING-05 | `test_splitter_factory.py` |
| R-ING-08 | T-ING-06 | `test_document_chunker.py` |
| R-ING-09 | T-ING-06 | `test_document_chunker.py` |
| R-ING-10 | T-ING-07 | `test_chunk_refiner.py` |
| R-ING-11 | T-ING-08 | `test_metadata_enricher_contract.py` |
| R-ING-12 | T-ING-09 | `test_image_storage.py` |
| R-ING-13 | T-ING-24 | 代码审查 |
| R-ING-14 | T-ING-10 | `test_dense_encoder.py` |
| R-ING-15 | T-ING-11 | `test_sparse_encoder.py` |
| R-ING-16 | T-ING-12 | `test_batch_processor.py` |
| R-ING-17 | T-ING-13 | `test_batch_processor.py` |
| R-ING-18 | T-ING-14 | `test_vector_upserter_idempotency.py` |
| R-ING-19 | T-ING-15 | `test_vector_upserter_idempotency.py` |
| R-ING-20 | T-ING-16 | `test_bm25_indexer_roundtrip.py` |
| R-ING-21 | T-ING-17 | `test_image_storage.py` |
| R-ING-22 | T-ING-18 | `test_document_manager.py` |
| R-ING-23 | T-ING-19 | `test_document_manager.py` |
| R-ING-24 | T-ING-20 | `test_ingestion_trace.py` |
| R-ING-25 | T-ING-21 | `test_pipeline_progress.py` |
| R-ING-26 | T-ING-22 | CLI 用例 |
| R-ING-27 | T-ING-23 | CLI 用例 |
