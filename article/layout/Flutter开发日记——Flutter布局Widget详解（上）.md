## Container

**1、简介**

* Container类似于h5的盒子模型，相当于布局容器
* Container在没有子节点的时候，会试图变得足够大
* Container在带有子节点的时候，会根据子节点的尺寸调节自身大小

**2、构造函数**

```dart
Container({
    Key key,
    this.alignment,
    this.padding,
    Color color,
    Decoration decoration,
    this.foregroundDecoration,
    double width,
    double height,
    BoxConstraints constraints,
    this.margin,
    this.transform,
    this.child,
})
```

* alignment：控制child的对齐方式
* padding：容器本身的内边距
* color：容器的背景色
* decoration：容器的样式，类似于css的style
* foregroundDecoration：容器的前景色，可能会遮盖color效果
* width：容器的宽度
* height：容器的高度
* constraints：容器的约束，约束宽高的大小
* margin：容器本身的外边距
* transform：容器的变换矩阵，可以让容器的缩放、旋转、平移等
* child：容器的子控件

**3、例子**

decoration可以实现阴影和边框的效果

```dart
Widget _buildColumn() {
    return Container(
      constraints: BoxConstraints.expand(
        height: 200,
      ),
      padding: EdgeInsets.all(8.0),
      child: Text("Hello World"),
      alignment: Alignment.center,
      transform: Matrix4.identity(),
      margin: EdgeInsets.all(16.0),
      decoration: BoxDecoration(
        border: Border.all(color: Colors.black, width: 2.0),
        color: Colors.blue[200],
        borderRadius: BorderRadius.circular(20.0)
      ),
      foregroundDecoration: BoxDecoration(),
      height: 200,
      width: 100,
      //color: Colors.blue[200],
    );
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191029155905285.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzc5Njg5,size_16,color_FFFFFF,t_70)

## Padding

**1、简介**

* Padding是比较功能单一的控件，负责子控件的内边距

**2、构造函数**

```dart
const Padding({
    Key key,
    @required this.padding,
    Widget child,
})
```

* padding：控件的内边距
* child：子控件

**3、例子**

```dart
Widget _buildColumn() {
    return Padding(
      padding: EdgeInsets.all(8.0),
      child: Container(
        height: 200,
        width: 200,
        color: Colors.blue[200],
      ),
    );
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191029155913387.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzc5Njg5,size_16,color_FFFFFF,t_70)

## Align

**1、简介**

* Align可以设置child的对齐方式，例如居中、居左、居右等，并根据child尺寸调节自身尺寸
* 当widthFactor和heightFactor为null的时候，child的尺寸会尽量的扩展自己的尺寸，直至填充父控件

**2、构造函数**

```dart
const Align({
    Key key,
    this.alignment: Alignment.center,
    this.widthFactor,
    this.heightFactor,
    Widget child
})
```

* alignment：child的对齐方式
* widthFactor：宽度因子，若设置2.0的时候，Align的宽度将会是child的两倍
* heightFactor：高度因子，若设置2.0的时候，Align的高度将会是child的两倍
* child：子控件

**3、例子**

由于设置了heightFactor和widthFactor，表示父控件的宽高最大应该是子控件的2.0倍。如果不设置heightFactor和widthFactor，则父控件则无限大，则子控件会在屏幕底部中点

```dart
Widget _buildColumn() {
    return Container(
      color: Colors.blue[200],
      child: Align(
        heightFactor: 2.0,
        widthFactor: 2.0,
        alignment: Alignment(0.0, 1.0), //底部中点对齐
        child: Text("Hello!"),
      ),
    );
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191029160109328.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzc5Njg5,size_16,color_FFFFFF,t_70)

## Center

**1、简介**

* Center控件是将child居中的控件，居中的位置是父控件的中点位置
* Center控件若设置了heightFactor和widthFactor，则父控件的尺寸会有所变化
* Center控件完全继承自Align控件，只不过内部默认将`alignment`属性设置为居中

**2、构造函数**

```dart
class Center extends Align {
  const Center({ Key key, double widthFactor, double heightFactor, Widget child })
    : super(key: key, widthFactor: widthFactor, heightFactor: heightFactor, child: child);
}
```

**3、例子**

由于设置了heightFactor和widthFactor，表示父控件的宽高最大应该是子控件的1.5倍，所以父控件大小是300x300，则子控件就会在父控件的基础上居中显示。如果不设置heightFactor和widthFactor，则父控件则无限大，填充屏幕，则Center组件就在父控件的居中显示，即屏幕中间

```dart
Widget _buildColumn() {
    return Container(
      color: Colors.blueGrey,
      child: Center(
        heightFactor: 1.5,
        widthFactor: 1.5,
        child: Container(
          height: 200,
          width: 200,
          color: Colors.blue[200],
        ),
      ),
    );
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191029160116747.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzc5Njg5,size_16,color_FFFFFF,t_70)

