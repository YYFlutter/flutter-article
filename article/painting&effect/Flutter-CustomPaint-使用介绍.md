### CustomPaint 介绍
CustomPaint class提供了让用户自定义widget的能力，它暴露了一个canvas，可以通过这个canvas来绘制widget，CustomPaint会先调用painter绘制背景，然后再绘制child，最后调用foregroundPainter来绘制前景，CustomPaint的定义如下
```dart
CustomPaint({Key key, 
      CustomPainter painter,
      CustomPainter foregroundPainter,
      Size size: Size.zero, 
      bool isComplex: false, 
      bool willChange: false, 
      Widget child })
```
- `painter`：负责绘制背景的painter
- `foregroundPainter` : 负责绘制前景的painter
- `size` : 控件大小
- `isComplex` ： 是否复杂绘制，需要用cache来提高绘制效率
-  `willChange` ： 和isComplex配合使用，当启用缓存时，该属性代表在下一帧中绘制是否会改变
- `child` ： 子widget

### CustomPainter 介绍
CustomPaint的绘制过程都将会交给CustomPainter来完成，CustomPainter是个抽象接口，在子类化CustomPainter的时候必须要重写它的`paint` 跟 `shouldRepaint`接口，可以根据自己的场景来选择性的重写`hitTest`跟`shouldRebuildSemantics`方法。
- `paint` : 每当CustomPaint需要重绘的时候都会调用此接口
- `shouldRepaint` ： 当CustomPaint被重新设置了一个新的painter后会回调此方法，CustomPaint会根据shouldRepaint的返回值来判断是否需要重新绘制ui，譬如新的painter跟旧的painter绘制的内容不一样时，此时shouldRepaint需要返回true来通知CustomPaint重新绘制。

### Canvas 介绍
canvas--画布，真正的绘制是由canvas跟paint来完成的，画布提供了各种绘制的接口来绘制图形，除此以外画布还提供了平移、缩放、旋转等矩阵变换接口，画布都有固定大小跟形状，还可以使用画布提供的裁剪接口来裁剪画布的大小形状等等。
常用的绘制接口有[更多请查看官方文档]([https://api.flutter.dev/flutter/dart-ui/Canvas-class.html](https://api.flutter.dev/flutter/dart-ui/Canvas-class.html)
)
```dart
//画圆
drawCircle(Offset c, double radius, Paint paint) → void
//画图片
drawImage(Image image, Offset p, Paint paint) → void
//画九宫图
drawImageNine(Image image, Rect center, Rect dst, Paint paint) → void
//画线
drawLine(Offset p1, Offset p2, Paint paint) → void
//画椭圆
drawOval(Rect rect, Paint paint) → void
//画文字
drawParagraph(Paragraph paragraph, Offset offset) → void
//画Rect区域
drawRect(Rect rect, Paint paint) → void
//画阴影
drawShadow(Path path, Color color, double elevation, bool transparentOccluder) → void
```

### Paint 介绍
Paint---笔画，是用来设置在画布上面绘制图形时的一些笔画属性，如：颜色、线宽、绘制模式、抗锯齿等等。常用属性有[更多请查看官方文档]([https://api.flutter.dev/flutter/dart-ui/Paint-class.html](https://api.flutter.dev/flutter/dart-ui/Paint-class.html)
)
`color` ： 设置画笔颜色
`isAntiAlias` ： 设置画笔是否扛锯齿
`shader` : 着色器，填充形状或者画线时用到，如果没设置将会使用color
`strokeWidth` ： 设置画笔画线宽度
`style ` ：绘制模式，画线或充满

### CustomPaint 使用
下面这个例子来自于官方，通过`CustomPaint` 画出了一个蓝天跟太阳出来
```dart
class HomeState extends State<HomeWidget> {

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('CustomPaintDemo'),),
      body: Container(
        alignment: Alignment.center,
        child: CustomPaint(
          painter: Sky(),
          child: Center(
            child: Text(
              'Once upon a time...',
              style: const TextStyle(
                fontSize: 40.0,
                fontWeight: FontWeight.w900,
                color: Color(0xFFFFFFFF),
              ),
            ),
          ),
        )
      ),
    );
  }
}

class Sky extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    var rect = Offset.zero & size;
    var gradient = RadialGradient(
      center: const Alignment(0.7, -0.6),
      radius: 0.2,
      colors: [const Color(0xFFFFFF00), const Color(0xFF0099FF)],
      stops: [0.4, 1.0],
    );
    canvas.drawRect(
      rect,
      Paint()..shader = gradient.createShader(rect),
    );
  }

  @override
  SemanticsBuilderCallback get semanticsBuilder {
    return (Size size) {
      // Annotate a rectangle containing the picture of the sun
      // with the label "Sun". When text to speech feature is enabled on the
      // device, a user will be able to locate the sun on this picture by
      // touch.
      var rect = Offset.zero & size;
      var width = size.shortestSide * 0.4;
      rect = const Alignment(0.8, -0.9).inscribe(Size(width, width), rect);
      return [
        CustomPainterSemantics(
          rect: rect,
          properties: SemanticsProperties(
            label: 'Sun',
            textDirection: TextDirection.ltr,
          ),
        ),
      ];
    };
  }

  // Since this Sky painter has no fields, it always paints
  // the same thing and semantics information is the same.
  // Therefore we return false here. If we had fields (set
  // from the constructor) then we would return true if any
  // of them differed from the same fields on the oldDelegate.
  @override
  bool shouldRepaint(Sky oldDelegate) => false;
  @override
  bool shouldRebuildSemantics(Sky oldDelegate) => false;
}
```
效果如下：
![](https://upload-images.jianshu.io/upload_images/2829725-ae1207e03b154204.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
