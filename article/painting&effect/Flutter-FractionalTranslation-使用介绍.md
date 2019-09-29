###FractionalTranslation介绍
前面我们已经讲过了Transform的使用，其中Transform.translate是一种平移的矩阵变换，平移的单位是实际的屏幕单位，今天要讲的FractionalTranslation class本质上也是Transform的一种，它也是用来做平移变换的，不同的地方是，它平移的单位是控件宽高的倍数单位。它的定义如下
```dart
FractionalTranslation({
Key key, 
@required Offset translation, 
bool transformHitTests: true, 
Widget child })
```
可以看得出来它的定义是跟`Transform.translate`一样的，不一样的地方是`translation` 参数的理解，下面我们通过几个例子来讲解下FractionalTranslation的使用

###FractionalTranslation 使用
把Text控件向右平移 平移的距离是Text控件宽度的0.5倍
```dart
Container(
        color: Colors.amberAccent,
        alignment: Alignment.center,
        child: FractionalTranslation(
        translation: Offset(0.5, 0),
        child: Text("Hello world")),
      ),
```

把Text控件向右平移 平移的距离是Text控件宽度的2倍
```dart
Container(
        color: Colors.amberAccent,
        alignment: Alignment.center,
        child: FractionalTranslation(
        translation: Offset(2, 0),
        child: Text("Hello world")),
      ),
```
把Text控件向右向下平移 右边平移距离是Text宽度的1倍，向下平移的距离是Text高度的1.5倍
```dart
Container(
        color: Colors.amberAccent,
        alignment: Alignment.center,
        child: FractionalTranslation(
        translation: Offset(1, 1.5),
        child: Text("Hello world")),
      ),
```
### 完整例子
```dart
import 'package:flutter/material.dart';
import 'dart:math' as math;

/**
 * Created by nls on 2019/7/20.
 * Nothing.
 */
class TransformDemo extends StatelessWidget {


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
        child: FractionalTranslation(
            translation: Offset(1, 0),
        child: Text("Hello world")),
      ),
    );
  }
}
```
效果如下：
![](https://upload-images.jianshu.io/upload_images/2829725-f10c0ecbb8cfe625.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


