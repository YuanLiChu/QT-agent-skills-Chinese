# qt-qml-profiler

该 skill 用于分析 QML Profiler trace，定位 Qt Quick/QML 性能问题。

## 覆盖范围

- 启动耗时。
- QML 对象创建。
- Binding 执行成本。
- JavaScript 热点。
- 绘制与渲染。
- 动画掉帧。
- Loader 和内存。

## 工作方式

1. 确认性能症状。
2. 获取 QML Profiler trace。
3. 解析 trace 中的热点事件。
4. 将热点映射到 QML 组件和文件。
5. 给出按影响排序的修复建议。
6. 建议修复后重新采集 trace 对比。

无 trace 时，不应声称已经确认根因。
