# Flutter 系列文章：Flutter TabBar 控件介绍
#### 一、控件介绍
一个顶部导航栏控件，用于进行不同视图的切换，跟BottomNavigationBar类似，顶部导航栏可以由文本、图标 或者两者结合的形式组成，顶导航栏统筹与Scaffold结合使用，它通常作为Scaffold.appBar参数提供。
#### 二、使用方法

```
TabBar(
      tabs: widget.mTab, //设置tabbar 的标签显示内容，一般使用Tab对象,当然也可以是其他的Widget
      controller:TabController(length: 3, vsync: this), //TabController对象
      isScrollable: true, //是否可滚动
      indicatorColor: Colors.lightBlueAccent, //指示器颜色
      indicatorWeight: 10.0, //指示器的高度
      indicatorPadding: EdgeInsets.all(10), //底部指示器的Padding
      indicator: BoxDecoration(
          border: Border.all(
          width: 1, color: Colors.black)), //指示器decoration，例如边框、颜色等
      indicatorSize: TabBarIndicatorSize.tab, //指示器大小计算方式,label 为以文本为边框计算，tab 为以指示器为边框计算
      labelColor: Colors.yellowAccent, //tab 标签颜色
      labelStyle: TextStyle(color: Colors.black, fontSize: 20),
      unselectedLabelColor: Colors.redAccent, //未选中Tab中文字颜色
      unselectedLabelStyle:TextStyle(color: Colors.red, fontSize: 25),//未选中Tab中文字style
      )
  
```

#### 二、常用属性
1.设置tabbar 的标签显示内容，一般使用Tab对象,当然也可以是其他的Widget
```dart
 tabs: widget.mTab, //设置tabbar 的标签显示内容，使用Tab对象
 
  var mTab = [
    Tab(text: 'tab1', icon: Icon(Icons.ac_unit)),
    Tab(text: 'tab2', icon: Icon(Icons.link)),
    Tab(text: 'tab3', icon: Icon(Icons.directions_run))
  ];

```

```
  tabs: [Text('tab1'), Text('tab2'), Text('tab3')]  //使用widget的形式

```
2.设置TabController对象

```
  controller:TabController(length: 3, vsync: this), //TabController对象

```
3.是否可滚动

```dart
  isScrollable: true, // 是否可滚动
```
4.设置指示器颜色

```
  indicatorColor: Colors.lightBlueAccent, //指示器颜色
```
5.指示器的高度

```
   indicatorWeight: 10.0, //指示器的高度
```
6.底部指示器的Padding

```
   indicatorPadding: EdgeInsets.all(10), //底部指示器的Padding
```
7.指示器decoration，例如边框、颜色等

```dart
  indicator: BoxDecoration(
      border: Border.all(
              width: 1, 
              color: Colors.black
              )
          ), //指示器decoration，例如边框、颜色等
```
8.指示器大小计算方式,label 为以文本为边框计算，tab 为以指示器为边框计算

```
  indicatorSize: TabBarIndicatorSize.tab, //指示器大小计算方式,label为以文本为边框计算，tab 为以指示器为边框计算
```
9.tab 标签颜色

```
  labelColor: Colors.yellowAccent, //tab 标签颜色
```
10.设置标签样式

```
  labelStyle: TextStyle(color: Colors.black, fontSize: 20)
```
11.未选中Tab中文字颜色

```
  unselectedLabelColor: Colors.redAccent     
```
12.未选中Tab中文字style

```
  unselectedLabelStyle:TextStyle(color: Colors.red, fontSize: 25), //未选中Tab中文字style
```



#### 三、一个完整的例子


```dart

import 'dart:ui';
import 'package:flutter/material.dart';

void main() => runApp(MaterialApp(
      title: 'TabBar',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: TabBarPage(),
    ));

// This app is a stateful, it tracks the user's current choice.
class TabBarPage extends StatefulWidget {
  TabBarPage({Key key}) : super(key: key);
  var mTab = [
    Tab(text: 'tab1', icon: Icon(Icons.ac_unit)),
    Tab(text: 'tab2', icon: Icon(Icons.link)),
    Tab(text: 'tab3', icon: Icon(Icons.directions_run))
  ];
  @override
  _TabBarPageState createState() => _TabBarPageState();
}

class _TabBarPageState extends State<TabBarPage> with TickerProviderStateMixin {
  @override
  void initState() {
    super.initState();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
          title: Text('TabBar Demo'),
          bottom: TabBar(
            tabs: widget.mTab, //设置tabbar 的标签显示内容，一般使用Tab对象,当然也可以是其他的Widget
//              tabs: [Text('tab1'), Text('tab2'), Text('tab3')],
            controller: TabController(vsync: this, length: 3), //TabController对象
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
          ) //tab 文字样式

          ),
    );
  }
}


```
