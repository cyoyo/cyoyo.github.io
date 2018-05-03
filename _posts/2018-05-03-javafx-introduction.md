---
layout: post
title:  "JavaFX - Introduction"
date:   2018-05-02 17:12:00
categories: MindNote
tags: [blog, jekyll]
---

> JavaFX 是一个强大的图形和多媒体处理工具包集合，它允许开发者来设计、创建、测试、调试和部署`富客户端程序 （Rich Internet Applications, RIAs）`，并且和 Java 一样跨平台。 —— [JavaFX 中文文档](http://www.javafxchina.net/blog/docs/tutorial1/)

## 学习资源
- [Oracle 官方文档](https://docs.oracle.com/javase/8/javase-clienttechnologies.htm)
- [JavaFX China](http://www.javafxchina.net/main/) - JavaFX、OSGi、Eclipse 开源资料
- [JavaFX 8 API](https://docs.oracle.com/javase/8/javafx/api/) - JavaFX 类的文档
- [ControlsFX API](https://controlsfx.bitbucket.io/) - [ControlsFX project](http://fxexperience.com/controlsfx/) - 额外 JavaFX 控件的文档
- 网络教程资源：[code.markery](http://code.makery.ch/library/javafx-8-tutorial/zh-cn/)、[易百教程](https://www.yiibai.com/javafx/)、[tutorialspoint](https://www.tutorialspoint.com/javafx/index.htm)

## 开发环境准备
- 最新的 Java JDK 8 （包含 JavaFX 8）。
- Eclipse 4.3 或更高版本与 [e(fx)clipse 插件](http://www.eclipse.org/efxclipse/index.html)，使用 Install New Software 功能从[Update Site](https://projects.eclipse.org/projects/technology.efxclipse/downloads) 安装。
- [Scene Builder 2.0](http://www.oracle.com/technetwork/java/javase/downloads/javafxscenebuilder-info-2157684.html) 或更高。
- 如果遇到 Eclipse Access Restrictions 问题，需要在 Build Path 设置中对 JRE System Library 添加 Access Rule 配置，解除访问限制。
<!-- more -->
## JavaFX 架构
JavaFX 的架构如下图所示，底层是 JVM 和 JDK，顶层则是对外提供的 `JavaFX Public APIs` 和`场景图（Scene Graph）`。在 Public APIs 之下便是代码运行引擎，它由几大部分组成：
- 性能图形引擎（Prism）
- 简洁高效的窗体系统（Glass）
- 媒体引擎
- web 引擎

![@JavaFX 架构图 | JavaFX 架构图](/img/1525332949554.png)
#### JavaFX Public APIs
提供了一套支持富客户端应用（RIAs）开发的完整 Java API 集合。

#### 场景图 Scene Graph
`场景图（Scene Graph）`是构建 JavaFX 应用的入口，它是一个层级结构的节点树，<span style="border-bottom:2px solid;">表示了所有用户界面的视觉元素</span>，可以处理输入，并且可以被渲染。
- 场景图中的一个元素即为一个`节点（Node）`，每个节点都有一个 ID、样式类和包围盒（bounding volume）包含了各种视觉属性（模糊、透明度、变换等）、事件处理器（Event handlers，例如鼠标、键盘和输入法）、应用相关的状态（Application-specific state）。

#### 图形系统 Graphics System
图中蓝色部分是 JavaFX 的图形系统（Graphics System），是在 JavaFX 场景图层之下的实现细节。其中：
- `Prism` 用于处理渲染工作。
- `Quantum Toolkit` 将 Prism 和 Glass Windowing ToolKit 绑在一起，使得它们可以被其上层的 JavaFX层使用，它也负责管理与渲染有关的事件处理的线程规则。

#### 窗体工具包 Glass
`Glass 窗体工具包`（Glass Windowing Toolkit）提供了本地操作服务，例如窗体、计时器、皮肤等。它是连接 JavaFX 层与本地操作系统的平台无关层，同时还负责管理事件队列。

#### 多媒体和图像
通过 `javafx.scene.media API` 可以访问 JavaFX 的多媒体功能，支持视频和音频媒体。

#### Web组件
Web 组件（Web Component）是一个基于 Webkit 的 JavaFX UI 控件，提供了一个 Web Viewer，并通过其API 提供了完全的浏览功能，同时 Java 和 JavaScript 可以互相调用。

#### CSS
层叠样式表（CSS）提供了在不修改应用程序代码的情况下自定义应用程序外观的能力。

#### UI 控件
JavaFX UI 控件通过场景图中的节点来构建，支持多种操作系统，并可以用 CSS 进行主题和风格控制。

#### 布局
布局容器（Layoutcontainer）或面板（Pane）允许对应用程序场景图中的 UI 控件进行灵活、动态的排布。为了获得理想的布局结构，可以在应用中嵌套使用各类布局。

#### 2D 和 3D 变换
场景图中的每个节点都可以使用下面的 `javafx.scene.tranform` 包中的类来进行 x-y 坐标系变换。

## Key Features

#### 1. Java API
JavaFX 是一个 Java 库，其 API 对基于 JVM 的语言也是友好的，例如 JRuby 和 Scala。
#### 2. FXML 与 Scene Builder
`FXML` 是一种基于 XML 的声明式标记语言，用于描述 JavaFX 应用程序的用户界面。设计师可以在 FXML 中编码或者使用 `JavaFX Scene Builder` 来交互式地设计图形用户接口（GUI）。
#### 3. WebView
这是一个使用了 WebKitHTML 技术的 Web 组件，可用于在 JavaFX 应用程序中嵌入 Web 页面。在 `WebView 中运行的 JavaScript 可以方便地调用 JavaAPI`，而 `JavaAPI 也可以调用 WebView 中的 JavaScript`。JavaFX8 中增加了对 HTML5 的支持。
#### 4. 与 Swing 互操作
现有的 Swing 程序可以使用 JavaFX 获得新特性，例如多媒体播放和 Web 内容嵌入。JavaFX 程序可以使用 SwingNode 类嵌入 Swing 内容。
#### 5. 内置的 UI 控件和 CSS
提供了开发一个应用程序所需的主要控件，这些组件可以使用 CSS 来控制样式。
#### 6. Modena 主题
JavaFX8 提供了新的 `Modena 主题`来替换原来的 Caspian 主题。
#### 7. 3D 图像处理能力
JavaFX8 的 3D 图像处理 API 中加入了一些新的 API，原有的 Camera 类 API 也得到了更新。
#### 8. Canvas API
通过 `Canvas API` 可以在 JavaFX 场景（Scene）中直接绘图。
#### 9. Printing API 
JavaFX8 中加入了 print 包并且提供了打印功能公共类。
#### 10. Rich Text 支持
提供了强大的文本支持能力，包括双向文字（例如阿拉伯语）、复杂文字脚本，并且支持多行、多种风格的文本节点。
#### 11. 多点触摸
提供了对多点触摸的支持。
#### 12. Hi-DPI 支持
JavaFX8 开始支持 `Hi-DPI` 显示。
#### 13. 图形渲染硬件加速
JavaFX 图像均基于图形渲染流水线（`Prism`）。实现了更为平滑的图像效果并且支持GPU 渲染加速。
#### 14. 高性能多媒体引擎
提供了一个基于 GStreamer 多媒体框架的稳定、低延迟的多媒体处理框架。
#### 15. 自包含的应用部署模型
自包含应用包具有应用所需的所有资源、包括一个 Java 和 JavaFX 运行时的私有拷贝。它们可作为操作系统原生安装包发布，并提供与原生应用相同的安装和运行体验。


