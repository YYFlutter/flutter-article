# GridView
### 一、构造GridView的四种方式

#### 1、通过GridView.count来构造
子视图的数量是固定的，可以通过此方式来构造

```
class GridViewDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return GridView.count(crossAxisCount: 3, children: <Widget>[
      Center(
        child: Text("hello world1"),
      ),
      Center(
        child: Text("hello world2"),
      ),
      Center(
        child: Text("hello world3"),
      ),
      Center(
        child: Text("hello world4"),
      ),
      Center(
        child: Text("hello world5"),
      )
    ]);
  }
}
```

#### 2、通过GridView.builder来构造
和ListView.builder一样，使用这个构造函数适用于具有大量子视图的列表，因为构造器只会生成那些只有在列表中实际可见的子视图，所以建议如果是子视图是根据需求来生成的，并且数量不是固定的，那么推荐使用这种方式来构建。使用该builder必现要给gridDelegate赋值，这个girdDelegate主要是用来计算网格每一行子视图的数量，它有两个已经实现的类，一个是SliverGridDelegateWithFixedCrossAxisCount，如果每一行的子视图的个数是固定的，那么就可以使用它来实现。如果每一行的子视图的个数不是固定的，那么可以使用SliverGridDelegateWithMaxCrossAxisExtent来控制最大容纳每个子视图的宽度。例如，网格宽度是500像素，而maxCrossAxisExtent是150像素，那么这个代理器会创建4列的网格出来。

```
class GridViewDemo1 extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return GridView.builder(
        itemCount: 50,
        gridDelegate: //每一列固定显示4个
            SliverGridDelegateWithFixedCrossAxisCount(crossAxisCount: 4),
        itemBuilder: (BuildContext context, int index) {
          return Center(
            child: Text("hello world $index"),
          );
        });
  }
}
```

```
lass GridViewDemo1 extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return GridView.builder(
        itemCount: 50,
        gridDelegate: //每一列最大元素宽度是100
        SliverGridDelegateWithMaxCrossAxisExtent(maxCrossAxisExtent: 100),
        itemBuilder: (BuildContext context, int index) {
          return Center(
            child: Text("hello world $index"),
          );
        });
  }
}
```

#### 3、通过GridView.custom来构造
使用custom可以最大自定义网格视图，gridDelegate负责计算网格每一列子视图的数量，而childrenDelegate就可以负责生成需要展示出来的子视图

```
class GridViewDemo2 extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return GridView.custom(
        gridDelegate:
            SliverGridDelegateWithFixedCrossAxisCount(crossAxisCount: 2),
        childrenDelegate: SliverChildListDelegate(<Widget>[
          Center(
            child: Text("hello world1"),
          ),
          Center(
            child: Text("hello world2"),
          ),
          Center(
            child: Text("hello world3"),
          )
        ]));
  }
}
```

#### 4、通过GridView.extent来构造
通过这种方式构建和GridView.count是差不多的，count是用来控制每一列的子视图数量，而extent中的maxCrossAxisExtent其实是和SliverGridDelegateWithMaxCrossAxisExtent中的maxCrossAxisExtent一样，用来计算每一列能容纳每个子视图的宽度

```
class GridViewDemo3 extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    //每个子视图最多能占用100像素，也可以说，网格每一格最大的宽度是100个像素，
    // 可以根据这个宽度来计算出一列该显示多个元素
    return GridView.extent(maxCrossAxisExtent: 100, children: <Widget>[
      Center(
        child: Text("hello world1"),
      ),
      Center(
        child: Text("hello world2"),
      ),
      Center(
        child: Text("hello world3"),
      )
    ]);
  }
}
```
### 二、常用的属性

#### [childrenDelegate](https://api.flutter.dev/flutter/widgets/GridView/childrenDelegate.html)
用于构造子视图的代理器

#### [gridDelegate](https://api.flutter.dev/flutter/widgets/GridView/gridDelegate.html)
用于计算网格每一列元素个数的代理器

#### [controller](https://api.flutter.dev/flutter/widgets/ScrollView/controller.html)
可用于控制网格视图滚动到指定位置的对象
