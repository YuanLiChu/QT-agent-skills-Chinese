---
name: qt-cpp-review
description: 对 Qt/C++ 代码执行结构化审查，关注 Qt API 使用、对象所有权、线程、模型契约、二进制兼容、现代 C++ 和框架规则。
metadata:
  author: qt-ai-skills
  version: "1.0"
  qt-version: "6.x"
  category: review
---

# Qt C++ 代码审查 Skill（中文版）

## 适用场景

当用户要求 review、check、audit、提交前检查 Qt/C++ 代码时使用。

## 审查范围

- diff / commit 范围：只审查变更行和必要上下文。
- codebase / path 范围：审查指定路径内的 C++ / header 文件。
- framework 范围：当用户明确提到 Qt framework / module development 时，额外应用框架级规则。

## 执行流程

### Phase 1：确定性 lint

运行 `references/lint-scripts/qt_review_lint.py`，对机械可检查规则做第一轮扫描。

### Phase 2：语义审查

重点检查：

- QObject 生命周期和 parent ownership。
- 信号槽连接类型、线程亲和性、跨线程访问。
- Q_PROPERTY、NOTIFY、READ/WRITE 语义。
- QAbstractItemModel 契约：index、parent、rowCount、data、setData、dataChanged roles。
- 二进制兼容和导出宏。
- 现代 C++ 用法、const correctness、移动语义。
- Qt 容器与 STL 容器选择。
- 错误处理和 API 设计。

### Phase 3：合并报告

只输出高置信问题，按严重程度排序。避免重复报告 lint 已经覆盖的问题。

## 重点检查项

### QObject 与所有权

- parented QObject 不应手动 delete。
- 跨线程 QObject 需要关注 thread affinity。
- `deleteLater()` 只在事件循环存在时可靠。
- 避免把 parentless 对象返回给 QML 后被意外接管。

### 信号槽

- 线程间连接应明确连接类型或确保默认行为正确。
- 避免 lambda 捕获悬空对象。
- 连接生命周期应清晰。

### Model/View

- `dataChanged` 应传递具体 roles，避免 `{}` 触发全量刷新。
- `beginInsertRows` / `endInsertRows` 必须成对。
- `rowCount`、`data`、`index` 处理 invalid index。
- roleNames 与 QML delegate 角色保持一致。

### QML/C++ 集成

- 优先使用 `QML_ELEMENT` 注册类型，不推荐全局 `rootContext()->setContextProperty()`。
- 暴露给 QML 的属性应有 NOTIFY。
- 注意线程和对象所有权。

### API 与兼容性

- 公共 API 命名清晰，避免破坏 binary compatibility。
- enum、flags、虚函数、导出宏遵循项目/Qt 约定。

## 输出格式

报告包含：

- Scope
- Files reviewed
- Issues found
- Lint findings
- Deep findings
- Investigation targets
- Summary

每个问题应包含文件行号、规则、发现、影响和修复建议。

## 原则

- 审查不是风格挑剔，优先报告会导致 bug、崩溃、性能问题、维护风险的问题。
- 不修改代码。
- 低置信猜测不输出。
