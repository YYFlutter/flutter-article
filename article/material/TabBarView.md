
#### 一、控件介绍
一个用于显示切换的内容区域的视图控件，常用于与tabBar结合使用，abBar就是导航栏，TabBarView就是导航栏当前所对应的内容区，也可以单独使用做滑动切换的效果类似android的viewpager。

#### 二、使用方法

```
TabBarView(
    children: mTabView,//用于切换的子控件列表，若要合TabBar一起使用注意和TabBar的长度一样
    controller:_tabController,//控制器，若TabBar一起使用注意和TabBar使用同一个controller ，这样才能保证两者的联动关系
    physics: ScrollPhysics()), //暂时还未查到是什么作用
    drawerDragStartBehavior: DragStartBehavior.start, //暂时还未查到是什么作用
    );
  
```

#### 三、常用属性
1.设置切换的子控件列表，若要合TabBar一起使用注意和TabBar的长度一样
```dart
  children: mTabView,//用于切换的子控件列表，若要合TabBar一起使用注意和TabBar的长度一样
```

```
    var mTabView = [
    Container(
      child: Center(
        child: Text(
          '1',
          style: TextStyle(fontSize: 50),
        ),
      ),
      color: Colors.green,
    ),
    Container(
      child: Center(
        child: Text(
          '2',
          style: TextStyle(fontSize: 50),
        ),
      ),
      color: Colors.yellow,
    ),
    Container(
      child: Center(
        child: Text(
          '3',
          style: TextStyle(fontSize: 50),
        ),
      ),
      color: Colors.red,
    )
  ]; //使用widget的形式

```
2.设置TabController对象（控制器，如果和TabBar一起使用注意和TabBar使用同一个controller）

```
  controller:TabController(vsync: this, length: mTabView.length) //TabController对象

```

#### 四、总结

##### 1、TabBarView 一个用于显示切换的内容区域的视图控件，类似android开发的viewpager控件，常用于与tabbar结合使用，与tabbar结合使用时，若要进行两者的联动，要用同一个TabController，如下面的完整例子所示
##### 2、若要对TabBarView 的切换进行监听可以通过TabController.addListener 进行监听
```
  @override
  void initState() {
    super.initState();
    _tabController = TabController(vsync: this, length: mTabView.length);
    //监听tab切换的回调
    _tabController.addListener(() {
      var index = _tabController.index;
      print('tab 切换了 $index');
    });
  }

```

##### 3、使用TabController 时对应的类要实现 TickerProviderStateMixin 接口，见下面完整例子，若用DefaultTabController 则简单很多，由于应用在无状态控件中，使用DefaultTabController包裹需要用到Tab的页面即可，也可以不用实现对应的接口。
```
class TabbedAppBarSample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      home: new DefaultTabController(
        length: choices.length,
        child: new Scaffold(
          appBar: new AppBar(
            title: const Text('Tabbed AppBar'),
            bottom: new TabBar(
              isScrollable: true,
              tabs: choices.map((Choice choice) {
                return new Tab(
                  text: choice.title,
                  icon: new Icon(choice.icon),
                );
              }).toList(),
            ),
          ),
          body: new TabBarView(
            children: choices.map((Choice choice) {
              return new Padding(
                padding: const EdgeInsets.all(16.0),
                child: new ChoiceCard(choice: choice),
              );
            }).toList(),
          ),
        ),
      ),
    );
  }
}

```




#### 五、一个完整的例子


![](https://user-gold-cdn.xitu.io/2019/7/31/16c46f2d5096f452?w=502&h=729&f=gif&s=122927)


![](https://user-gold-cdn.xitu.io/2019/7/31/16c46f2f0d0addda?w=463&h=707&f=gif&s=630314)


```dart

import 'dart:ui';
import 'package:flutter/gestures.dart';
import 'package:flutter/material.dart';

void main() => runApp(MaterialApp(
      title: 'TabBar',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: TabBarViewPage(),
    ));

// This app is a stateful, it tracks the user's current choice.
class TabBarViewPage extends StatefulWidget {
  TabBarViewPage({Key key}) : super(key: key);
  @override
  _TabBarViewPageState createState() => _TabBarViewPageState();
}

class _TabBarViewPageState extends State<TabBarViewPage>
    with TickerProviderStateMixin {
  var mTab = [
    Tab(text: 'tab1', icon: Icon(Icons.ac_unit)),
    Tab(text: 'tab2', icon: Icon(Icons.link)),
    Tab(text: 'tab3', icon: Icon(Icons.directions_run))
  ];
  var mTabView = [
    Container(
      child: Center(
        child: Text(
          '1',
          style: TextStyle(fontSize: 50),
        ),
      ),
      color: Colors.green,
    ),
    Container(
      child: Center(
        child: Text(
          '2',
          style: TextStyle(fontSize: 50),
        ),
      ),
      color: Colors.yellow,
    ),
    Container(
      child: Center(
        child: Text(
          '3',
          style: TextStyle(fontSize: 50),
        ),
      ),
      color: Colors.red,
    )
  ];

  TabController _tabController;
  @override
  void initState() {
    super.initState();
    _tabController = TabController(vsync: this, length: mTabView.length);
    //监听tab切换的回调
    _tabController.addListener(() {
      var index = _tabController.index;
      print('tab 切换了 $index');
    });
  }

  @override
  void dispose() {
    _tabController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('TabBarView Demo'),
        bottom: TabBar(
          tabs: mTab, //设置tabbar 的标签显示内容，一般使用Tab对象,当然也可以是其他的Widget
          controller: _tabController, //TabController对象
          isScrollable: true, //是否可滚动
          indicatorColor: Colors.lightBlueAccent, //指示器颜色
          indicatorWeight: 10.0, //指示器的高度
          indicatorPadding: EdgeInsets.all(10), //底部指示器的Padding
          indicator: BoxDecoration(
              border: Border.all(
                  width: 1, color: Colors.black)), //指示器decoration，例如边框、颜色等
          indicatorSize: TabBarIndicatorSize
              .tab, //指示器大小计算方式,label 为以文本为边框计算，tab 为以指示器为边框计算
          labelColor: Colors.yellowAccent, //tab 标签颜色
          labelStyle: TextStyle(color: Colors.black, fontSize: 20), //设置标签样式
          unselectedLabelColor: Colors.redAccent, //未选中Tab中文字颜色
          unselectedLabelStyle:
              TextStyle(color: Colors.red, fontSize: 25), //未选中Tab中文字style
        ),
        //tab 文字样式
      ),
      body: TabBarView(
          children: mTabView, //一系列子控件，如果和TabBar一起使用注意和TabBar的长度一样
          controller:
              _tabController, //控制器，如果和TabBar一起使用注意和TabBar使用同一个controller
          physics: ScrollPhysics()), //??
      drawerDragStartBehavior: DragStartBehavior.start, //?
    );
  }
}




```
