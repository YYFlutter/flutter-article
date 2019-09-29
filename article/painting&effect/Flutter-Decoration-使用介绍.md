### Decoration Class介绍
Decoration是个窗口小部件(widget)，可以在子widget的绘制前后对其进行装饰，Decoration的定义如下：
```dart
DecoratedBox({Key key, @required Decoration decoration, DecorationPosition position: DecorationPosition.background, Widget child })
```
- `decoration` : 装饰器接口，Decoration是个抽象接口，BoxDecoration是它其一个具体实现类，Decoration装饰器的绘制最终会由BoxPainter来完成，实现一个Decoration装饰器可以通过createBoxPainter方法来获取一个BoxPainter，最终通过BoxPainter来进行绘制。
- `position `:  是个枚举类型，用来控制装饰器在哪里绘制，取值有`background`跟`foreground`，前者代表是在背景绘制，后者是在前景绘制

### BoxDecoration介绍
BoxDecoration是Decoration的一个实现类，BoxDecoration提供了背景颜色、边框、阴影、圆角、颜色渐变、形状等等装饰能力，BoxDecoration的定义如下
```dart
BoxDecoration({
  Color color,
  DecorationImage image,
  BoxBorder border,
  BorderRadiusGeometry borderRadius, 
  List<BoxShadow> boxShadow, 
  Gradient gradient,
  BlendMode backgroundBlendMode,
  BoxShape shape = BoxShape.rectangle, 
})
```
- `color` ： 背景颜色
- `image` ：背景图片，会绘制在背景颜色上面
- `border` ： 边框，会绘制在背景颜色背景图片上面
- `borderRadius` ： 边框圆角
- `boxShadow` ： 背景阴影
- `gradient` ： 填充渐变颜色
- `backgroundBlendMode` ： 背景混合模式
- `shape` ： 形状

### DecoratedBox使用
下面直接给出一个完整的例子
```dart
import 'package:flutter/material.dart';

/**
 * Created by nls on 2019/7/20.
 * Nothing.
 */
class DecoratedBoxDemo extends StatelessWidget {


  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      theme: ThemeData(primaryColor: Colors.blue),
      home: HomeWidget(),
    );
  }
}

class HomeWidget extends StatefulWidget {

  @override
  State createState() {
    return HomeState();
  }
}

class HomeState extends State<HomeWidget> {

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("TransformDemo"),),
      body: Container(
        color: Colors.amberAccent,
        alignment: Alignment.center,
        child:  DecoratedBox(
            decoration: BoxDecoration(
                gradient: LinearGradient(colors:[Colors.red,Colors.orange[700]]), //背景渐变
                borderRadius: BorderRadius.circular(3.0), //3像素圆角
                boxShadow: [ //阴影
                  BoxShadow(
                      color:Colors.black54,
                      offset: Offset(2.0,2.0),
                      blurRadius: 4.0
                  )
                ]
            ),
            child: Padding(padding: EdgeInsets.symmetric(horizontal: 80.0, vertical: 18.0),
              child: Text("Login", style: TextStyle(color: Colors.white),),
            )
        )
      ),
    );
  }
}
```
效果如下：
![](https://upload-images.jianshu.io/upload_images/2829725-62e009263d6030b8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
