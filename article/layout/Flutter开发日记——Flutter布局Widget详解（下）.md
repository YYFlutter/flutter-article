## Row

**1、简介**

* Row组件是一个横向排布的布局组件，跟h5的Flex布局一样，只不过限定了横向排布

**2、构造函数**

```dart
Row({
  Key key,
  MainAxisAlignment mainAxisAlignment = MainAxisAlignment.start,
  MainAxisSize mainAxisSize = MainAxisSize.max,
  CrossAxisAlignment crossAxisAlignment = CrossAxisAlignment.center,
  TextDirection textDirection,
  VerticalDirection verticalDirection = VerticalDirection.down,
  TextBaseline textBaseline,
  List<Widget> children = const <Widget>[],
})
```

* mainAxisAlignment：主轴方向的排布方式，由于是横向布局，其主轴是横向的水平线
    * center：主轴中心
    * start：主轴起点
    * end：主轴末尾
    * spaceAround：主轴中间空白区域均分，首尾空白区域为1/2
    * spaceBetween：主轴中间空白区域均分，首尾没有空白区域
    * spaceEvenly：主轴中间空白区域均分，首尾平分空白区域
* mainAxisSize：主轴方向占有空间的值
    * max：占用最大空间
    * min：占用最小空间  
* crossAxisAlignment：侧轴方向的排布方式，由于是横向布局，其侧轴是垂直的竖线
    * baseline：侧轴与baseline对齐
    * center：侧轴居中显示
    * end：侧轴末尾显示
    * start：侧轴起点显示
    * stretch：侧轴填满显示
* textDirection：文字的排布方式
    * TextDirection.ltr：从左到右
    * TextDirection.rtl：从右到左
* verticalDirection：子控件的排布方式
    * down：从左上角到右下角进行布局
    * up：从右下角到左上角进行布局 
* textBaseline：文字的基准线
* children：子控件集合

**3、例子**

三个容器横向排放

```dart
Widget _buildColumn() {
    return Row(
      mainAxisAlignment: MainAxisAlignment.center,
      crossAxisAlignment: CrossAxisAlignment.center,
      textDirection: TextDirection.ltr,
      textBaseline: TextBaseline.alphabetic,
      mainAxisSize: MainAxisSize.max,
      verticalDirection: VerticalDirection.down,
      children: <Widget>[
        Container(
          height: 50,
          width: 50,
          color: Colors.blueAccent,
        ),
        Container(
          height: 50,
          width: 50,
          color: Colors.redAccent,
        ),
        Container(
          height: 50,
          width: 50,
          color: Colors.greenAccent,
        )
      ],
    );
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191104232354192.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzc5Njg5,size_16,color_FFFFFF,t_70)

## Column

**1、简介**

* Column组件是一个竖向排布的布局组件，跟h5的Flex布局一样，只不过限定了竖向排布

**2、构造函数**

```dart
Column({
    Key key,
    MainAxisAlignment mainAxisAlignment = MainAxisAlignment.start,
    MainAxisSize mainAxisSize = MainAxisSize.max,
    CrossAxisAlignment crossAxisAlignment = CrossAxisAlignment.center,
    TextDirection textDirection,
    VerticalDirection verticalDirection = VerticalDirection.down,
    TextBaseline textBaseline,
    List<Widget> children = const <Widget>[],
})
```

* mainAxisAlignment：主轴方向的排布方式，由于是竖向布局，其主轴是竖向的垂直线
    * center：主轴中心
    * start：主轴起点
    * end：主轴末尾
    * spaceAround：主轴中间空白区域均分，首尾空白区域为1/2
    * spaceBetween：主轴中间空白区域均分，首尾没有空白区域
    * spaceEvenly：主轴中间空白区域均分，首尾平分空白区域
* mainAxisSize：主轴方向占有空间的值
    * max：占用最大空间
    * min：占用最小空间  
* crossAxisAlignment：侧轴方向的排布方式，由于是竖向布局，其侧轴是横向的水平线
    * baseline：侧轴与baseline对齐
    * center：侧轴居中显示
    * end：侧轴末尾显示
    * start：侧轴起点显示
    * stretch：侧轴填满显示
* textDirection：文字的排布方式
    * TextDirection.ltr：从左到右
    * TextDirection.rtl：从右到左
* verticalDirection：子控件的排布方式
    * down：从左上角到右下角进行布局
    * up：从右下角到左上角进行布局 
* textBaseline：文字的基准线
* children：子控件集合

**3、例子**

三个容器竖向排放，由于设置了up的摆放方式，导致位置是倒过来的

```dart
Widget _buildColumn() {
    return Column(
      mainAxisAlignment: MainAxisAlignment.center,
      crossAxisAlignment: CrossAxisAlignment.center,
      verticalDirection: VerticalDirection.up,
      textBaseline: TextBaseline.alphabetic,
      textDirection: TextDirection.ltr,
      children: <Widget>[Container(
        height: 50,
        width: 50,
        color: Colors.blueAccent,
      ),
      Container(
        height: 50,
        width: 50,
        color: Colors.redAccent,
      ),
      Container(
        height: 50,
        width: 50,
        color: Colors.greenAccent,
      )],
    );
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191104232406525.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzc5Njg5,size_16,color_FFFFFF,t_70)

