### BackdropFilter 介绍
BackdropFilter可以用于对背景图片进行高斯模糊设置或者矩阵变换，除了图片以外BackdropFilter还能对任何子widget进行高斯模糊设置。BackdropFilter的定义如下：
```dart
BackdropFilter({Key key, 
         @required ImageFilter filter,
         Widget child })
```
核心参数是filter，它是个ImageFilter类型，ImageFilter有两种构造方法，分别是用来设置背景高斯模糊以及矩阵变换的：

- 设置高斯模糊
```dart
//构造一个设置高斯模糊的ImageFilter，sigmaX，sigmaY用来控制
//模糊度，取值范围是0-10
ImageFilter.blur({double sigmaX: 0.0, double sigmaY: 0.0 })
```

- 设置矩阵变换
```dart
ImageFilter.matrix(
        Float64List matrix4, 
        { FilterQuality filterQuality: FilterQuality.low })
```
**需要注意的是BackdropFilter不是变换背景来实现高斯模糊的效果，而是通过在背景上面盖上一个模糊层从而达到高斯模糊的效果，因此要做模糊的背景图必须要在BackdropFilter底下**

### BackdropFilter 使用
可以通过`Stack `来控制布局的层次摆放，下面给一个例子来演示下BackdropFilter的使用
```dart
class HomeState extends State<HomeWidget> {

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("BackdropFilterDemo")),
      body: Stack(
        children: <Widget>[
          Container(
            alignment: Alignment.center,
            child: Image.network("http://img.redocn.com/sheying/20150213/mulanweichangcaoyuanfengjing_3951976.jpg",
            width: 300, height: 300,),
          ),
          BackdropFilter(
            filter: ImageFilter.blur(sigmaX: 5, sigmaY: 5),
          child: Container(
            color: Colors.white.withAlpha(0),
          ),)
        ],
      )
    );
  }
}
```
效果如下
![](https://upload-images.jianshu.io/upload_images/2829725-d3da7666fbf7932b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

BackdropFilter可以对一切背景设置高斯模糊效果，不仅限于图片，譬如我们把Image替换成Text，代码如下
```dart
class HomeState extends State<HomeWidget> {

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("BackdropFilterDemo")),
      body: Stack(
        children: <Widget>[
          Container(
            alignment: Alignment.center,
            child: Text("BackdropFilterDemo" * 10),
          ),
          BackdropFilter(
            filter: ImageFilter.blur(sigmaX: 5, sigmaY: 5),
          child: Container(
            color: Colors.white.withAlpha(0),
          ),)
        ],
      )
    );
  }
}
```
效果如下
![](https://upload-images.jianshu.io/upload_images/2829725-41e95aecb7ecf685.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

