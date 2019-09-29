本篇文章已授权微信公众号 `YYGeeker` 独家发布转载请标明出处

## 控件介绍

1. `AnimatedCrossFade`存放着两个动画的容器，只要切换动画的状态，就能表现出对应的动画效果
2. `AnimatedCrossFade`本质就是一个Stack分别存放有两个组件和两个动画，

## 构造函数

```java
const AnimatedCrossFade({
    Key key,
    @required this.firstChild,                    //第一个动画元素
    @required this.secondChild,                   //第二个动画元素
    this.firstCurve = Curves.linear,              //第一个动画元素的插值器
    this.secondCurve = Curves.linear,             //第二个动画元素的插值器
    this.sizeCurve = Curves.linear,               //动画切换时候的尺寸变化插值器
    this.alignment = Alignment.topCenter,         //动画切换后的对齐方式
    @required this.crossFadeState,                //动画当前的状态
    @required this.duration,                      //动画时长
    this.layoutBuilder = defaultLayoutBuilder,    //动画布局的构造器
  }) 
```

## 常用属性

1、firstChild

* 第一个动画元素的控件

```
firstChild: FlutterLogo(
    style: FlutterLogoStyle.horizontal,
    size: 100.0,
  ),
```

2、secondChild

* 第二个动画元素的控件

```
secondChild: FlutterLogo(
    style: FlutterLogoStyle.stacked,
    size: 200.0,
  ),
```

3、firstCurve

* 第一个动画元素的插值器

```
firstCurve: Curves.fastOutSlowIn,
```

4、secondCurve

* 第二个动画元素的插值器

```
secondCurve: Curves.fastOutSlowIn,
```

5、sizeCurve

* 动画切换时候的尺寸变化插值器

```
sizeCurve: Curves.fastOutSlowIn,
```

6、alignment

* 动画在切换到第二个状态的时候，当前alignment的参数会应用在第二个动画元素中

```
alignment: AlignmentDirectional(0.0, 1.0),
```

7、crossFadeState

* 动画当前的状态，当状态变化时，动画也会随之切换到对应的元素上

```
crossFadeState:
      _first ? CrossFadeState.showFirst : CrossFadeState.showSecond,
```

8、duration

* 动画时长

```
duration: Duration(seconds: 1),
```

9、layoutBuilder

* 动画布局的构造器，可以构建两个动画元素之间的布局关系

源码默认帮我们实现了`defaultLayoutBuilder`，我们可以跟进去源码

```dart
static Widget defaultLayoutBuilder(Widget topChild, Key topChildKey, Widget bottomChild, Key bottomChildKey) {
    return Stack(
      overflow: Overflow.visible,
      children: <Widget>[
        Positioned(
          key: bottomChildKey,
          left: 0.0,
          top: 0.0,
          right: 0.0,
          child: bottomChild,
        ),
        Positioned(
          key: topChildKey,
          child: topChild,
        ),
      ],
    );
  }
```

其实就是通过Stack控件将两个动画元素叠加起来，从而去控制他们的显示和隐藏，形成动画

## 效果图

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190729215147330.gif)

## 源代码

```dart
import 'dart:async';

import 'package:flutter/material.dart';

var time = 0;
var _first = true;

class Day7 extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      theme: ThemeData(
        primaryColor: Colors.white,
      ),
      home: WeWidget(),
    );
  }
}

class WeWidget extends StatefulWidget {
  @override
  State<StatefulWidget> createState() {
    return WeWidgetState();
  }
}

class WeWidgetState extends State<WeWidget> {
  WeWidgetState() {
    Timer.periodic(Duration(seconds: 1), (timer) {
      setState(() {
        switch (time % 4) {
          case 0:
            _first = false;
            break;
          case 2:
            _first = true;
            break;
        }
        time++;
      });
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("day7"),
      ),
      body: _buildColumn(),
    );
  }

  Widget _buildColumn() {
    return Column(
      children: <Widget>[
        AnimatedCrossFade(
          //layoutBuilder: ,
          alignment: AlignmentDirectional(0.0, 1.0),
          duration: Duration(seconds: 1),
          firstCurve: Curves.fastOutSlowIn,
          secondCurve: Curves.fastOutSlowIn,
          sizeCurve: Curves.fastOutSlowIn,
          firstChild: FlutterLogo(
            style: FlutterLogoStyle.horizontal,
            size: 100.0,
          ),
          secondChild: FlutterLogo(
            style: FlutterLogoStyle.stacked,
            size: 200.0,
          ),
          crossFadeState:
              _first ? CrossFadeState.showFirst : CrossFadeState.showSecond,
        ),
      ],
    );
  }
}
```
