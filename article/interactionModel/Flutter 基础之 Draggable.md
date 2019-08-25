## 介绍
Draggable 是Flutter中的一个可以拖拽到DragTarget的Widget。并且，他可以把自己携带的数据传递给DragTarget。当Draggable被拖动到DragTarget的时候，DragTarget会判断是不是需要接收传递过来的数据，在接收后做相应的状态改变。

## 继承关系
 
 Object -> Diagnosticable -> DiagnosticableTree -> Widget  ->StatefulWidget -> Draggable 
 
## 构造函数

```
 Draggable({Key key, 
 @required Widget child,
 @required Widget feedback,
 T data, 
 Axis axis,
 Widget childWhenDragging,
 Offset feedbackOffset: Offset.zero, 
 DragAnchor dragAnchor: DragAnchor.child, 
 Axis affinity, 
 int maxSimultaneousDrags,
 VoidCallback onDragStarted, 
 DraggableCanceledCallback onDraggableCanceled, 
 DragEndCallback onDragEnd, 
 VoidCallback onDragCompleted, 
 bool ignoringFeedbackSemantics: true }) 
 ```
 
## 常用属性

- affinity → Axis
   控制此窗口小部件如何与其他手势竞争以启动拖动。
- axis → Axis
   限制此可拖动移动的轴（如果有指定）。
- child → Widget
    子控件。
- childWhenDragging → Widget
    当一个或多个拖动操作正在进行时，所要显示的控件而不是子控件。
- data → T 表示要传入DragTarget 的数据。
- dragAnchor → DragAnchor
    在拖动过程中，所应该指定此Widget的位置。
- feedback → Widget
    当拖动正在进行时，指定在当前Point下所显示的Widget。
- feedbackOffset → Offset
    feedbackOffset可用于设置命中测试目标点，以便找到拖动的目标。如果将反馈与子控件相比进行转换，则尤其有用。
- ignoringFeedbackSemantics → bool
   构建语义树的时候，是否忽略反馈Widget的语义。
- maxSimultaneousDrags → int
  最大支持多少个同时拖动的Widget。
- onDragCompleted → VoidCallback
    当Draggable被DraggTarget移除并接受时调用，表示拖拽完成。
- onDragEnd → DragEndCallback
   当Draggable被DraggTarget移除时调用。
- onDraggableCanceled → DraggableCanceledCallback
     当Draggable被DraggTarget移除时并且不被接受时调用，表示拖拽被取消。
- onDragStarted → VoidCallback
    当 draggable 开始被拖拽时调用。 

## 常用方法

- createRecognizer(GestureMultiDragStartCallback onStart) → 创建一个识别拖动开始的手势识别器。
- createState() → _DraggableState<T>
  在树中的给定位置为此Widget创建可变状态。

## 使用示例

示例1：

![draggable.gif](https://upload-images.jianshu.io/upload_images/4835249-e74967e05f4576d0.gif?imageMogr2/auto-orient/strip)

代码如下：

```java
import 'package:flutter/material.dart';

class DraggableTest extends StatefulWidget {
  @override
  State<StatefulWidget> createState() {
    return DraggableState();
  }
}

class DraggableState extends State<DraggableTest> {
  Offset _offset = Offset(100, 100);
  double _width = 120.0;
  String url =
      "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1564055541946&di=6da25e7ef3c905ce81d5e75694b62c19&imgtype=0&src=http%3A%2F%2Fimg4q.duitang.com%2Fuploads%2Fitem%2F201407%2F02%2F20140702203112_BGFPv.thumb.700_0.jpeg";

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          title: Text("DraggableDemo"),
        ),
        body: Transform.translate(
            offset: _offset,
            child: Draggable(
              child: Image.network(url, width: _width),
              feedback: Image.network(url, width: _width),
              childWhenDragging: Image.network(url, width: _width),
              onDraggableCanceled: (v, o) {
                setState(() {
                  _offset = o;
                  print("dx:" + o.dx.toString());
                  print("dy:" + o.dy.toString());
                });
              },
              onDragCompleted: () {
                print("onDragCompleted");
              },
              onDragEnd: (dragEndDetails) {
                setState(() {
                  _offset = dragEndDetails.offset;
                });
                print("onDragEnd");
                print(" dragEndDetails.offset:" +
                    dragEndDetails.offset.toString());
              },
            )));
  }
}

```


除此之外，我们也可以修改一下代码，childWhenDragging参数传入一个不可见的Widget，用于实现类似于GestureDetector 的拖拽平移功能。

示例2：

![draggable2.gif](https://upload-images.jianshu.io/upload_images/4835249-be9a737c6fbf3803.gif?imageMogr2/auto-orient/strip)


代码如下：

```java
import 'package:flutter/material.dart';

class DraggableTest extends StatefulWidget {
  @override
  State<StatefulWidget> createState() {
    return DraggableState();
  }
}

class DraggableState extends State<DraggableTest> {
  Offset _offset = Offset(100, 100);
  double _size = 150.0;
  String url =
      "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1564055541946&di=6da25e7ef3c905ce81d5e75694b62c19&imgtype=0&src=http%3A%2F%2Fimg4q.duitang.com%2Fuploads%2Fitem%2F201407%2F02%2F20140702203112_BGFPv.thumb.700_0.jpeg";

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          title: Text("DraggableDemo"),
        ),
        body: Transform.translate(
            offset: _offset,
            child: Draggable(
              child: Image.network(url, width: _size),
              feedback: Image.network(url, width: _size),
              childWhenDragging: Container(
                width: 0,
                height: 0,
              ),
              onDragEnd: (dragEndDetails) {
                setState(() {
                  _offset = dragEndDetails.offset;
                  print(" onDragEnd - dragEndDetails.offset:" +
                      dragEndDetails.offset.toString());
                });
              },
            )));
  }
}

```

**log 输出**：

```
2019-08-09 17:01:18.492 15029-15061/com.xiaosong.flutterwidgets I/flutter: onDragStarted
2019-08-09 17:01:20.091 15029-15061/com.xiaosong.flutterwidgets I/flutter:  onDragEnd - dragEndDetails.offset:Offset(57.7, 370.0)
2019-08-09 17:01:20.091 15029-15061/com.xiaosong.flutterwidgets I/flutter: dx:57.66666666666674, dy:370.0000000000001
2019-08-09 17:01:23.385 15029-15061/com.xiaosong.flutterwidgets I/flutter: onDragStarted
2019-08-09 17:01:23.878 15029-15061/com.xiaosong.flutterwidgets I/flutter:  onDragEnd - dragEndDetails.offset:Offset(114.0, 274.3)
2019-08-09 17:01:23.878 15029-15061/com.xiaosong.flutterwidgets I/flutter: dx:114.00000000000007, dy:274.3333333333334
```

从log 可以看到，如果没有与DragTarget 配合使用，它不会触发 onDragCompleted 或者 onDraggableCanceled 回调。而onDragStarted、onDragEnd 依旧会触发。

## 总结

本篇文章我们大致讲解了Draggable的基本概念及常用示例。由于Draggable 没有 GestureDetector中类似onPanUpdate的监听，因此触发onDragEnd 的position 并不是非常精准。若我们需要拖拽平移Widget，一般来说还是建议通过GestureDetector去实现，Draggable一般是搭配DragTarget去使用的。下篇文章我们将讲解如何搭配DragTarget来实现拖拽状态并改变数据。