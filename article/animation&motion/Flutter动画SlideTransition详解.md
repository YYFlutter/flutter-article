本篇文章已授权微信公众号 `YYGeeker` 独家发布转载请标明出处

## 控件介绍

1. `SlideTransition`表示一个平移动画，可以通过控制器去控制动画尺寸值的改变，从而控制动画的平移位置

## 构造函数

```java
SlideTransition({
    Key key,
    this.position,            //动画缩放值的变化
    this.transformHitTests,   //点击事件是否落在动画后的控件上
    this.textDirection,       //动画执行的位置关系
    Widget child,             //动画子元素
})
```

## 使用方法

1、封装动画

我们可以将常用属性包装成一个控件

* child：表示由外传递进来的元素，由`SlideTransition`包裹
* position：表示由外传递进来的动画属性值的变化，通过获取其值，填充到`child`的位置值上
* textDirection：表示动画执行的位置关系，分别是`TextDirection.rtl`左到右和`TextDirection.ltr`右到左
* transformHitTests：表示点击事件是否落在动画后的控件上

```java

class AnimatorTransition extends StatelessWidget {
  final Widget child;
  final Animation<Offset> animation;

  AnimatorTransition({this.child, this.animation});

  @override
  Widget build(BuildContext context) {
    return Center(
      child: SlideTransition(
        //点击事件是否落在动画后的控件上
        transformHitTests: true,
        //动画执行的位置关系
        textDirection: TextDirection.rtl,
        position: animation,
        child: this.child,
      ),
    );
  }
}
```

2、控制动画

* 动画属性值的变化需要`AnimationController`来控制
* 通过`CurvedAnimation`设置其插值器
* 通过`Tween`设置其值的变化范围

```java
class WeWidgetState extends State<WeWidget>
    with SingleTickerProviderStateMixin {
    
  Animation<num> _animation;
  AnimationController _controller;
  Animation _curve;

  @override
  void initState() {
    super.initState();

    //动画控制器
    _controller = AnimationController(
      duration: const Duration(milliseconds: 3000),
      vsync: this,
    );
    //动画插值器
    _curve = CurvedAnimation(parent: _controller, curve: Curves.fastOutSlowIn);
    //动画变化范围
    _animation = Tween(
      begin: Offset(0.0, 0.0),
      end: Offset(0.6, 0.3),
    ).animate(_curve);
    //启动动画
    _controller.forward();
  }
}
```

3、监听动画

* 通过`addStatusListener`监听动画状态的变化和通过`addListener`监听动画值的变化

```java
class WeWidgetState extends State<WeWidget>
    with SingleTickerProviderStateMixin {
  //尝试扩展或实现num时，除int或double之外的任何类型都是编译时错误
  Animation<num> _animation;
  AnimationController _controller;
  Animation _curve;

  double _animationValue;
  AnimationStatus _state;

  @override
  void initState() {
    super.initState();

    //动画控制器
    _controller = AnimationController(
      duration: const Duration(milliseconds: 3000),
      vsync: this,
    );
    //动画插值器
    _curve = CurvedAnimation(parent: _controller, curve: Curves.fastOutSlowIn);
    //动画变化范围
    _animation = Tween(
      begin: Offset(0.0, 0.0),
      end: Offset(0.6, 0.3),
    ).animate(_curve)
      ..addListener(() {
        setState(() {
          //记录变化的值
          _animationValue = _animation.value;
        });
      })
      ..addStatusListener((AnimationStatus state) {
        //如果动画已完成，就反转动画
        if (state == AnimationStatus.completed) {
          _controller.reverse();
        } else if (state == AnimationStatus.dismissed) {
        //如果动画已经消失，则开始动画
          _controller.forward();
        }

        setState(() {
          _state = state;
        });
      });
    //启动动画
    _controller.forward();
  }
}
```

## 效果图

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190805102413973.gif)

## 源代码

```java
import 'package:flutter/material.dart';

class Day17 extends StatelessWidget {
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

class WeWidgetState extends State<WeWidget>
    with SingleTickerProviderStateMixin {
  //尝试扩展或实现num时，除int或double之外的任何类型都是编译时错误
  Animation<Offset> _animation;
  AnimationController _controller;
  Animation _curve;

  Offset _animationValue;
  AnimationStatus _state;

  @override
  void initState() {
    super.initState();

    _controller = AnimationController(
      duration: const Duration(milliseconds: 3000),
      vsync: this,
    );
    _curve = CurvedAnimation(parent: _controller, curve: Curves.fastOutSlowIn);
    _animation = Tween(
      begin: Offset(0.0, 0.0),
      end: Offset(0.6, 0.3),
    ).animate(_curve)
      ..addListener(() {
        setState(() {
          _animationValue = _animation.value;
        });
      })
      ..addStatusListener((AnimationStatus state) {
        if (state == AnimationStatus.completed) {
          _controller.reverse();
        } else if (state == AnimationStatus.dismissed) {
          _controller.forward();
        }

        setState(() {
          _state = state;
        });
      });
    _controller.forward();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("day17"),
      ),
      body: _buildColumn(),
    );
  }

  Widget _buildColumn() {
    return Column(
      children: <Widget>[
        AnimatorTransition(
          child: FlutterLogo(
            style: FlutterLogoStyle.horizontal,
            size: 200,
          ),
          animation: _animation,
        ),
        Text("动画值：" + _animationValue.toString()),
        Text("动画状态：" + _state.toString()),
      ],
    );
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }
}

class AnimatorTransition extends StatelessWidget {
  final Widget child;
  final Animation<Offset> animation;

  AnimatorTransition({this.child, this.animation});

  @override
  Widget build(BuildContext context) {
    return Center(
      child: SlideTransition(
        //点击事件是否落在动画后的控件上
        transformHitTests: true,
        //动画执行的位置关系
        textDirection: TextDirection.rtl,
        position: animation,
        child: this.child,
      ),
    );
  }
}
```
