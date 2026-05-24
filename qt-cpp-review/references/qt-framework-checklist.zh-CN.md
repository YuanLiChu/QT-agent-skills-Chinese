# Qt Framework / Module 审查清单

当审查 Qt framework 或模块开发代码时，除了普通 Qt/C++ 规则，还应关注：

## 二进制兼容

- 公共类新增 virtual、数据成员、enum 值时要评估 ABI。
- 公共头文件变更应谨慎。
- d-pointer / private class 使用符合项目约定。

## API 设计

- 命名与 Qt 风格一致。
- public API 简洁、可测试、可长期维护。
- 避免暴露实现细节。
- enum、flags、property、signal 语义清晰。

## 模型契约

- `dataChanged` 传递具体 roles。
- begin/end insert/remove/move/reset 成对。
- index、parent、rowCount、columnCount 处理 invalid index。

## 线程与事件循环

- QObject thread affinity 清晰。
- 跨线程调用使用正确连接方式。
- 不在错误线程访问 GUI 对象。

## 文档和测试

- 新 API 需要文档。
- 行为变更需要测试。
- 边界条件和错误路径需要覆盖。
