# CustomScrollView

它超级强悍，它可以支持多种滚动组件联合滚动。例如你可以使用它来创建一个混合的滚动组件，包括ListView和GridView，并且保证他们滚动是保持一致的，但如果你不使用CustomScrollView的话，ListView和GridView自身的内容滚动效果是分开的。
需要注意的是，CustomScrollView仅支持Sliver系列的子组件，但ListView和GridView等都有相对应的Sliver实现的组件，如果SliverList和SliverGrid等。

常用的Sliver组件有：[SliverList](https://api.flutter.dev/flutter/widgets/SliverList-class.html)、[SliverFixedExtentList](https://api.flutter.dev/flutter/widgets/SliverFixedExtentList-class.html)、[SliverGrid](https://api.flutter.dev/flutter/widgets/SliverGrid-class.html)、[SliverPadding](https://api.flutter.dev/flutter/widgets/SliverPadding-class.html)、[SliverAppBar](https://api.flutter.dev/flutter/material/SliverAppBar-class.html)

```
class SingleChildScrollViewDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CustomScrollView(
      slivers: <Widget>[
        SliverGrid.count(
          crossAxisCount: 2,
          children: <Widget>[
            Container(
              height: 50,
              color: Colors.blue,
              child: Center(
                child: const Text("Hello world1"),
              ),
            ),
            Container(
              height: 50,
              color: Colors.blue,
              child: Center(
                child: const Text("Hello world2"),
              ),
            ),
            Container(
              height: 50,
              color: Colors.blue,
              child: Center(
                child: const Text("Hello world3"),
              ),
            )
          ],
        ),
        SliverList(
          delegate: SliverChildListDelegate(<Widget>[
            Container(
              height: 150,
              color: Colors.blue,
              child: Center(
                child: const Text("Hello world1"),
              ),
            ),
            Container(
              height: 150,
              color: Colors.blue,
              child: Center(
                child: const Text("Hello world2"),
              ),
            ),
            Container(
              height: 150,
              color: Colors.blue,
              child: Center(
                child: const Text("Hello world3"),
              ),
            )
          ]),
        )
      ],
    );
  }
}

```