## Stack

**1、简介**

* Stack组件是可以互相叠在一起的布局，类似于一个栈
* Stack组件通过alignment去决定子控件的位置

**2、构造函数**

```dart
Stack({
  Key key,
  this.alignment = AlignmentDirectional.topStart,
  this.textDirection,
  this.fit = StackFit.loose,
  this.overflow = Overflow.clip,
  List<Widget> children = const <Widget>[],
})
```

* alignment：控制child的对齐方式
* textDirection：文字的排布方式
    * TextDirection.ltr：从左到右
    * TextDirection.rtl：从右到左
* fit：定义子控件集合的尺寸
    * StackFit.loose：子控件的尺寸不受限制
    * StackFit.expand：子控件的尺寸尽可能大
    * StackFit.passthrough：不改变子控件的约束条件
* overflow：超出布局本身的处理
    * Overflow.clip：超出的布局被裁剪
    * Overflow.visible：超出的布局被显示
* children：子控件集合

**3、例子**

将两个容器叠加在一起，并且在对齐右下角

```dart
Widget _buildColumn() {
    return Stack(
      textDirection: TextDirection.ltr,
      alignment: Alignment.bottomRight,
      overflow: Overflow.visible,
      fit: StackFit.loose,
      children: <Widget>[
        Container(
          width: 100,
          height: 100,
          color: Colors.greenAccent,
        ),
        Container(
          height: 50,
          width: 50,
          color: Colors.redAccent,
        )
      ],
    );
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191104232412241.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzc5Njg5,size_16,color_FFFFFF,t_70)

## IndexedStack

**1、简介**

* IndexedStack控件本质继承了Stack组件，区别在于通过index增加了层级控制，控制层级的显示

**2、构造函数**

```dart
IndexedStack({
    Key key,
    AlignmentGeometry alignment = AlignmentDirectional.topStart,
    TextDirection textDirection,
    StackFit sizing = StackFit.loose,
    this.index = 0,
    List<Widget> children = const <Widget>[],
}) 
```

* alignment：控制child的对齐方式
* textDirection：文字的排布方式
    * TextDirection.ltr：从左到右
    * TextDirection.rtl：从右到左
* sizing：定义子控件集合的尺寸
    * StackFit.loose：子控件的尺寸不受限制
    * StackFit.expand：子控件的尺寸尽可能大
    * StackFit.passthrough：不改变子控件的约束条件
* index：控制第几个child的显示，0表示第一个
* children：子控件集合

**3、例子**

通过index控制第二个容器的出现，第一个容器则隐藏

```dart
Widget _buildColumn() {
    return IndexedStack(
      index: 1,
      sizing: StackFit.loose,
      textDirection: TextDirection.ltr,
      alignment: Alignment.bottomRight,
      children: <Widget>[
        Container(
          width: 100,
          height: 100,
          color: Colors.greenAccent,
        ),
        Container(
          height: 50,
          width: 50,
          color: Colors.redAccent,
        )
      ],
    );
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191104232422203.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzc5Njg5,size_16,color_FFFFFF,t_70)

## Flow

**1、简介**

* Flow控件相当于流式布局，其布局的摆布方式任由开发者去控制

**2、构造函数**

```dart
Flow({
    Key key,
    @required this.delegate,
    List<Widget> children = const <Widget>[],
})
```

* delegate：布局管理器，可以管理布局的摆放
* children：子控件集合

**3、例子**

在Flow布局中摆放一堆容器，并且大小不一

