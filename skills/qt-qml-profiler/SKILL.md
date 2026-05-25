---
name: qt-qml-profiler
description: 使用 QML Profiler 数据定位 Qt Quick/QML 性能问题，分析创建、绑定、绘制、JavaScript、动画和内存等维度。
metadata:
  author: qt-ai-skills
  version: "1.0"
  qt-version: "6.x"
  category: profiler
---

# QML 性能分析 Skill（中文版）

## 适用场景

当用户要求分析 QML 性能、卡顿、启动慢、动画掉帧、绑定过多、内存或渲染成本时使用。

该 skill 的目标不是凭经验猜，而是基于 profiler trace 证据定位问题。

## 输入

常见输入包括：

- QML Profiler trace 文件。
- 用户描述的症状，例如启动慢、界面切换卡顿、滚动不流畅、CPU 占用高。
- 相关 QML 文件和构建/运行环境信息。

如果没有 trace，应先说明缺少证据，并指导用户采集。

## 基本流程

1. 确认问题症状：启动慢、交互卡顿、动画掉帧、内存增长、绑定频繁等。
2. 确认 profiler 数据是否可用。
3. 解析 trace，提取高耗时事件和热点区间。
4. 按类别分析：
   - Creating / Compiling / Binding
   - JavaScript 执行
   - Painting / Rendering
   - Animation
   - Memory / Loader
5. 将热点映射回 QML 文件、组件和行号。
6. 给出按影响排序的修复建议。
7. 建议在修复后重新采集 trace 对比。

## 常见反模式

- delegate 太重，导致滚动期间大量创建和绑定。
- 热路径绑定中调用函数或复杂表达式。
- 使用 `Canvas` 进行频繁重绘或动画。
- 对复杂子树使用 `opacity`、`clip`、`layer.enabled`。
- 图片未设置 `sourceSize`，导致大图解码和纹理浪费。
- Loader 未按需关闭，隐藏组件仍占用资源。
- JavaScript 中循环执行复杂逻辑。
- 动画宽高，触发布局反复计算。

## 输出要求

报告应包含：

- 症状摘要。
- 使用的 trace 或证据来源。
- Top hotspots，按耗时或影响排序。
- 每个问题的文件/组件/行号。
- 根因解释。
- 建议修改方式。
- 验证方式：重新采集 trace、观察 FPS、启动耗时或 CPU/内存指标。

## 注意事项

- 不要在没有 trace 或测量数据时声称已确认性能根因。
- 不要只给泛泛建议；必须把建议连接到具体 QML 结构。
- 修复建议应优先简单、低风险、可验证。
- 如果问题更适合代码质量审查，应建议同时运行 `qt-qml-review`。
