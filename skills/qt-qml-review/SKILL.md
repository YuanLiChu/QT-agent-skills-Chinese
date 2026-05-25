---
name: qt-qml-review
description: 对 Qt6 QML 代码执行结构化只读审查，包含确定性 lint、可选 qmllint、以及绑定、布局、加载、delegate、状态和性能维度分析。
metadata:
  author: qt-ai-skills
  version: "1.0"
  qt-version: "6.x"
  category: review
---

# Qt QML 代码审查 Skill（中文版）

## 适用场景

当用户要求 review、check、audit、look over、code review、sanity check，或希望提交前检查 Qt6 QML 代码质量时使用。

该 skill 是只读流程，不修改代码。

## 范围识别

### Diff / commit 范围

当用户说“这次提交”“这些改动”“diff”“staged changes”等时：

- 读取 unstaged diff 和 staged diff。
- 如果用户说“this commit”，读取 `git diff HEAD~1..HEAD`。
- 只审查变更行及必要上下文。
- 只报告变更行中的问题。

### 代码库范围

当用户说“review the codebase”“audit the project”“review src/”或给定路径时：

- 查找范围内的 `*.qml`。
- 审查所有匹配文件。

## 执行顺序

### Phase 1：确定性 lint

运行官方 Python linter：

```bash
python3 references/lint-scripts/qt_qml_lint.py <files...>
```

若 `python3` 不存在，回退到：

```bash
python references/lint-scripts/qt_qml_lint.py <files...>
```

linter 单次扫描文件，执行机械可检查规则。输出是权威结果，不要主观否定。

规则类别包括：

- `IMP`：imports、版本号、重复导入、Controls style。
- `ORD`：QML 属性顺序。
- `BND`：绑定、`property var`、`Qt.binding`。
- `LAY`：anchors 与 Layout 混用、Layout 子项尺寸。
- `LDR`：Loader、动态创建。
- `DEL`：delegate、required property、复用安全。
- `STA`：状态、Transition、PropertyChanges。
- `IMG`：图片 `sourceSize`、异步加载。
- `PRF`：透明 Rectangle、opacity、clip、layer、RichText。
- `STY`：`id: root`、camelCase、group notation。
- `SIG`：Connections、信号处理语法。
- `ERR`：硬编码 http、非跨平台路径。
- `JS`：`var`、宽松相等、动态执行。

### Phase 1b：可选 qmllint

按以下顺序查找 `qmllint`：

1. `$QT_HOST_PATH/bin/qmllint`
2. `which qmllint` / `where qmllint`
3. 找不到则跳过并提示

若存在，运行 JSON 输出：

```bash
qmllint --json - -I <import-paths> <files...>
```

`qmllint` 对类型级问题权威，例如 unresolved type、赋值不兼容、alias 循环等。

### Phase 2：六个深度分析维度

并行分析以下六个方向：

1. Bindings & Properties：绑定正确性、类型、alias 链、裸属性访问、绑定循环。
2. Layout & Anchoring：锚定、Layout 尺寸协商、视觉树结构。
3. Component Loading & Lifecycle：Loader、动态对象、Connections 生命周期、C++ 集成。
4. ListView & Delegate Correctness：模型角色、delegate 生命周期、复用状态、复杂度。
5. States, Transitions & Structure：状态机、迁移模式、结构化组件。
6. Performance & Code Quality：渲染成本、JavaScript 质量、可维护性。

只报告置信度大于 80/100 的问题；60-79 作为 investigation target；低于 60 的怀疑不输出。

### Phase 3：合并报告

合并 lint、qmllint 和深度分析结果，按 file + line + issue 去重，输出结构化报告。

## 输出格式

报告包含：

- Scope
- Files reviewed
- Issues found
- qmllint 是否运行
- Lint findings
- Deep analysis findings
- Investigation targets
- Summary 表格

每个 lint finding 包含：

- File
- Rule
- Finding
- Mitigation

每个 deep finding 包含：

- File
- Category
- Confidence
- Finding
- Trace
- Mitigation

## 关键原则

- linter 和 qmllint 的输出是权威输入。
- 不重复报告同一个问题。
- 只读审查，不修改文件。
- 输出高置信问题，避免用低置信猜测打扰用户。