```dart
Widget _buildColumn() {
    return Flow(
      delegate: GridFlowDelegate(margin: EdgeInsets.all(10.0)),
      children: <Widget>[
        Container(
          width: 100,
          height: 100,
          color: Colors.greenAccent,
        ),
        Container(
          height: 50,
          width: 50,
          color: Colors.redAccent,
        ),
        Container(
          width: 100,
          height: 100,
          color: Colors.greenAccent,
        ),
        Container(
          height: 50,
          width: 50,
          color: Colors.redAccent,
        ),
        Container(
          width: 100,
          height: 100,
          color: Colors.greenAccent,
        ),
        Container(
          height: 50,
          width: 50,
          color: Colors.redAccent,
        ),
        Container(
          width: 100,
          height: 100,
          color: Colors.greenAccent,
        ),
        Container(
          height: 50,
          width: 50,
          color: Colors.redAccent,
        ),
        Container(
          width: 100,
          height: 100,
          color: Colors.greenAccent,
        )
      ],
    );
}
```

在布局管理器中，自定义我们的摆布方式，以一行中最高的容器作为换行的高度进行横向摆布

```dart
class GridFlowDelegate extends FlowDelegate {
  EdgeInsets margin = EdgeInsets.zero;

  GridFlowDelegate({this.margin});

  @override
  void paintChildren(FlowPaintingContext context) {
    var x = margin.left; //绘制子控件的x坐标
    var y = margin.top; //绘制子控件的y坐标
    var maxHeightIndex  = 0; //同一行中最大高度的子控件的索引，用于换行
    for (int i = 0; i < context.childCount; i++) {
      // 当前控件需要的最大宽度 = 控件本身的宽度 + 左右边距
      var w = context.getChildSize(i).width + x + margin.right;
      if (w < context.size.width) {
        // 如果未超出当前未分配的宽度，则直接平移到对应位置画出来
        context.paintChild(i, transform: Matrix4.translationValues(x, y, 0.0));
        // 下一次的x坐标
        x = w + margin.left;
        // 在第二个控件开始取同一行的最大高度的控件
        if (i >= 1){
          var currentHeight = context.getChildSize(i).height + margin.top + margin.bottom;
          var lastHeight = context.getChildSize(maxHeightIndex).height + margin.top + margin.bottom;
          if (currentHeight > lastHeight) {
            // 保留最大高度的索引值
            maxHeightIndex = i;
          }
        }
      }else{
        // 如果超出当前未分配的宽度，则先归位x坐标恢复默认值，从左边开始重新分配空间
        x = margin.left;
        // y坐标
        y += context.getChildSize(maxHeightIndex).height + margin.top + margin.bottom;
        // 找到坐标后直接平移到对应位置画出来
        context.paintChild(i, transform: Matrix4.translationValues(x, y, 0.0));
        // 下一次的x坐标需要将它加上自己的宽度，和自己的左右边距
        x += context.getChildSize(i).width + margin.left + margin.right;
      }
    }
  }

  @override
  bool shouldRepaint(FlowDelegate oldDelegate) {
    return oldDelegate != this;
  }
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191104232432892.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzc5Njg5,size_16,color_FFFFFF,t_70)

## Table

**1、简介**

* Table控件具有控制宽度和位置的表格控件

**2、构造函数**

```dart
Table({
  Key key,
  this.children = const <TableRow>[],
  this.columnWidths,
  this.defaultColumnWidth = const FlexColumnWidth(1.0),
  this.textDirection,
  this.border,
  this.defaultVerticalAlignment = TableCellVerticalAlignment.top,
  this.textBaseline,
})
```

* children：子控件集合
* columnWidths：表格的宽度
* defaultColumnWidth：默认表格的宽度
    * top：顶部
    * middle：垂直居中
    * bottom：底部
    * baseline：文本baseline对齐
    * fill：充满整个单元
* textDirection：文字的对齐方式
* border：表格的边框
* defaultVerticalAlignment：默认的表格位置对齐方式
* textBaseline：文字baseline类型
    * alphabetic：对齐字符底部的水平线
    * ideographic：对齐表意字符的水平线

**3、例子**

将文字居底对齐的表格

```dart
Widget _buildColumn() {
    return Table(
        textDirection: TextDirection.ltr,
        textBaseline: TextBaseline.alphabetic,
        defaultColumnWidth: FixedColumnWidth(80.0),
        defaultVerticalAlignment: TableCellVerticalAlignment.bottom,
        border:
            TableBorder.all(color: Colors.blueGrey, style: BorderStyle.solid),
        columnWidths: {
          0: FixedColumnWidth(50.0),
          1: FixedColumnWidth(100.0),
          2: FixedColumnWidth(100.0),
        },
        children: <TableRow>[
          TableRow(children: [
            Text("序号"),
            Text("名字"),
            Text("成绩"),
          ]),
          TableRow(children: [
            Text("1"),
            Text("张三"),
            Text("80"),
          ]),
          TableRow(children: [
            Text("2"),
            Text("李四"),
            Text("88"),
          ]),
          TableRow(children: [
            Text("3"),
            Text("王五"),
            Text("92"),
          ])
        ]);
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191104232440535.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzc5Njg5,size_16,color_FFFFFF,t_70)

