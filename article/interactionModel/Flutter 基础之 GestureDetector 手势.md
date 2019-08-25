### 介绍

GestureDetector是Flutter的手势检测器，它会尝试识别与其非null的回调相对应的手势。如果此Widget组件具有子控件，那么它的大小调整行为将遵从该子控件件。如果它没有子控件，那么它将变大以适合父控件。

默认情况下，带有不可见子控件的手势检测器会忽略触摸；可以通过行为控制此逻辑。GestureDetector还监听可访问性事件，并将其映射到callback回调。若要忽略可访问性事件，请将ExcludeFromSemantics设置为true。

Flutter中的手势系统有两个独立的层。第一层为原始指针(pointer)事件，它描述了屏幕上指针（例如，触摸、鼠标和触控笔）的位置和移动。 第二层为手势，描述由一个或多个指针移动组成的语义动作，如拖拽、缩放、双击、长按等。

### 手势

在flutter中，手势表示可以从多个单独的指针事件（甚至可能是多个单独的指针）识别的语义动作（例如点击，拖拽和缩放）。 完整的一个手势可以分发多个事件，对应于手势的生命周期（例如，拖拽开始，拖拽更新和拖拽结束）：

- 单击
    - onTapDown 指针已经在特定位置与屏幕接触
    - onTapUp 指针停止在特定位置与屏幕接触
    - onTap 单击事件触发
    - onTapCancel 先前指针触发的onTapDown不会在触发单击事件
    
- 双击
    - onDoubleTap 用户快速连续两次在同一位置轻敲屏幕.
- 长按
    - onLongPress 指针在相同位置长时间保持与屏幕接触
- 垂直拖拽
    - onVerticalDragStart 指针已经与屏幕接触并可能开始垂直移动
    - onVerticalDragUpdate 指针与屏幕接触并已沿垂直方向移动.
    - onVerticalDragEnd 先前与屏幕接触并垂直移动的指针不再与屏幕接触，并且在停止接触屏幕时以特定速度移动
- 水平拖拽
    - onHorizontalDragStart 指针已经接触到屏幕并可能开始水平移动
    - onHorizontalDragUpdate 指针与屏幕接触并已沿水平方向移动
    - onHorizontalDragEnd 先前与屏幕接触并水平移动的指针不再与屏幕接触，并在停止接触屏幕时以特定速度移动

### 继承关系

Object —> Diagnosticable —> DiagnosticableTree —> Widget —> StatelessWidget —> GestureDetector 

### 构造函数

 GestureDetector({Key key, Widget child, GestureTapDownCallback onTapDown, GestureTapUpCallback onTapUp, GestureTapCallback onTap, GestureTapCancelCallback onTapCancel, GestureTapDownCallback onSecondaryTapDown, GestureTapUpCallback onSecondaryTapUp, GestureTapCancelCallback onSecondaryTapCancel, GestureTapCallback onDoubleTap, GestureLongPressCallback onLongPress, GestureLongPressStartCallback onLongPressStart, GestureLongPressMoveUpdateCallback onLongPressMoveUpdate, GestureLongPressUpCallback onLongPressUp, GestureLongPressEndCallback onLongPressEnd, GestureDragDownCallback onVerticalDragDown, GestureDragStartCallback onVerticalDragStart, GestureDragUpdateCallback onVerticalDragUpdate, GestureDragEndCallback onVerticalDragEnd, GestureDragCancelCallback onVerticalDragCancel, GestureDragDownCallback onHorizontalDragDown, GestureDragStartCallback onHorizontalDragStart, GestureDragUpdateCallback onHorizontalDragUpdate, GestureDragEndCallback onHorizontalDragEnd, GestureDragCancelCallback onHorizontalDragCancel, GestureForcePressStartCallback onForcePressStart, GestureForcePressPeakCallback onForcePressPeak, GestureForcePressUpdateCallback onForcePressUpdate, GestureForcePressEndCallback onForcePressEnd, GestureDragDownCallback onPanDown, GestureDragStartCallback onPanStart, GestureDragUpdateCallback onPanUpdate, GestureDragEndCallback onPanEnd, GestureDragCancelCallback onPanCancel, GestureScaleStartCallback onScaleStart, GestureScaleUpdateCallback onScaleUpdate, GestureScaleEndCallback onScaleEnd, HitTestBehavior behavior, bool excludeFromSemantics: false, DragStartBehavior dragStartBehavior: DragStartBehavior.start }) 

### 常用属性

- dragStartBehavior → DragStartBehavior
确定处理拖拽开始行为的方式
- excludeFromSemantics → bool 是否从语义树中排除这些手势。
    
    例如，用于显示工具提示的长按手势被排除，因为工具提示本身直接包含在语义树中，因此具有显示它的手势将导致信息的重复。

- onDoubleTap → GestureTapCallback 用户已快速连续两次在同一位置使用主按钮轻触屏幕。

