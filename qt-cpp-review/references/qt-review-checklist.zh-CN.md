# Qt C++ 审查清单

## QObject 与所有权

- parented QObject 不手动 delete。
- parentless 对象 ownership 必须清晰。
- `deleteLater()` 依赖事件循环。
- lambda 捕获 QObject 时注意生命周期。

## 信号槽

- 跨线程连接行为明确。
- 避免重复连接导致重复响应。
- 不从 QML 直接 emit C++ signal。
- signal 用于向上通知，函数用于向下调用。

## Q_PROPERTY

- 可变属性应有 NOTIFY。
- READ 方法通常应为 const。
- WRITE 方法应避免无变化也发信号。
- 属性类型应适合 QML 和元对象系统。

## Model/View

- `dataChanged` 使用具体 roles。
- `setData()` 正确返回 bool。
- begin/end 操作成对。
- invalid index 处理正确。
- roleNames 与 QML 使用一致。

## QML/C++ 集成

- 优先使用 `QML_ELEMENT` / `QML_NAMED_ELEMENT`。
- 避免全局 context property。
- 注意对象 ownership 和线程。

## 现代 C++

- 使用 `override`。
- const correctness。
- 避免不必要拷贝。
- 选择合适的智能指针或 Qt ownership。
- 不滥用模板或宏。

## 错误处理

- 错误路径明确。
- 不吞掉失败。
- 日志不泄露敏感信息。

## 性能

- 避免热路径不必要分配。
- 避免隐式共享容器非 const 遍历导致 detach。
- 大模型更新应最小化通知范围。