## Wrap

**1、简介**

* Wrap控件相当于流式布局，会自动换行，比Flex自定义的功能好用

**2、构造函数**

```dart
Wrap({
  Key key,
  this.direction = Axis.horizontal,
  this.alignment = WrapAlignment.start,
  this.spacing = 0.0,
  this.runAlignment = WrapAlignment.start,
  this.runSpacing = 0.0,
  this.crossAxisAlignment = WrapCrossAlignment.start,
  this.textDirection,
  this.verticalDirection = VerticalDirection.down,
  List<Widget> children = const <Widget>[],
})
```

* direction：主轴的方向
    * Axis.horizontal：横向排布
    * Axis.vertical：竖向排布
* alignment：主轴方向上的对齐方式
* spacing：主轴方向上的间距
* runAlignment：横向排布的话，表示一行的对齐方式，竖向排布的话，表示一列的对齐方式
* runSpacing：一行或者一列方向上的间距
* crossAxisAlignment：侧轴方向的对齐方式
* textDirection：文本的对齐方式
* verticalDirection：子控件的排布方式
    * down：从左上角到右下角进行布局
    * up：从右下角到左上角进行布局 
* children：子控件集合

**3、例子**

通过Wrap控件创建出竖向的流式布局

```dart
Widget _buildColumn() {
    return Wrap(
      textDirection: TextDirection.ltr,
      alignment: WrapAlignment.center,
      verticalDirection: VerticalDirection.down,
      crossAxisAlignment: WrapCrossAlignment.center,
      direction: Axis.horizontal,
      runAlignment: WrapAlignment.center,
      runSpacing: 10.0,
      spacing: 10.0,
      children: <Widget>[
        Chip(
          label: Text("张三张三张三"),
        ),
        Chip(
          label: Text("李四李四李四"),
        ),
        Chip(
          label: Text("王五王五王五"),
        ),
        Chip(
          label: Text("赵六赵六赵六"),
        ),
        Chip(
          label: Text("钱七"),
        ),
        Chip(
          label: Text("孙八"),
        ),
      ],
    );
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191104232447722.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzc5Njg5,size_16,color_FFFFFF,t_70)

## ListBody

**1、简介**

* ListBody控件一般会配合ListView使用，属于ListView的子节点
* ListBody控件的作用是按给定的轴方向，按照顺序排列子节点

**2、构造函数**

```dart
ListBody({
  Key key,
  this.mainAxis = Axis.vertical,
  this.reverse = false,
  List<Widget> children = const <Widget>[],
})
```

* mainAxis：主轴方向
    * Axis.vertical：垂直方向
    * Axis.horizontal：横向方向
* reverse：是否控件翻转过来
* children：子控件集合

**3、例子**

显示3个不同颜色的容器，由于其父容器是`Flex`，会导致`ListBody`的侧轴被拉升到最大

```dart
Widget _buildColumn() {
    return Flex(
      direction: Axis.vertical,
      children: <Widget>[
        ListBody(
          mainAxis: Axis.vertical,
          reverse: false,
          children: <Widget>[
            Container(
              height: 50,
              width: 50,
              color: Colors.blueAccent,
            ),
            Container(
              height: 50,
              width: 50,
              color: Colors.redAccent,
            ),
            Container(
              height: 50,
              width: 50,
              color: Colors.greenAccent,
            )
          ],
        ),
      ],
    );
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191104232454796.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzc5Njg5,size_16,color_FFFFFF,t_70)

## ListView

**1、简介**

* ListView控件是个功能丰富的列表组件

**2、构造函数**

```dart
ListView({
  Key key,
  Axis scrollDirection = Axis.vertical,
  bool reverse = false,
  ScrollController controller,
  bool primary,
  ScrollPhysics physics,
  bool shrinkWrap = false,
  EdgeInsetsGeometry padding,
  this.itemExtent,
  bool addAutomaticKeepAlives = true,
  bool addRepaintBoundaries = true,
  double cacheExtent,
  List<Widget> children = const <Widget>[],
})
```

