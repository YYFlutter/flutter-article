本篇文章已授权微信公众号 `YYGeeker` 独家发布转载请标明出处

## 控件介绍

1. `DecoratedBoxTransition`表示一个边框动画，可以通过控制器去控制动画边框值的改变，从而控制动画边框

## 构造函数

```java
DecoratedBoxTransition({
    Key key,
    this.decoration,           //动画属性值的变化
    this.position,             //动画的位置
    this.child,                //动画子元素
})
```

## 使用方法

1、封装动画

我们可以将常用属性包装成一个控件

* child：表示由外传递进来的元素，由`DecoratedBoxTransition`包裹
* decoration：表示由外传递进来的动画属性值的变化，通过获取其值，填充到`child`的边框上
* position：表示边框动画的位置，可以是前景位置或者是背景位置，前景位置会盖住`child`元素

```java
class AnimatorTransition extends StatelessWidget {
  final Widget child;
  final Animation<Decoration> animation;

  AnimatorTransition({this.child, this.animation});

  @override
  Widget build(BuildContext context) {
    return Center(
      child: DecoratedBoxTransition(
        position: DecorationPosition.background,
        decoration: animation,
        child: Container(
          child: this.child,
        ),
      ),
    );
  }
}
```

2、控制动画

* 动画属性值的变化需要`AnimationController`来控制
* 通过`CurvedAnimation`设置其插值器
* 通过`DecorationTween`设置其值的变化范围

```java
class WeWidgetState extends State<WeWidget>
    with SingleTickerProviderStateMixin {
    
  Animation<Decoration> _animation;
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
    _animation = DecorationTween(
      begin: BoxDecoration(
        borderRadius: BorderRadius.all(Radius.circular(0.0)),
        color: Colors.red,
      ),
      end: BoxDecoration(
        borderRadius: BorderRadius.all(Radius.circular(100.0)),
        color: Colors.green,
      ),
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
  Animation<Decoration> _animation;
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
    _animation = DecorationTween(
      begin: BoxDecoration(
        borderRadius: BorderRadius.all(Radius.circular(0.0)),
        color: Colors.red,
      ),
      end: BoxDecoration(
        borderRadius: BorderRadius.all(Radius.circular(100.0)),
        color: Colors.green,
      ),
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

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190731211456574.gif)

## 源代码

```java
import 'package:flutter/material.dart';

class Day11 extends StatelessWidget {
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
  Animation<Decoration> _animation;
  AnimationController _controller;
  Animation _curve;

  Decoration _animationValue;
  AnimationStatus _state;

  @override
  void initState() {
    super.initState();

    _controller = AnimationController(
      duration: const Duration(milliseconds: 3000),
      vsync: this,
    );
    _curve = CurvedAnimation(parent: _controller, curve: Curves.fastOutSlowIn);
    _animation = DecorationTween(
      begin: BoxDecoration(
        borderRadius: BorderRadius.all(Radius.circular(0.0)),
        color: Colors.red,
      ),
      end: BoxDecoration(
        borderRadius: BorderRadius.all(Radius.circular(100.0)),
        color: Colors.green,
      ),
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
        title: Text("day11"),
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
        Text("动画值：" + _animationValue.toStringShort()),
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
  final Animation<Decoration> animation;

  AnimatorTransition({this.child, this.animation});

  @override
  Widget build(BuildContext context) {
    return Center(
      child: DecoratedBoxTransition(
        position: DecorationPosition.background,
        decoration: animation,
        child: Container(
          child: this.child,
        ),
      ),
    );
  }
}
```
