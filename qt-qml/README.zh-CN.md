# qt-qml

该 skill 在编写或修改 QML 源码时应用 Qt 6 QML 最佳实践。它覆盖 import、Controls、Loader、属性绑定、Layouts、ListView/delegate、状态、动画、图片、可访问性、singleton、国际化和性能渲染等规则。

## 主要能力

- 生成符合 Qt 6 import 习惯的 QML，不使用版本号 import。
- 在定制 Controls 时使用具体 style import，如 `QtQuick.Controls.Basic`。
- 避免混用 anchors 和 `Layout.*`。
- 避免在 Layout 子项上直接写 `width` / `height`。
- 避免杜撰不存在的 QML 属性。
- 使用 `qsTr()` 包裹用户可见字符串。
- 对 Loader、delegate、Image、Canvas、opacity、clip 等常见性能点给出约束。

## 使用时机

当任务主要涉及 QML 文件的编写、重构、修复、优化或调试时使用。

不适用于只解释概念、且不生成或检查代码的纯问答。
