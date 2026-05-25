# Windsurf 平台说明：qt-qml

在 Windsurf 中使用该 skill 时，重点仍是约束 QML 生成质量：

- Qt 6 中不使用版本号 import。
- 已导入 `QtQuick` 时不额外导入 `QtQuick.Window`。
- 使用 `contentItem`、`background`、`handle`、`indicator` 等 Controls 定制项时，导入具体 style，如 `QtQuick.Controls.Basic`。
- Layout 子项使用 `Layout.*` 设置尺寸，不使用裸 `width` / `height`。
- 用户可见字符串使用 `qsTr()`。
- 不凭模型记忆编造 QML 属性或类型。

Windsurf 中若项目已有明确风格，优先遵循项目现有风格，并在必要时说明与通用规则的差异。