* scrollDirection：滚动放向
* reverse：子控件是否翻转
* controller：用来控制滚动位置及监听滚动事件
* primary：当内容不足以滚动时，是否支持滚动
* physics：控制用户滚动视图的交互
    * AlwaysScrollableScrollPhysics：列表总是可滚动的
    * PageScrollPhysics：一页一页的列表滑动，一般用于PageView控件用的滑动效果，滑动到末尾会有比较大的弹起
    * ClampingScrollPhysics：滚动时没有回弹效果
    * NeverScrollableScrollPhysics：就算内容超过列表范围也不会滑动
    * BouncingScrollPhysics：不论什么平台都会有回弹效果
    * FixedExtentScrollPhysics：仅滚动到子项而不存在任何偏移，必须与使用FixedExtentScrollController的可滚动对象一起使用
* shrinkWrap：是否根据子widget的总长度来设置ListView的长度
* padding：父控件的内边距
* itemExtent：指定子控件的固定高度
* addAutomaticKeepAlives：是否将子控件包裹在AutomaticKeepAlive控件内
* addRepaintBoundaries：是否将子控件包裹在 RepaintBoundary 控件内。用于避免列表滚动时的重绘
* cacheExtent：可见区域的前后会有一定高度的空间去缓存子控件，当滑动时就可以迅速呈现
* children：子控件集合

**3、例子**

创建三个具有回弹功能的列表控件

```dart
Widget _buildColumn() {
    return ListView(
      physics: BouncingScrollPhysics(),
      cacheExtent: 10.0,
      primary: true,
      padding: EdgeInsets.all(15.0),
      reverse: false,
      scrollDirection: Axis.vertical,
      children: <Widget>[
        Container(
          height: 300,
          width: 300,
          color: Colors.blueAccent,
        ),
        Container(
          height: 300,
          width: 300,
          color: Colors.redAccent,
        ),
        Container(
          height: 300,
          width: 300,
          color: Colors.greenAccent,
        )
      ],
    );
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191104232502357.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzc5Njg5,size_16,color_FFFFFF,t_70)

## CustomMultiChildLayout

**1、简介**

* CustomMultiChildLayout控件和CustomSingleChildLayout类似，区别于CustomMultiChildLayout可以控制多个控件
* CustomMultiChildLayout控件控制的子控件是通过Id进行区分和摆放

**2、构造函数**

```dart
CustomMultiChildLayout({
  Key key,
  @required this.delegate,
  List<Widget> children = const <Widget>[],
})
```

* delegate：控制子控件集合的代理类
* children：子控件集合

**3、例子**

首先创建控件的代理类，包括控件的大小和控件的位置，通过id获取传递过来的子控件，将`description`的控件放置在`title`下方

```dart
class IdLayoutDelegate extends MultiChildLayoutDelegate {
  IdLayoutDelegate();

  @override
  void performLayout(Size size) {
    BoxConstraints constraints = BoxConstraints(maxWidth: size.width);

    // 通过id获取对应的控件大小
    Size titleSize = layoutChild("title", constraints);
    Size descriptionSize = layoutChild("description", constraints);

    // 摆放id的控件位置
    positionChild("title", Offset(0.0, 0.0));
    positionChild("description", Offset(0.0, titleSize.height));
  }

  @override
  bool shouldRelayout(MultiChildLayoutDelegate oldDelegate) {
    return oldDelegate != null;
  }
}
```

通过id将对应的控件摆布在对应的位置

```dart
Widget _buildColumn() {
    return CustomMultiChildLayout(
      delegate: IdLayoutDelegate(),
      children: <Widget>[
        LayoutId(
          id: "title",
          child: Text("Hensen"),
        ),
        LayoutId(
          id: "description",
          child: Text("Flutter工程师"),
        )
      ],
    );
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191104232508256.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzc5Njg5,size_16,color_FFFFFF,t_70)

## LayoutBuilder

**1、简介**

* LayoutBuilder控件可以通过获取父控件的约束条件，从而控制布局的返回结果

**2、构造函数**

```dart
const LayoutBuilder({
    Key key,
    LayoutWidgetBuilder builder,
})
```

* builder：子控件的构建者

**3、例子**

通过判断父控件的尺寸大小，如果是大尺寸，就用大图标，如果是小尺寸，就用小图标

```dart
Widget _buildColumn() {
    return LayoutBuilder(
      builder: (BuildContext context, BoxConstraints constraints) {
        if (constraints.maxWidth > 200.0) {
          // 尺寸大的
          return FlutterLogo(size: 200);
        }
        // 尺寸小的
        return FlutterLogo(size: 50);
      },
    );
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191104232514469.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzc5Njg5,size_16,color_FFFFFF,t_70)