# qt-qml-review

该 skill 用于审查 Qt 6 QML 代码。它结合确定性 Python linter、可选 `qmllint`、以及多个语义分析维度，对 QML 代码进行只读检查。

## 审查内容

- import 规则和 Controls style。
- QML 属性顺序和命名约定。
- 属性绑定、`property var`、绑定破坏。
- anchors 与 Layout 使用。
- Loader 生命周期。
- delegate 角色、复用和复杂度。
- 状态、Transition、PropertyChanges。
- 图片、RichText、Canvas、opacity、clip、layer 等性能点。
- JavaScript 中的 `var`、宽松相等、动态执行。

## 输出

输出结构化审查报告，包含 lint findings、深度分析 findings、人工确认项和 summary。

该 skill 不修改代码。