- onForcePressEnd → GestureForcePressEndCallback 指针不再与屏幕接触。
- onForcePressPeak → GestureForcePressPeakCallback 指针与屏幕接触并以最大力按下。力量至少是 ForcePressGestureRecognizer.peakPressure。
- onForcePressStart → GestureForcePressStartCallback 指针与屏幕接触，并用足够的力按压以启动压力。力量至少是 ForcePressGestureRecognizer.startPressure。
- onForcePressUpdate → GestureForcePressUpdateCallback 指针与屏幕接触，之前已经通过了 ForcePressGestureRecognizer.startPressure，并且要么在屏幕的平面上移动，要么用不同的力按压屏幕，要么同时按两个屏幕。
- onHorizontalDragCancel → GestureDragCancelCallback
先前触发onHorizontalDragDown的指针未完成触发了取消。
- onHorizontalDragDown → GestureDragDownCallback
指针已通过主按钮与屏幕接触，并可能开始水平移动。
- onHorizontalDragEnd → GestureDragEndCallback
之前与主屏幕接触并且水平移动的指针不再与屏幕接触，并且当它停止接触屏幕时以特定速度移动。
- onHorizontalDragStart → GestureDragStartCallback
指针已通过主按钮与屏幕接触，并开始水平移动。
- onHorizontalDragUpdate → GestureDragUpdateCallback
与主按钮接触并且水平移动的指针在水平方向上移动。
- onLongPress → GestureLongPressCallback
当识别出具有主按钮的长按手势时调用。
- onLongPressEnd → GestureLongPressEndCallback
使用主按钮触发长按的指针已停止接触屏幕。
- onLongPressMoveUpdate → GestureLongPressMoveUpdateCallback
使用主按钮长按后，指针已被拖动。
- onLongPressStart → GestureLongPressStartCallback
当识别出具有主按钮的长按手势时调用。
- onLongPressUp → GestureLongPressUpCallback
使用主按钮触发长按的指针已停止接触屏幕。
- onPanCancel → GestureDragCancelCallback
先前触发onPanDown的指针未完成。
- onPanDown → GestureDragDownCallback
指针已通过主按钮与屏幕接触，并可能开始移动。
- onPanEnd → GestureDragEndCallback
先前通过主按钮与屏幕接触并且移动的指针不再与屏幕接触，并且当它停止接触屏幕时以特定速度移动。
- onPanStart → GestureDragStartCallback
触摸点与屏幕接触，并已开始移动。
- onPanUpdate → GestureDragUpdateCallback
屏幕上的触摸点位置每次改变时，都会触发该回调。
- onScaleEnd → GestureScaleEndCallback
指针不再与屏幕接触。
- onScaleStart → GestureScaleStartCallback
与屏幕接触的指针已建立焦点，初始比例为1.0。

- onScaleUpdate → GestureScaleUpdateCallback
与屏幕接触的指针表示新的焦点和/或比例。

- onSecondaryTapCancel → GestureTapCancelCallback
先前触发onSecondaryTapDown的指针不会最终导致点击。

- onSecondaryTapDown → GestureTapDownCallback
可能导致使用辅助按钮敲击的指针已在特定位置与屏幕联系。
- onSecondaryTapUp → GestureTapUpCallback
将触发带有辅助按钮的敲击的指针已停止在特定位置接触屏幕。
- onTap → GestureTapCallback
带主按钮的点击事件触发源头。
- onTapCancel → GestureTapCancelCallback
先前触发onTapDown的指针不会导致点击。
- onTapDown → GestureTapDownCallback
可能导致使用主按钮敲击的指针已在特定位置与屏幕联系。
- onTapUp → GestureTapUpCallback
将触发带主按钮的敲击的指针已停止在特定位置接触屏幕。
- onVerticalDragCancel → GestureDragCancelCallback
先前触发onVerticalDragDown的指针未完成。
- onVerticalDragDown → GestureDragDownCallback
指针已通过主按钮与屏幕接触，并可能开始垂直移动。
- onVerticalDragEnd → GestureDragEndCallback
先前与主屏幕接触并且垂直移动的指针不再与屏幕接触，并且当它停止接触屏幕时以特定速度移动。
- onVerticalDragStart → GestureDragStartCallback
指针已通过主按钮与屏幕接触，并已开始垂直移动。
- onVerticalDragUpdate → GestureDragUpdateCallback
与主按钮接触并且垂直移动的指针在垂直方向上移动。

### 常用方法

- build（BuildContext context） → Widget
创建组件。
- debugFillProperties（DiagnosticPropertiesBuilder 属性） →void
添加与节点关联的其他属性。
- createElement（） → StatelessElement
创建StatelessElement以管理此组件在UI树中的位置。


### 使用示例

#### 1. 单击、双击、长按事件

这里通过一个demo，用GestureDetector对Container组件进行手势识别。在触发相应事件后，Container上显示事件名，为了增大点击区域，将Container设置为200×200，代码如下：

