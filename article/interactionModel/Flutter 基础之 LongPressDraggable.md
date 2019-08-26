## 介绍

LongPressDraggable，它是Draggable的子类，使用方式基本和Draggable 一致，它和Draggable区别就是LongPressDraggable的手势识别需要长按才会触发。
可参考这篇文章: [《Flutter 基础之 Draggable》](https://github.com/YYFlutter/flutter-article/blob/master/article/interactionModel/Flutter%20%E5%9F%BA%E7%A1%80%E4%B9%8B%20Draggable.md)

## 继承关系
Object —> Diagnosticable —> DiagnosticableTree —> Widget —> StatefulWidget  —> Draggable<T> —> LongPressDraggable

## 构造函数
```
LongPressDraggable({Key key,
@required Widget child,
@required Widget feedback, 
T data, 
Axis axis,
Widget childWhenDragging, 
Offset feedbackOffset: Offset.zero,
DragAnchor dragAnchor: DragAnchor.child, 
int maxSimultaneousDrags, 
VoidCallback onDragStarted,
DraggableCanceledCallback onDraggableCanceled, 
DragEndCallback onDragEnd,
VoidCallback onDragCompleted, 
bool hapticFeedbackOnStart: true,
bool ignoringFeedbackSemantics: true })
```

可以看出它和Draggable的构造函数参数基本一致，主要有以下区别：
- hapticFeedbackOnStart 是否应在拖动开始时触发触觉的反馈。

## 常用属性

可以参考 [《Flutter 基础之 Draggable》](https://github.com/YYFlutter/flutter-article/blob/master/article/interactionModel/Flutter%20%E5%9F%BA%E7%A1%80%E4%B9%8B%20Draggable.md)


## 使用示例

可以参考 [《Flutter 基础之 Draggable》](https://github.com/YYFlutter/flutter-article/blob/master/article/interactionModel/Flutter%20%E5%9F%BA%E7%A1%80%E4%B9%8B%20Draggable.md)
