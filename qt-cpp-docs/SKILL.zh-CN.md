---
name: qt-cpp-docs
description: 为 Qt C++ 类、模块、方法和 Q_PROPERTY/Q_SIGNAL/Q_SLOT 生成面向开发者的文档。
metadata:
  author: qt-ai-skills
  version: "1.0"
  qt-version: "6.x"
  category: documentation
---

# Qt C++ 文档 Skill（中文版）

## 适用场景

当用户要求为 Qt/C++ 源码生成或更新文档时使用，包括：

- QObject 派生类
- QML 暴露类型
- Model/View 类
- Widgets 类
- 工具类、模块 API、公共方法

## 文档原则

- 先阅读头文件和实现文件。
- 遵循项目已有文档风格。
- 不编造 API，不猜测未在代码中体现的行为。
- 解释类的职责、线程要求、所有权、生命周期和 QML 暴露方式。

## 推荐结构

### 概览

说明类/模块是什么、属于项目哪个层次、解决什么问题。

### 何时使用

说明调用者在什么场景下使用该类。

### Public API

列出：

- 构造函数
- public 方法
- `Q_PROPERTY`
- `Q_SIGNAL`
- `Q_SLOT`
- enum / flag

每个条目说明参数、返回值、副作用、错误处理和线程要求。

### QML 集成

如果类暴露给 QML，说明：

- 使用 `QML_ELEMENT`、`QML_NAMED_ELEMENT`、singleton 等方式。
- QML 可见属性和信号。
- ownership 和 parent 约束。

### 生命周期与所有权

说明对象由谁创建、谁销毁、是否 parented、是否可跨线程。

### 线程模型

说明对象必须在哪个线程使用，信号槽连接是否跨线程，是否需要 queued connection。

### 示例

给出简洁示例，代码应与真实 API 一致。

## 注意事项

- 不要把私有 helper 当公共 API。
- 对 Model/View 类要说明 role、rowCount、data、setData、dataChanged 语义。
- 对 QWidget 或 QQuickItem 类要说明关键事件处理或渲染路径。
- 对异步类要说明完成信号、错误信号和取消策略。
