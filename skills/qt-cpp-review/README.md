# qt-cpp-review

该 skill 用于审查 Qt/C++ 代码，关注 Qt API 正确性、对象生命周期、线程、模型契约、现代 C++ 和框架规则。

## 审查重点

- QObject parent ownership。
- signal/slot 连接和线程亲和性。
- Q_PROPERTY / NOTIFY 语义。
- QAbstractItemModel 契约。
- QML/C++ 集成。
- 二进制兼容和导出宏。
- const correctness、移动语义和 API 设计。

## 输出

输出结构化 review report，按严重程度列出问题、影响和修复建议。

该 skill 保持只读，不直接修改代码。
