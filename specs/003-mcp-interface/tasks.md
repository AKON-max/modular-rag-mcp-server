# Tasks: MCP Interface

## Phase 1 · 启动与流约束

- [x] T-MCP-01 使用官方 MCP SDK + stdio transport
- [x] T-MCP-02 重定向所有 root logger 到 stderr
- [x] T-MCP-03 主线程预加载重依赖，避免 worker 线程导入死锁
- [x] T-MCP-04 显式声明服务名与版本
- [x] T-MCP-21 检查并禁止任何工具向 stdout 输出

## Phase 2 · 工具注册

- [x] T-MCP-05 `query_knowledge_hub` 工具与 Schema
- [x] T-MCP-06 `list_collections` 工具与 Schema
- [x] T-MCP-07 `get_document_summary` 工具与 Schema
- [x] T-MCP-08 显式 JSON Schema（不从签名推断）
- [x] T-MCP-09 工具注册表与重名拒绝

## Phase 3 · 协议

- [x] T-MCP-10 `initialize` 能力协商与 `tools/list`
- [x] T-MCP-11 `-32700` / `-32600` 解析与结构错误
- [x] T-MCP-12 `-32601` 未知方法/工具（不执行检索）
- [x] T-MCP-13 `-32602` 参数校验
- [x] T-MCP-14 `-32603` 内部异常（堆栈只进 stderr）

## Phase 4 · 返回值

- [x] T-MCP-15 `content` 数组（TextContent / ImageContent）
- [x] T-MCP-16 空结果 `is_empty` 语义
- [x] T-MCP-17 `structuredContent`（citations + metadata）
- [x] T-MCP-18 图片 MIME 与缺失容错
- [x] T-MCP-19 工具调用产生查询 Trace

## Phase 5 · 并发

- [x] T-MCP-20 工具处理器通过 `asyncio.to_thread` 执行

## Phase 6 · 验证

- [x] T-TEST-MCP-01 `test_protocol_handler.py` Schema 与错误码
- [x] T-TEST-MCP-02 `test_list_collections.py` / `test_get_document_summary.py`
- [x] T-TEST-MCP-03 `test_smoke_imports.py` 导入与预加载
- [x] T-TEST-MCP-04 `test_mcp_server.py` 集成
- [x] T-TEST-MCP-05 `test_mcp_client.py` 客户端模拟 E2E
- [x] T-TEST-MCP-06 CI 执行 `pytest -m unit` 与 `ruff check .`

## Follow-up

- [ ] T-PROD-MCP-01 支持 HTTP / SSE transport
- [ ] T-PROD-MCP-02 工具级鉴权与配额
- [ ] T-PROD-MCP-03 长时任务的进度上报与取消
- [ ] T-PROD-MCP-04 stdout 纯净性的自动化检查（把协议流做完整往返断言）

## Traceability

| 需求 | 任务 | 验证 |
|---|---|---|
| R-MCP-01 | T-MCP-01 | `test_mcp_server.py` |
| R-MCP-02 | T-MCP-02 | `test_mcp_server.py` |
| R-MCP-03 | T-MCP-03 | `test_smoke_imports.py` |
| R-MCP-04 | T-MCP-04 | `test_mcp_server.py` |
| R-MCP-05 | T-MCP-21 | 代码审查 |
| R-MCP-06 | T-MCP-05 | `test_protocol_handler.py` |
| R-MCP-07 | T-MCP-06 | `test_list_collections.py` |
| R-MCP-08 | T-MCP-07 | `test_get_document_summary.py` |
| R-MCP-09 | T-MCP-08 | `test_protocol_handler.py` |
| R-MCP-10 | T-MCP-05 / T-MCP-06 / T-MCP-07 | 描述审查 |
| R-MCP-11 | T-MCP-09 | `test_protocol_handler.py` |
| R-MCP-12 | T-MCP-10 | `test_protocol_handler.py` |
| R-MCP-13 | T-MCP-11 | `test_protocol_handler.py` |
| R-MCP-14 | T-MCP-12 | `test_protocol_handler.py` |
| R-MCP-15 | T-MCP-13 | `test_protocol_handler.py` |
| R-MCP-16 | T-MCP-14 | `test_mcp_server.py` |
| R-MCP-17 | T-MCP-15 | `test_mcp_server.py` |
| R-MCP-18 | T-MCP-16 | `test_response_builder.py` |
| R-MCP-19 | T-MCP-17 | `test_response_builder.py` |
| R-MCP-20 | T-MCP-18 | `test_multimodal_assembler.py` |
| R-MCP-21 | T-MCP-19 | `test_query_trace.py` |
| R-MCP-22 | T-MCP-20 | 代码审查 |
| R-MCP-23 | T-MCP-20 | 集成用例 |
