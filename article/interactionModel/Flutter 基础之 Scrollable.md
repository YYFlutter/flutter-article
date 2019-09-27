## 介绍
Scrollable实现了一个可滚动 Widget 的交互模型，包括手势识别。但对如何构造实际显示子对象的视图，则没有明确定义。
实际上，在flutter里面很少直接构造Scrollable的。通常情况下，都是考虑ListView或GridView，它结合滚动、视图接口和布局模型。如果要组合布局模型（或使用自定义布局模式），则可以考虑使用CustomScrollView。 


若要使用Scrollable进一步自定义滚动行为：

1. 可以提供viewportBuilder 来自定义子模型。例如，SingleChildScrollView使用显示单个框子项的视口，而CustomScrollView使用Viewport 或 ShrinkWrappingViewport，两者都显示子列表。

2. 可以提供自定义ScrollController，以创建自定义 ScrollPosition子类。例如，PageView使用 PageController，它创建一个面向页面的滚动位置子类，在Scrollable调整大小时保持同一页面可见。


## 继承关系

Object -> Diagnosticable -> DiagnosticableTree -> Widget -> StatefulWidget -> Scrollable

## 构造函数

```dart
Scrollable({ Key key， 
AxisDirection axisDirection：AxisDirection.down，
ScrollController controller，
ScrollPhysics physics，
@ required ViewportBuilder viewportBuilder，
bool excludeFromSemantics：false， 
int semanticChildCount， DragStartBehavior dragStartBehavior：DragStartBehavior.start 
})
```

## 常用属性


- axisDirection → AxisDirection
滚动的方向。

- controller → ScrollController
控制器，可用于控制滚动此Widget的位置。

- dragStartBehavior → DragStartBehavior
确定处理拖动开始行为的方式。

- excludeFromSemantics → bool
此Scrollable引入的滚动操作是否在语义树中公开。

- physics → ScrollPhysics
应如何响应用户输入。

- semanticChildCount → int
提供语义信息的子控件数量。

- viewportBuilder → ViewportBuilder
构建可通过其显示可滚动内容的窗口。

## 常用方法

- createState（） → ScrollableState
在树中的给定位置为此窗口小部件创建可变状态。

- ensureVisible(BuildContext context，{ double alignment：0.0， Duration duration：Duration.zero， Curve curve：Curves.ease }) → Future < void >
滚动包含给定 context 的滚动条，让给定的 context 可见。

## 使用示例

 可参考系统源码 SingleChildScrollView、CustomScrollView。