## FittedBox

**1、简介**

* FittedBox会在自己的尺寸范围内缩放并且调整child位置，使得child适合其尺寸
* FittedBox类似于ImageView的ScaleType的属性

**2、构造函数**

```dart
const FittedBox({
    Key key,
    this.fit: BoxFit.contain,
    this.alignment: Alignment.center,
    Widget child,
})
```

* fit：child控件的填充模式
* alignment：child的对齐方式
* child：子控件

填充模式

* BoxFit.none：默认不缩放，以子控件的宽和高作为基准，如果父控件不够承载，则按比例缩小子控件，图片不会变形
* BoxFit.fill：将子控件的宽和高，填充整个父控件，图片会变形
* BoxFit.contain：将子控件的宽和高，按比例填充父控件的宽和高，直到有一边先填充完成为止，图片不会变形
* BoxFit.cover：以子控件的宽和高作为基准，放入父控件中，如果父控件不够承载，则裁剪子控件多余的部分，图片不会变形，但会被裁剪
* BoxFit.fitWidth：以子控件的宽作为基准，放入父控件中，直到父控件的宽被挤满，图片不会变形，但会被裁剪
* BoxFit.fitHeight：以子控件的高作为基准，放入父控件中，直到父控件的高被挤满，图片不会变形，但会被裁剪
* BoxFit.scaleDown：以父控件的宽和高作为基准，子控件无条件缩放直到可以塞进父控件

**3、例子**

常用的就是对图片的裁剪，也可以是对widget的裁剪，只要widget有固定的大小

```dart
Widget _buildColumn() {
    return Container(
      width: 300,
      height: 300,
      color: Colors.blue,
      child: FittedBox(
        fit: BoxFit.cover,
        alignment: Alignment.centerLeft,
        child: Image.asset("images/day27/girl.jpg"),
      ),
    );
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191029160124115.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzc5Njg5,size_16,color_FFFFFF,t_70)

## AspectRatio

**1、简介**

* AspectRatio是调整child到设置的宽高比的组件
* AspectRatio会根据未明确的宽或高按比例进行缩放

**2、构造函数**

```dart
const AspectRatio({
    Key key,
    @required this.aspectRatio,
    Widget child
}) 
```

* aspectRatio：缩放比例，1.0为初始比例
* child：子控件

**3、例子**

由于高度200是确定的，宽度是不确定的，而子控件的缩放比是1.5，最后子控件的大小宽为300，高为200

```dart
Widget _buildColumn() {
    return Container(
      height: 200.0,
      color: Colors.blue,
      child: AspectRatio(
        aspectRatio: 1.5,
        child: Container(
          color: Colors.red,
        ),
      ),
    );
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191029160133595.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzc5Njg5,size_16,color_FFFFFF,t_70)

## ConstrainedBox

**1、简介**

* ConstrainedBox表示对子控件的约束条件，可以约束子控件的大小

**2、构造函数**

```dart
ConstrainedBox({
    Key key,
    @required this.constraints,
    Widget child
})
```

* constraints：子控件的约束条件
* child：子控件

**3、例子**

约束子控件最小必须是100x100，最大必须是150x150

