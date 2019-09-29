# ListView

### 一、构造ListView的四种方式
#### 1、 通过默认的children 属性来构造
我们可以利用ListView的children属性通过List\<Widget\>来构造一个列表，但通过这种方式的只适用具有少量子视图的列表，因为通过这种方式构造列表，列表中的每个子组件都需要做些耗时的操作，而不是只针对那些只显示出来的子组件。

```
class ListView1 extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ListView(
      padding: EdgeInsets.all(10.0),
      children: <Widget>[
        Container(
          height: 50,
          color: Colors.red,
          child: const Center(
            child: const Text("hello world1"),
          ),
        ),
        Container(
          height: 50,
          color: Colors.blue,
          child: const Center(
            child: const Text("hello world2"),
          ),
        ),
        Container(
          height: 50,
          color: Colors.green,
          child: const Center(
            child: const Text("hello world3"),
          ),
        )
      ],
    );
  }
}
```

#### 2、通过ListView.builder构造
ListVIew.builder构造函数适用于具有大量子视图的列表，因为构造器只会生成那些只有在列表中实际可见的子视图，builder可以通过IndexedWidgetBuilder根据需要来生成这些子视图。

```
class ListView2 extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ListView.builder(
        itemCount: 100, //构造100个子视图
        itemBuilder: (BuildContext context, int index) {
          return Container(
            height: 50,
            color: Colors.green,
            padding: EdgeInsets.all(10.0),
            child: Center(
              child: Text("hello world $index"),
            ),
          );
        });
  }
}
```

####  3、通过ListView.separated构造
ListView.separated构造函数可以接受两个IndexedWidgetBuilder，itemBuilder根据需要来构造子视图，而separatorBuilder更倾向于是用来构造两个子视图之间的分割元素，此构造函数适用于具有固定数量子视图的列表。

```
class ListView3 extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ListView.separated(
        itemCount: 100, //构造100个子视图
        //构造视图之间的分割线
        separatorBuilder: (BuildContext context, int index) => const Divider(),
        itemBuilder: (BuildContext context, int index) => Container(
              height: 50,
              color: Colors.green,
              padding: EdgeInsets.all(10.0),
              child: Center(
                child: Text("hello world $index"),
              ),
            ));
  }
}
```

#### 4、通过ListView.custom构造
可以使用ListView.custom的SliverChildDelegate来构造一个列表，它提供了制定子视图的能力。例如，使用它可以计算出不可见子视图的实际大小等。SliverChildDelegate提供了两个默认的实现类，一个是SliverChildListDelegate，提供通过List\<Widget\>来构造一个列表的能力，一个是SliverChildBuilderDelegate，可以通过接受IndexedWidgetBuilder来构造一个列表。

```
class ListView4 extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ListView.custom(
      //默认的构造函数可以同List<Widget>来构造一个列表
      childrenDelegate: SliverChildListDelegate(<Widget>[
        Container(
          height: 50,
          color: Colors.red,
          child: const Center(
            child: const Text("hello world1"),
          ),
        ),
        Container(
          height: 50,
          color: Colors.blue,
          child: const Center(
            child: const Text("hello world2"),
          ),
        )
      ]),
    );
  }
}
```

```
class ListView5 extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ListView.custom(
      //默认的构造函数可以接受一个IndexedWidgetBuilder来构造一个列表
      childrenDelegate: SliverChildBuilderDelegate(
              (BuildContext context, int index) => Container(
            height: 50,
            color: Colors.red,
            child: Center(
              child: Text("hello world $index"),
            ),
          )),
    );
  }
}
```

### 二、 常用的一些属性

#### [childrenDelegate](https://api.flutter.dev/flutter/widgets/ListView/childrenDelegate.html)
构造子视图的代理

#### [itemExtent](https://api.flutter.dev/flutter/widgets/ListView/itemExtent.html)
如果不为空，则强制子元素在滚动方向上具有给定的范围

#### [cacheExtent](https://api.flutter.dev/flutter/widgets/ScrollView/cacheExtent.html) 
用于缓存列表滚动时即将要显示子视图的数量

#### [controller](https://api.flutter.dev/flutter/widgets/ScrollView/controller.html)
可用于控制此滚动视图被滚动到的位置的对象

### [padding](https://api.flutter.dev/flutter/widgets/BoxScrollView/padding.html)
子视图的内边距

#### [reverse](https://api.flutter.dev/flutter/widgets/ScrollView/reverse.html)  
是否是反向滚动，就是向上滚动

#### [scrollDirection](https://api.flutter.dev/flutter/widgets/ScrollView/scrollDirection.html)
视图的滚动方向


### 三、常用的一些方法

#### [buildChildLayout](https://api.flutter.dev/flutter/widgets/ListView/buildChildLayout.html)([BuildContext](https://api.flutter.dev/flutter/widgets/BuildContext-class.html)  context)
可以通过重写此方法来构建一个布局组件

#### [build](https://api.flutter.dev/flutter/widgets/ScrollView/build.html)([BuildContext](https://api.flutter.dev/flutter/widgets/BuildContext-class.html)  context)

重写此方法构造一个组件可以表示当前的用户界面
