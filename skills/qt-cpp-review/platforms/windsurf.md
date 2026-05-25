# Windsurf 平台说明：qt-cpp-review

在 Windsurf 中审查 Qt/C++ 代码时：

- 先运行 `references/lint-scripts/qt_review_lint.py`。
- 再做语义层审查。
- 只报告高置信问题。
- 对 Model/View、QObject ownership、线程和 QML 集成保持重点关注。

如果用户明确要求 Qt framework/module 级审查，应额外应用 framework checklist。
