# Windsurf 平台说明：qt-qml-review

在 Windsurf 中执行 QML 审查时：

- 先运行 `references/lint-scripts/qt_qml_lint.py`。
- 如果系统有 `qmllint`，再运行 `qmllint` 做类型级检查。
- 对 linter 已报告的问题不要重复报告。
- 仅输出高置信问题。
- 审查过程保持只读，不直接修改文件。

重点关注 Qt 6 迁移问题、Controls import、Layout/anchors 冲突、delegate 角色、Loader 生命周期和性能反模式。
