

# NestedScrollView

一个可以嵌套滚动视图的滚动组件

### 一、NestedScrollView的构造函数
它的构造函数有两个是必须的参数，一个是headerSliverBuilder，用于构造一个滚动视图的头部，一个是body，它可以是一个ListView组件。headerSliverBuilder和SliverAppBar结合使用，可以实现滚动的时候隐藏AppBar的效果。它同时提供了自定义ScrollController来解决滚动冲突的问题。

```
class NestedScrollViewDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return NestedScrollView(
        headerSliverBuilder: (BuildContext context, bool innerBoxIsScrolled) {
          return <Widget>[SliverAppBar(title: Text("hello title"))];
        },
        body: ListView.builder(
            itemCount: 50,
            itemBuilder: (BuildContext context, int index) {
              return Container(
                height: 100,
                color: Colors.green,
                child: Center(
                  child: Text("hello world $index"),
                ),
              );
            }));
  }
}
```

### 二、常用的属性

#### [body](https://api.flutter.dev/flutter/widgets/NestedScrollView/body.html)
NestedScrollView内部嵌套的组件

#### [controller](https://api.flutter.dev/flutter/widgets/NestedScrollView/controller.html)
可以使用这个controller来控制视图的滚动到特定的位置

### [headerSliverBuilder](https://api.flutter.dev/flutter/widgets/NestedScrollView/headerSliverBuilder.html)
用于构造嵌套滚动视图内部的滚动头部

### [scrollDirection](https://api.flutter.dev/flutter/widgets/NestedScrollView/scrollDirection.html)
滚动的方向
