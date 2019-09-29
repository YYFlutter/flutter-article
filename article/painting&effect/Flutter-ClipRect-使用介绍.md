### ClipRect 介绍
ClipRect控件默认是通过限制子widget的绘制区域来达到裁剪的效果的，通过custom clipper，可以自定义裁剪的大小跟坐标
ClipRect的定义如下
```dart
ClipRect({Key key, 
        CustomClipper<Rect> clipper, 
        Clip clipBehavior: Clip.hardEdge, 
        Widget child })
```
- `clipper` ： 自定义裁剪的大小跟局域
- `clipBehavior ` ： 裁剪方式，取值有：
`Clip.hardEdge`（快速裁剪，牺牲质量，不支持抗锯齿）
`antiAlias`（较慢的裁剪，支持抗锯齿，裁剪出来的边框相对圆滑），`antiAliasWithSaveLayer` （裁剪效率最低最慢，通常比较少用到）

### CustomClipper 介绍
ClipRect class默认是没有任何裁剪效果的，需要通过clipper参数告诉ClipRect如何去裁剪，clipper是个CustomClipper类型，CustomClipper是个抽象接口类，我们通过继承CustomClipper，重写`getClip` 方法可以定义一个裁剪区域，通过重写`shouldReclip`方法来告诉ClipRect当一个新的clipper被设置了是否需要更新裁剪区域，譬如开始设置的clipper裁剪坐标是从(10,10)开始的，新设置的clipper裁剪坐标是(20,20)，那么shouldReclip需要返回true来通知ClipRect更新裁剪区域。

### ClipRect 使用
下面这个例子从网络上加载一张图片，并且进行裁剪，裁剪坐标是(10,10) 裁剪的宽高是图片的宽高减去10
```dart
import 'package:flutter/material.dart';

/**
 * Created by nls on 2019/7/27.
 * Nothing.
 */
class ClipDemo extends StatelessWidget {

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
  State createState() => HomeState();
}

class HomeState extends State<HomeWidget> {

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(title: Text('ClipDemo'),),
        body: Container(
            alignment: Alignment.center,
            child: clipRect()
        ));
  }

  Widget clipRect() {
    return ClipRect(
      clipper: _MyClipper(),
      child: Align(
        alignment: Alignment.topCenter,
        child: Image.network("http://img.redocn.com/sheying/20150213/mulanweichangcaoyuanfengjing_3951976.jpg",fit: BoxFit.fill),
      ),
    );
  }
}

class _MyClipper extends CustomClipper<Rect>{
  @override
  Rect getClip(Size size) {
    return new Rect.fromLTRB(10.0, 10.0, size.width - 10.0,  size.height- 10.0);
  }

  @override
  bool shouldReclip(CustomClipper<Rect> oldClipper) {
    return false;
  }
}
```
效果如下
![9357349.png](https://upload-images.jianshu.io/upload_images/2829725-96dc6e29ff460d40.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

