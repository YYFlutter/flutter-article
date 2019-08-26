# Icon

## 介绍

Icon：图标，是一个专门用来显示图标的widget，在功能上，它与Android原生中的矢量图非常相似，
可以任意改变图标颜色和大小，并且在任何情况下都保持着清晰和低空间占用。

## 构造函数

Icon 继承自 StatefulWidget，只有一个构造方法：Icon()

从基础构造函数中：
```dart
  const Icon(this.icon, {
    Key key,
    this.size,
    this.color,
    this.semanticLabel,
    this.textDirection,
  }) : super(key: key);
```
我们可以看到其基本属性

### IconData icon
IconData是一个数据类，里面定义矢量图的点线，我们可以在里面绘制自己的点线图。
不过，flutter官方sdk给我们提供了一些基本的矢量图标，全部在Icons静态类里面，我们可以直接使用。

### double size
size是Icon的边长，或者说是直径，它没有宽高的概念

### Color color
color不用多说，自然是用来定义矢量图的颜色的

### TextDirection textDirection
TextDirection用于设置渲染图标的文字方向