```dart
Widget _buildColumn() {
    return ConstrainedBox(
      constraints: BoxConstraints(
        minWidth: 100.0,
        minHeight: 100.0,
        maxWidth: 150.0,
        maxHeight: 150.0,
      ),
      child: Container(
        width: 200.0,
        height: 200.0,
        color: Colors.red,
      ),
    );
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191029160142292.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzc5Njg5,size_16,color_FFFFFF,t_70)

## Baseline

**1、简介**

* Baseline控件同文字的baseline是同个意思的，处于文字的基准线
* 如果child有baseline（比如Text控件），则根据child的baseline属性，调整child的位置
* 如果child没有baseline（比如Container控件），则根据child的bottom，来调整child的位置

**2、构造函数**

```dart
const Baseline({
  Key key,
  @required this.baseline,
  @required this.baselineType,
  Widget child
})
```

* baseline：baseline数值，自上而下
* baselineType：baseline类型，alphabetic（对齐字符底部的水平线）和ideographic（对齐表意字符的水平线）
* child：子控件

**3、例子**

由于文字是具有baseline属性的，通过例子看出没有baseline属性的话，只能根据child的bottom对齐，文字则会在baseline上

```dart
Widget _buildColumn() {
    return Row(
      mainAxisAlignment: MainAxisAlignment.spaceBetween,
      children: <Widget>[
        Baseline(
          baselineType: TextBaseline.alphabetic,
          child: Text("Java",style: TextStyle(fontSize: 20.0),),
          baseline: 50.0,
        ),
        Baseline(
          //alphabetic：对齐字符底部的水平线
          //ideographic：对齐表意字符的水平线
          baselineType: TextBaseline.alphabetic,
          child: Container(
            width: 30,
            height: 30,
            color: Colors.blue[200],
          ),
          baseline: 50.0,
        ),
        Baseline(
          baselineType: TextBaseline.alphabetic,
          child: Text("iOS",style: TextStyle(fontSize: 30.0),),
          baseline: 50.0,
        ),
      ],
    );
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191029160150526.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzc5Njg5,size_16,color_FFFFFF,t_70)

## FractionallySizedBox

**1、简介**

* FractionallySizedBox控件会根据现有空间，来调整child的尺寸
* FractionallySizedBox控件中若child设置了具体的尺寸数值，也不起作用

**2、构造函数**

```dart
const FractionallySizedBox({
  Key key,
  this.alignment = Alignment.center,
  this.widthFactor,
  this.heightFactor,
  Widget child,
})
```

* alignment：child的对齐方式
* widthFactor：宽度因子，若设置0.5的时候，子控件的宽度将会是父控件的一半，若设置1.5的时候，子控件的宽度将会是父控件的1.5倍
* heightFactor：高度因子，若设置0.5的时候，子控件的高度将会是父控件的一半，若设置1.5的时候，子控件的高度将会是父控件的1.5倍
* child：子控件

**3、例子**

不需要指定子控件的大小，通过`FractionallySizedBox`约束子控件的大小为父控件的一半

```dart
Widget _buildColumn() {
    return Container(
      color: Colors.blue[600],
      width: 200,
      height: 200,
      child: FractionallySizedBox(
        alignment: Alignment.center,
        widthFactor: 0.5,
        heightFactor: 0.5,
        child: Container(
          color: Colors.blue[200],
        ),
      ),
    );
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191029160158782.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzc5Njg5,size_16,color_FFFFFF,t_70)

## IntrinsicHeight

**1、简介**

* IntrinsicHeight控件会调整child到固定的高度

**2、构造函数**

```dart
const IntrinsicHeight({ Key key, Widget child })
```

* child：子控件

**3、例子**

在`IntrinsicHeight`子控件中放置四个相同宽度的容器，设置其中两个容器的高度为150和60，另外两个不设置，`IntrinsicHeight`会找到最大的高度去限制其余容器

```dart
Widget _buildColumn() {
    return IntrinsicHeight(
      child: Row(
        mainAxisAlignment: MainAxisAlignment.spaceBetween,
        children: <Widget>[
          Container(
            color: Colors.blue,
            width: 40.0,
            height: 150.0,
          ),
          Container(
            color: Colors.red,
            width: 40.0,
            height: 60.0,
          ),
          Container(color: Colors.yellow, width: 40.0),
          Container(color: Colors.yellow, width: 40.0),
        ],
      ),
    );
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191029160206340.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzc5Njg5,size_16,color_FFFFFF,t_70)

## IntrinsicWidth

**1、简介**

* IntrinsicWidth控件会调整child到固定的宽度
* IntrinsicWidth控件和IntrinsicHeight控件最大的区别在于IntrinsicWidth的宽高会受到限制

**2、构造函数**

```dart
const IntrinsicWidth({ Key key, this.stepWidth, this.stepHeight, Widget child })
```

