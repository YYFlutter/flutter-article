### Transform介绍
窗口小部件(Widget)可以在Paint之前应用Transform进行转换，通过Transform可以对widget进行平移、旋转、缩放等矩阵变换。不像RotatedBox在layout前就对Widget进行旋转操作，Transform是在Widget绘制前进行转换，这意味着在计算Widget的显示需要占用多少空间时，不会去考虑Transform变换。

### Transform使用

-  **平移**
方法
```dart
// 创建一个widget，并且对他进行平移变换
//offset 偏移量，水平向右为正向，竖直向下为正向
// 子widget
Transform.translate({Key key, @required Offset offset, bool transformHitTests: true, Widget child })
```
例子
在垂直方向移动15个单位距离
```dart
Transform.translate(
  offset: const Offset(0.0, 15.0),
  child: Container(
    padding: const EdgeInsets.all(8.0),
    color: const Color(0xFF7F7F7F),
    child: const Text('Quarter'),
  ),
)
```
-  **旋转**
方法
```dart
//创建一个widget，并且对他进行旋转变换
//angle 旋转角度
//origin 偏移量
//alignment 对齐方式
//子widget 
Transform.rotate({ Key key, @required double angle, Offset origin, AlignmentGeometry alignment: Alignment.center, bool transformHitTests: true, Widget child })
```
例子
顺时针旋转45°
```dart
Transform.rotate(
  angle: math.pi / 4, // 旋转45°
  child: Container(
    padding: const EdgeInsets.all(8.0),
    color: const Color(0xFFE8581C),
    child: const Text('Apartment for rent!'),
  ),
)
```
> 使用math.pi时需要引入math包 import 'dart:math' as math;
-  **缩放**
方法
```dart
//scale 缩放多少倍
//origin 偏移量
//alignment 对齐方式
//子widget 
Transform.scale({ Key key, @required double scale, Offset origin, AlignmentGeometry alignment: Alignment.center, bool transformHitTests: true, Widget child })
```
例子
放大1.5倍
```dart
Transform.scale(
  scale: 1.5,
  child: Container(
    padding: const EdgeInsets.all(8.0),
    color: const Color(0xFFE8581C),
    child: const Text('Bad Ideas'),
  ),
)
```
