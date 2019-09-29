### ClipOval 介绍
ClipOval可以用来裁剪圆形或者椭圆，ClipOval的定义跟ClipRect一样，只不过是ClipRect裁剪出来的是矩形。ClipOval也接受一个Rect参数作为裁剪局域，它将会以给定的Rect的中心为圆心来裁剪圆，如果Rect长宽一样那么裁剪出来的就是个圆形，相反会裁剪出一个椭圆。ClipOval的定义如下：
```dart
ClipOval({Key key, 
        CustomClipper<Rect> clipper, 
        Clip clipBehavior: Clip.antiAlias, 
        Widget child })
```
这些参数跟ClipRect都一样，这里就不再赘述了。

### ClipOval 使用
下面我们继续用之前的例子来演示下ClipOval的用法
```dart
class HomeState extends State<HomeWidget> {

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('ClipDemo'),),
      body: Container(
          alignment: Alignment.center,
          child: ClipOval(
          clipper: _MyClipper(),
          child: new Image.network("http://img.redocn.com/sheying/20150213/mulanweichangcaoyuanfengjing_3951976.jpg",fit: BoxFit.fill)),
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
效果如下：
![](https://upload-images.jianshu.io/upload_images/2829725-9fef3010891e8967.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

因为我们的矩形并不是一个正方形，所以裁剪出来的是个椭圆，现在我们修改Rect为一个正方形，代码如下
```dart
class _MyClipper extends CustomClipper<Rect>{
  @override
  Rect getClip(Size size) {
   return new Rect.fromLTRB(0, 0, 200, 200);
  }

  @override
  bool shouldReclip(CustomClipper<Rect> oldClipper) {
    return false;
  }
}
```
现在Rect返回的是一个200x200的矩形，我们再看下效果
![](https://upload-images.jianshu.io/upload_images/2829725-0c2dfcbd88e8d9d9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这次裁剪出来的就是个圆形了