* stepWidth：如果为null，child的宽度是child集合当中的最大宽度，child的最小宽度为指定的stepWidth宽度，如果stepWidth宽度小于child的最小宽度，则该值不生效
* stepHeight：如果为null，child的高度是父控件的最大高度，不为null，child的最大高度为指定的stepHeight高度，如果stepHeight高度小于本身父容器的高度，则该值不生效
* child：子控件

**3、例子**

设置stepHeight为200，但是父控件的高度不止200，该值不生效。设置stepWidth为150，但是其他child的控件最大宽度不超过150，则最小的宽度为150，即图中的灰色背景

```dart
Widget _buildColumn() {
    return Container(
      color: Colors.grey,
      child: IntrinsicWidth(
        //父容器的大小
        stepHeight: 200,
        stepWidth: 150,
        child: Column(
          children: <Widget>[
            Container(
              color: Colors.blue,
              width: 100.0,
              height: 150.0,
            ),
            Container(
              color: Colors.red,
              width: 60.0,
              height: 150.0,
            ),
            Container(color: Colors.yellow, height: 150.0),
            Container(color: Colors.green, height: 150.0),
          ],
        ),
      ),
    );
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191029160211276.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzc5Njg5,size_16,color_FFFFFF,t_70)

## LimitedBox

**1、简介**

* LimitedBox控件是对子控件最大宽高进行限制的控件
* LimitedBox控件要使最大宽高限制起作用，是有一定条件的
* 如果LimitedBox外部宽度没有约束（比如Row，它是高度一定宽度不限制），child的宽受到LimitedBox最大宽度（maxWidth）属性限制
* 如果LimitedBox外部高度没有约束（比如Column，它是宽度一定高度不限制），child的高受到LimitedBox最大高度（maxHeight）属性限制

**2、构造函数**

```dart
const LimitedBox({
  Key key,
  this.maxWidth = double.infinity,
  this.maxHeight = double.infinity,
  Widget child,
})
```

* maxWidth：限制子控件的最大宽度
* maxHeight：限制子控件的最大高度
* child：子控件

**3、例子**

由于是Row组件，Row组件的高度是被确定的，宽度是不限制的，所以高度限制不起作用，宽度限制起作用，最后宽度是150，高度是250

```dart
Widget _buildColumn() {
    return Row(
      children: <Widget>[
        LimitedBox(
          maxHeight: 150, //由于是Row，高度被确定，所以高度限制不起作用
          maxWidth: 150, //由于是Row，宽度不限制，所以宽度限制起作用
          child: Container(
            width: 250,
            height: 250,
            color: Colors.redAccent,
          ),
        )
      ],
    );
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191029160219207.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzc5Njg5,size_16,color_FFFFFF,t_70)

## Offstage

**1、简介**

* Offstage控件是通过参数来控制child是否显示

**2、构造函数** 

```dart
const Offstage({ Key key, this.offstage = true, Widget child })
```

* offstage：当offstage为true，当前控件不会被绘制在屏幕上，不会响应点击事件，也不会占用空间，反之相反
* child：子控件

**3、例子**

```dart
Widget _buildColumn() {
    return Offstage(
      offstage: false,
      child: Container(
        width: 250,
        height: 250,
        color: Colors.redAccent,
      ),
    );
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191029160225857.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzc5Njg5,size_16,color_FFFFFF,t_70)

## OverflowBox

**1、简介**

* OverflowBox控件会限制一个范围区域，超出最大值部分会被裁剪，低于最小值会被填充

**2、构造函数**

```dart
const OverflowBox({
    Key key,
    this.alignment = Alignment.center,
    this.minWidth,
    this.maxWidth,
    this.minHeight,
    this.maxHeight,
    Widget child,
})
```

* alignment：子控件的对齐方式
* minWidth：限制子控件的最小宽度
* maxWidth：限制子控件的最大宽度
* minHeight：限制子控件的最小高度
* maxHeight：限制子控件的最大高度
* child：子控件

**3、例子**

子控件必须符合最小高度，所以最后出来的大小是300x600

```dart
Widget _buildColumn() {
    return OverflowBox(
      minHeight: 600,
      child: Container(
        width: 300,
        height: 300,
        color: Colors.blueAccent,
      ),
    );
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191029160233642.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzc5Njg5,size_16,color_FFFFFF,t_70)

