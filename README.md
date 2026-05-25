# Qt AI Skills 中文版

这是 Qt 官方 [TheQtCompanyRnD/agent-skills](https://github.com/TheQtCompanyRnD/agent-skills) 的中文 skill 仓库。仓库保留官方的 `skills/<skill-name>/SKILL.md` 目录结构，便于 Codex、Claude Code、GitHub Copilot、Gemini CLI 等 AI IDE 或 Agent 工具直接安装和加载。

## 处理原则

- `SKILL.md`、`README.md`、`platforms/*.md`、`references/*.md` 等文本说明已翻译为中文。
- `references/**/lint-scripts/*.py`、`references/scripts/*.py` 等可执行脚本保持官方原样，不做翻译或改写。
- `LICENSE` 和各 skill 下的 `LICENSE.txt` 保留官方英文原文；如目录内存在 `LICENSE.zh-CN.txt`，仅作为中文参考说明。

## Skills

| Skill | 类型 | 用途 |
| --- | --- | --- |
| `qt-cpp-review` | Review | Qt C++ 代码审查，结合确定性 lint 与多维度深度分析。 |
| `qt-qml-review` | Review | QML 代码审查，覆盖绑定、布局、Loader、delegate、状态和性能。 |
| `qt-qml` | Conceptual | 编写、审查、修复和重构 QML 时使用的最佳实践。 |
| `qt-qml-docs` | Process | 从 `.qml` 源码生成组件和应用的 Markdown 参考文档。 |
| `qt-cpp-docs` | Process | 从 Qt/C++ 源码生成类、模块、工具、头文件和入口点文档。 |
| `qt-qml-profiler` | Tool | 分析 QML Profiler `.qtd` trace，定位 Qt Quick 2D 应用性能热点。 |
| `qt-ui-design` | Conceptual | 面向 Qt Quick / Qt Widgets 的 UI 设计与可用性指导。 |

## 安装

### Codex

可以按需复制单个 skill 到本机 Codex skills 目录：

```powershell
git clone https://github.com/YuanLiChu/QT-agent-skills-Chinese.git
Copy-Item -Recurse .\QT-agent-skills-Chinese\skills\qt-qml "$env:USERPROFILE\.codex\skills\qt-qml"
Copy-Item -Recurse .\QT-agent-skills-Chinese\skills\qt-qml-review "$env:USERPROFILE\.codex\skills\qt-qml-review"
```

重启 Codex 后即可在支持的任务中自动触发。

### 其他工具

其他支持 `SKILL.md` 目录格式的 Agent 工具，可以直接引用或复制 `skills/<skill-name>` 目录。每个 skill 的入口都是该目录下的 `SKILL.md`。

## 仓库结构

```text
skills/
  qt-qml/
    SKILL.md
    README.md
    platforms/
  qt-qml-review/
    SKILL.md
    references/
      lint-scripts/
  qt-cpp-review/
    SKILL.md
    references/
      lint-scripts/
  ...
```

## 来源与许可

原始内容来自 Qt 官方 `TheQtCompanyRnD/agent-skills`。本仓库仅做中文翻译和可安装结构整理，脚本与许可证文件保留官方内容。许可证见 [LICENSE](LICENSE)。
