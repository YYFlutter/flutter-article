### ClipPath 介绍
ClipPath可以根据给定的Path来裁剪widget，它的定义跟ClipRect基本一样，不一样的地方是ClipRect传递的参数是个Rect类型，而ClipPath需要传一个Path类型，它的定义如下：
```dart
ClipPath({Key key, 
        CustomClipper<Path> clipper, 
        Clip clipBehavior: Clip.antiAlias, 
        Widget child })
```
这些参数的含义在讲ClipRect的时候都已经介绍过了，这里就不在赘述了，需要注意的是`clipper` 这里传入的需要是个Path类型。
根据Path去裁剪widget是相当的耗性能的，如果是一些已知的具体形状的裁剪，考虑使用下面裁剪工具来提高性能
- 矩形的裁剪，考虑使用`ClipRect`
- 椭圆或者圆形裁剪，考虑使用`ClipOval`
- 圆角矩形裁剪，考虑使用`ClipRRect`

### ClipPath 使用
上一节讲ClipRect的时候我们裁剪了一张图片，这里继续用上一节的例子，把图片裁剪成一个三角形的样子，代码如下：
```dart
class HomeState extends State<HomeWidget> {

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(title: Text('ClipDemo'),),
        body: Container(
            alignment: Alignment.center,
            child: clipPath()
        ));
  }

  Widget clipPath() {
    return  ClipPath(
          clipper: __MyPathClipper(),
          child: Align(
            alignment: Alignment.topCenter,
            heightFactor: 0.5,
            child: Image.network("http://img.redocn.com/sheying/20150213/mulanweichangcaoyuanfengjing_3951976.jpg",fit: BoxFit.fill),
          )
    );
  }
}

class __MyPathClipper extends CustomClipper<Path> {
  @override
  Path getClip(Size size) {
    var path = Path();
    path.moveTo(size.width / 2, 0);
    path.lineTo(0, size.height);
    path.lineTo(size.width, size.height);
    path.close();
    return path;
  }

  @override
  bool shouldReclip(CustomClipper<Path> oldClipper) {
    return false;
  }
}
```
效果如下：
![](https://upload-images.jianshu.io/upload_images/2829725-f95a7377d08706a9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

除了自己提供一个CustomClipper以外，ClipPath还提供了一个静态方法`shape`，这个静态方法接受一个参数类型为`ShapeBorder`的参数，用来标识想要裁剪的边框形状，`ShapeBorder`是个抽象接口类，目前flutter已经提供了需要实现接口类，如：`CircleBorder` `RoundedRectangleBorder` `BoxBorder` `UnderlineInputBorder`等等，通过这些现有的接口类，我们可以很方便的来做裁剪操作。

### ClipPath.shape 的使用
下面我们继续用上面那个例子来做演示，上面的例子中我们自己实现了一个`CustomClipper ` 返回了一个Path来裁剪出一个三角形，下面我们用`CircleBorder`来裁剪出一个圆形出来，代码如下：
```dart
class HomeState extends State<HomeWidget> {

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(title: Text('ClipDemo'),),
        body: Container(
            alignment: Alignment.center,
            child: clipPathShape()
        ));
  }

  Widget clipPathShape() {
    return ClipPath.shape(
        shape: CircleBorder(),
        child: Align(
          alignment: Alignment.topCenter,
          heightFactor: 0.5,
          child: Image.network(
              "http://img.redocn.com/sheying/20150213/mulanweichangcaoyuanfengjing_3951976.jpg",
              fit: BoxFit.fill),
        ));
  }
}
```
效果如下：
![](https://upload-images.jianshu.io/upload_images/2829725-307469353f2e25a6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
