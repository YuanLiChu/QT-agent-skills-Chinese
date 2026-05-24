# Qt6 QML 审查清单

该清单对应 `qt-qml-review` 的规则来源，供 linter 和语义审查共同使用。

## 1. Imports

- `IMP-1`：Qt 6 中 `QtQuick` 已包含 Window 类型，不要重复导入 `QtQuick.Window`。
- `IMP-2`：Qt 6 import 不写版本号，避免限制 API 面并影响 `qmlsc`。
- `IMP-3`：定制 Controls 时使用具体 style，如 `QtQuick.Controls.Basic`。
- `IMP-4`：import 按 Qt 模块、第三方、本地 C++、QML 文件夹排序。
- `IMP-5`：不使用已废弃的 `Qt.include()`。
- `IMP-6`：移除重复 import。

## 2. Attribute Ordering

对象内部属性顺序应为：

1. `id`
2. property / required property
3. signal
4. 普通属性赋值
5. attached properties
6. states
7. transitions
8. signal handlers
9. child objects
10. JavaScript functions

## 3. Bindings & Properties

- 避免 `property var`，优先使用具体类型。
- JavaScript 赋值会破坏绑定。
- `Qt.binding()` 使用箭头函数。
- 避免 `list<>` 绑定到昂贵计算。
- 关注绑定循环、alias 链、裸属性访问和缺失 `pragma ComponentBehavior: Bound`。

## 4. Layout & Anchoring

- 不混用 anchors 和 `Layout.*`。
- Layout 子项不直接设置 `width` / `height` / `x` / `y`。
- 四边锚定优先 `anchors.fill: parent`。
- 不锚定到不可见对象。
- 不通过 `parent.parent` 跨分支锚定。

## 5. Loader & Dynamic Creation

- 访问 `Loader.item` 前检查 `status`。
- 不使用字符串形式 `Qt.createComponent()`。
- 不使用 `Qt.createQmlObject()` 动态解析字符串。
- `source` 和 `sourceComponent` 不同时设置。
- `createObject()` 必须管理生命周期。

## 6. ListView & Delegates

- delegate 使用 `required property` 声明角色。
- `reuseItems: true` 时不能用 JS `var` 保存状态。
- 不在 delegate `Component.onCompleted` 中直接 `connect()`。
- 复用 delegate 时不要依赖 `Component.onCompleted` 初始化。
- 使用 required property 后，`index` 也需要显式声明。

## 7. States & Transitions

- Qt 6 使用 `PropertyChanges { item.property: value }`。
- `Transition` 明确 `from` / `to`。
- 可复用组件中内部 states 可考虑 `StateGroup`。
- `PropertyChanges` 使用声明式 `:`，不使用 imperative `=`。

## 8. Images

- Image 设置 `sourceSize`。
- 网络图片设置 `asynchronous: true`。
- 动态图片源需要处理 `Image.status`。

## 9. Performance & Rendering

- 透明 `Rectangle` 用 `Item` 替代。
- `opacity: 0` 不等同于不可见，非动画场景用 `visible: false`。
- `clip: true` 不是优化，会增加渲染成本。
- 不动画 `font.pixelSize`。
- 不必要时避免 `Text.RichText`。
- 谨慎使用 `layer.enabled`。
- 热绑定中避免函数调用。

## 10. Style & Conventions

- 顶层组件应有 `id: root`。
- 同一 group 的多个子属性使用 group notation。
- id 使用 lowerCamelCase。
- 不添加未使用 id。
- 可复用组件使用 `implicitWidth` / `implicitHeight`。

## 11. Signals & Connections

- `Connections` 明确 `target`。
- 使用 `function onFoo()`，不要旧式 `onFoo:`。
- 不混用两种 Connections handler 语法。
- signal 向上通知，function 向下调用。

## 12. Error Handling & Security

- 不硬编码 `http://`。
- 不硬编码 Unix 路径，如 `/tmp/`。

## 13. JavaScript Quality

- 使用 `let` / `const`，不用 `var`。
- 使用 `===` / `!==`。
- 不使用 `eval` 等动态执行。
- 尽量减少复杂 JS，重逻辑放到 C++。

## 14. C++ Integration

- 避免 `rootContext()->setContextProperty()`。
- singleton 用于 API 或常量，不作为共享数据存储。
- QML/C++ 边界注意对象 ownership。

## 15. Migration

- Qt 5 Connections 旧语法迁移为函数语法。
- Qt 5 PropertyChanges target 语法迁移为 Qt 6 推荐语法。
- `QtGraphicalEffects` 迁移到 Qt 6 可用方案。
- 注意 `Binding.restoreMode` 默认值变化。
- 优先考虑 Pointer Handlers 替代 MouseArea。