```
import 'package:flutter/material.dart';

class GestureDetectorTestRoute extends StatefulWidget {
  @override
  _GestureDetectorTestRouteState createState() =>
      new _GestureDetectorTestRouteState();
}

class _GestureDetectorTestRouteState extends State<GestureDetectorTestRoute> {
  String _operation = "No Gesture detected!"; 
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      key: _scaffoldKey,
      appBar: AppBar(
        title: Text("GestureDetectorTest"),
      ),
      body: Center(
        child: GestureDetector(
          child: Container(
            alignment: Alignment.center,
            color: Colors.blue,
            width: 200.0,
            height: 200.0,
            child: Text(
              _operation,
              style: TextStyle(
                  color: Colors.white,
                  fontSize: 14,
                  decoration: TextDecoration.none),
            ),
          ),
          onTap: () => updateText("onTap"), //单击
          onDoubleTap: () => updateText("onDoubleTap"), //双击
          onLongPress: () => updateText("onLongPress"), //长按
        ),
      ),
    );
  }

  //更新文本
  void updateText(String text) {
    setState(() {
      _operation = text;
    });
    //提示
    showSnackBar(text);
  }

  var _scaffoldKey = new GlobalKey<ScaffoldState>();

  void showSnackBar(String message) {
    var snackBar = SnackBar(
        content: Text(message),
        backgroundColor: Colors.lightGreen,
        duration: Duration(milliseconds: 400));
    _scaffoldKey.currentState.showSnackBar(snackBar);
  }
}

```

效果图如下：

![GestureDetector](https://mmbiz.qpic.cn/mmbiz_gif/Itr76Nia97dqhYlStHHlDqrGP5x11yrZzibUybyA3Fia6lfasY2nxa21SAMsE14Z1uKe4pqDQfkPEXZlSIklmWicmA/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

注意： 若同时监听onTap和onDoubleTap事件，当用户触发tap事件时，会有200毫秒左右的延时。这是因为当用户点击完之后很可能会再次点击以触发双击事件，所以GestureDetector源码内部会等200毫秒时间来确定是否为双击事件。如果用户只监听了onTap（没有监听onDoubleTap）事件则回调没有延时。


#### 2. 拖拽、滑动事件

```
import 'package:flutter/material.dart';

class DragTest extends StatefulWidget {
  @override
  _DragTestState createState() => new _DragTestState();
}

class _DragTestState extends State<DragTest>
    with SingleTickerProviderStateMixin {
  double _top = 0.0; //距顶部的偏移
  double _left = 0.0; //距左边的偏移

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("DragTest"),
      ),
      body: Stack(
        children: <Widget>[
          Positioned(
            top: _top,
            left: _left,
            child: GestureDetector(
              child: CircleAvatar(
                  child: Text("Draggable Text", textAlign: TextAlign.center),
                  radius: 50),
              //手指按下时会触发此回调
              onPanDown: (DragDownDetails e) {
                //打印手指按下的位置(屏幕)
                print("用户手指按下：${e.globalPosition}");
              },
              //手指滑动时会触发此回调
              onPanUpdate: (DragUpdateDetails e) {
                //用户手指滑动时，更新偏移，重新构建
                setState(() {
                  _left += e.delta.dx;
                  _top += e.delta.dy;
                });
              },
              onPanEnd: (DragEndDetails e) {
                //打印滑动结束时在x、y轴上的速度
                print(e.velocity);
              },
            ),
          )
        ],
      ),
    );
  }
}

```

效果图如下：

![Drag](https://mmbiz.qpic.cn/mmbiz_gif/Itr76Nia97dqhYlStHHlDqrGP5x11yrZzMstZyq0xwwP1ar7bJDHX6737jHoTQEq2I81Vkn84Op7Gic58rma0Pkg/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

#### 3. 缩放事件

除了单击/双击/拖拽等事件，GestureDetector可以监听缩放事件。下面我们演示一个简单的图片缩放效果，示例代码如下：

```
class _ScaleTestRouteState extends State<_ScaleTestRoute> {
  double _width = 200.0; //通过修改图片宽度来达到缩放效果

  @override
  Widget build(BuildContext context) {
   return Center(
     child: GestureDetector(
        //指定宽度，高度自适应
        child: Image.asset("./images/sea.png", width: _width),
        onScaleUpdate: (ScaleUpdateDetails details) {
          setState(() {
            //缩放倍数在0.8到10倍之间
            _width=200*details.scale.clamp(.8, 10.0);
          });
        },
      ),
   );
  }
}
```

效果图如下：
![Scale](https://mmbiz.qpic.cn/mmbiz_gif/Itr76Nia97dpAwUAG87p3clibWOOyXKBJUnu2zibLK6JEqsffjoVNwiasicZroKmODicdpc0E8ZvLpQyuxklQEzAic7Qw/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

### 总结

 通过这篇文章，我们了解了flutter 所提供的GestureDetector手势检测器的一些基本概念及能力，它内部封装了诸多API，让我们可以很高效快速开发应用。通过文章的内容讲述，我们知道如何去监听单击/双击/拖拽等事件及处理用户的交互逻辑。当然，触摸交互模型里面不可避免地会出现事件竞争和事件冲突问题，本篇文章由于篇幅问题就没有进行讲解了，下篇文章我们将会侧重讲述flutter中的事件竞争及冲突问题。