## SizedBox

**1、简介**

* SizedBox是设置具体尺寸的控件

**2、构造函数**

```dart
const SizedBox({ Key key, this.width, this.height, Widget child })
```

* width：子控件的宽度，若设置了，会强制调整到此宽度，若未设置，则会根据子控件的自身的宽度进行调整
* height：子控件的高度，若设置了，会强制调整到此高度，若未设置，则会根据子控件的自身的高度进行调整
* child：子控件

**3、例子**

```dart
Widget _buildColumn() {
    return SizedBox(
      width: 200,
      height: 200,
      child: Container(
        color: Colors.blueAccent,
      ),
    );
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191029160240952.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzc5Njg5,size_16,color_FFFFFF,t_70)

## SizedOverflowBox

**1、简介**

* SizedOverflowBox是SizedBox与OverflowBox的结合体
* SizedOverflowBox具有SizedBox的固定尺寸，也有OverflowBox的裁剪功能

**2、构造函数**

```dart
const SizedOverflowBox({
  Key key,
  @required this.size,
  this.alignment = Alignment.center,
  Widget child,
})
```

* size：子控件的尺寸
* alignment：子控件的对齐方式
* child：子控件

**3、例子**

控制child的尺寸大小为100x100

```dart
Widget _buildColumn() {
    return SizedOverflowBox(
      size: Size(100, 100),
      alignment: Alignment.center,
      child: Container(
        width: 300,
        height: 300,
        color: Colors.blueAccent,
      ),
    );
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191029160247315.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzc5Njg5,size_16,color_FFFFFF,t_70)

## Transform

**1、简介**

* Transform控件是控制child控件的矩阵变换的控件，通过变换矩阵，对控件做动画

**2、构造函数**

```dart
const Transform({
  Key key,
  @required this.transform,
  this.origin,
  this.alignment,
  this.transformHitTests = true,
  Widget child,
})
```

* transform：矩阵变换的结果
* origin：子控件的偏移位置
* alignment：子控件的对齐方式
* transformHitTests：子控件的点击区域是否也做相应的改变
* child：子控件

**3、例子**

让容器轻微的偏移上方，然后做居于自身的旋转效果

```dart
Widget _buildColumn() {
    return Transform(
      origin: Offset(0.0, 10.0),
      transformHitTests: true,
      alignment: Alignment.center,
      transform: Matrix4.rotationZ(3.0),
      child: Container(
        width: 100,
        height: 100,
        color: Colors.blueAccent,
      ),
    );
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191029160253676.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzc5Njg5,size_16,color_FFFFFF,t_70)

## CustomSingleChildLayout

**1、简介**

* CustomSingleChildLayout控件是一个可以自定义拥有单个子控件的布局

**2、构造函数**

```dart
const CustomSingleChildLayout({
  Key key,
  @required this.delegate,
  Widget child
})
```

* delegate：控制子控件的代理类
* child：子控件

**3、例子**

需要先创建一个代理类，将传递进来的参数Size作为预期尺寸，如果预期尺寸和当前子控件的尺寸不符合，则会重新让子控件设置新的约束来适应预期Size的尺寸

```dart
class FixedSizeLayoutDelegate extends SingleChildLayoutDelegate {
  FixedSizeLayoutDelegate(this.size);
  // 预期尺寸
  final Size size;

  @override
  Size getSize(BoxConstraints constraints) => size;

  @override
  BoxConstraints getConstraintsForChild(BoxConstraints constraints) {
    // 重新设置子控件的约束，让他适应预期Size的尺寸
    return BoxConstraints.tight(size);
  }

  @override
  bool shouldRelayout(FixedSizeLayoutDelegate oldDelegate) {
    // 如果预期尺寸和当前子控件的尺寸不符合，则重新layout
    return size != oldDelegate.size;
  }
}
```

由于预期的尺寸是300x300，当前尺寸和预期不匹配，所以会将子控件调整到预期的尺寸

```
Widget _buildColumn() {
    return CustomSingleChildLayout(
      delegate: FixedSizeLayoutDelegate(Size(300, 300)),
      child: Container(
        width: 100,
        height: 100,
        color: Colors.blueAccent,
      ),
    );
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191029160259780.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzc5Njg5,size_16,color_FFFFFF,t_70)