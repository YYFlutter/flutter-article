### Opacity class介绍
Opacity class是个widget控件，它可以改变子widget的透明度。这个类会先把子widget绘制到一个中间缓冲区里，然后做透明处理最后绘制到屏幕中。
当opacity的值为0时完全透明，不会进行绘制，控件不显示，当opacity的值为1时不透明，控件会被立马绘制，不会被先绘制到临时缓冲区里。当opacity值是0-1中间的值时，开销是比较昂贵的，因为控件需要先在中间缓冲区里绘制一遍。

### Opacity class的使用
下面这个例子，当_visible的值为true时将会显示Text控件，false的时候会隐藏Text控件
```dart
Opacity(
  opacity: _visible ? 1.0 : 0.0,
  child: const Text('Now you see me, now you don\'t!'),
)
```
通过这种方式去隐藏显示widget控件比把widget控件从控件树里面移除要高效多了。

### Opacity的动画性能问题
直接在Opacity控件上添加动画效果这样做效率是很低的，因为动画的每一帧效果都会导致Opacity的子控件树重建，这时候可以考虑使用`AnimatedOpacity`来代替。

### 设置图片透明的一些问题
如果是单张图片或者是纯色的背景，需要设置透明度时，考虑直接使用他们的透明通道比使用Opacity控件要高效得多，譬如`Container(color: Color.fromRGBO(255, 0, 0, 0.5))` 这行代码的效率要比`Opacity(opacity: 0.5, child: Container(color: Colors.red))`高效。
下面这个例子是不使用Opacity的情况下，显示一张图片，并且设置透明度为0.5
```dart
Image.network(
  'https://raw.githubusercontent.com/flutter/assets-for-api-docs/master/packages/diagrams/assets/blend_mode_destination.jpeg',
  color: Color.fromRGBO(255, 255, 255, 0.5),
  colorBlendMode: BlendMode.modulate
)
```
在绘制图片或者颜色的时候直接使用透明通道比起使用Opacity控件要高效多，因为Opacity控件将会在所有的widget控件上应用透明通道，这样会花费一定的屏外缓冲区，在屏外缓冲区内绘制内容又有可能会导致渲染目标的一些开关打开，特别的其中一些开关的打开又会导致GPU的绘制速度变慢。
