# QML 性能反模式

## 对象创建过多

症状：启动或页面切换时 Creating 事件耗时高。

常见原因：

- delegate 太重。
- 一次性加载大量不可见组件。
- 未使用 Loader 延迟加载。

建议：

- 拆分重组件。
- 使用 Loader 按需加载。
- 静态小列表用 `Repeater`，大列表优化 delegate。

## 热绑定成本高

症状：Binding 事件频繁且耗时。

常见原因：

- 绑定中调用函数。
- 绑定中执行复杂 JavaScript。
- 绑定依赖过多属性。

建议：

- 使用 `readonly property` 缓存计算。
- 把复杂逻辑移到 C++ 或模型层。
- 减少不必要依赖。

## JavaScript 热点

症状：JavaScript 事件占用高。

建议：

- 避免循环中创建对象或正则。
- 使用 `let` / `const`。
- 将重计算移出 UI 线程。

## 渲染成本高

常见原因：

- `clip: true`。
- 复杂子树上使用 `opacity`。
- `layer.enabled`。
- 多个 ShaderEffect。
- 频繁 Canvas 重绘。

建议：

- 仅在必要时 clip。
- 尽量在叶子节点使用 alpha。
- 避免动画 Canvas；静态复杂图形可接受。
- 减少 offscreen pass。

## 图片内存浪费

原因：图片未设置 `sourceSize`，导致大图按原尺寸解码。

建议：按显示尺寸设置 `sourceSize`，网络或大图使用 `asynchronous: true`。

## 动画导致布局抖动

原因：动画 `width` / `height` 触发布局重算。

建议：优先动画 `scale`、`opacity`、`x`、`y`，并使用 Animator 类型。
