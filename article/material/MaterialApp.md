
#### 一、控件介绍
一个用于材料设计的容器组件，是我们定义子控件的一个容器，它的构造函数里面虽然有多个参数，但是基本上大多数参数都是可以省略的。

#### 二、使用方法

```dart
    MaterialApp(
      title: 'TabBar', //用于为用户识别应用程序的单行描述
      theme: ThemeData(
        //应用各种 UI 所使用的主题颜色
        primarySwatch: Colors.red,
      ),
      color: Colors.red, //操作系统界面中用于应用程序的主要颜色,在Android上，这是应用程序切换器中应用程序使用的颜色。
      home: MaterialAppDemo(), //MaterialApp 显示的主界面
      routes: <String, WidgetBuilder>{
        // 应用的顶级导航表格，这个是多页面应用用来控制页面跳转的，类似于网页的网址
        "/MaterialApp": (BuildContext context) => TabBarView(),
      },
      initialRoute: '', //第一个显示的路由名字，默认值为 Window.defaultRouteName
      navigatorObservers: List<NavigatorObserver>(),
      debugShowMaterialGrid: false, //是否显示 纸墨设计 基础布局网格，用来调试 UI 的工具
//      showPerformanceOverlay:true,//显示性能标签，https://flutter.io/debugging/#performanceoverlay
//      showSemanticsDebugger: true,
//      debugShowCheckedModeBanner: true,//性能调试工具
    )
  
```

#### 三、常用属性
1.设置titile,这个和启动图标名字是不一样的，和当前 Activity 的名字也是不一样的。 这个 Title 是用来定义任务管理窗口界面所看到应用名字的。在原生 Android 系统中点击圆圈 Home 按钮右边的方块按钮就会打开多任务切换窗口。

```dart
  title: 'MaterialApp',//用于为用户识别应用程序的单行描述
```

2.定义应用所使用的主题颜色，在材料设计中定义了 primaryColor、accentColor、hintColor 等颜色值。可以通过这个来指定一个 ThemeData 定义应用中每个控件的颜色。

```
  theme: ThemeData(
    //应用各种 UI 所使用的主题颜色
    primarySwatch: Colors.red,
  ),

```
3、定义主界面的显示控件，这个是一个 Widget 对象，用来定义当前应用打开的时候，所显示的界面。
```
 home: MaterialAppDemo(), //MaterialApp 显示的主界面
 
 class MaterialAppDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Material Appbar'),
      ),
      body: Center(
        child: Text('MaterialApp Demo'),
      ),
    );
  }
}

```

4、定义页面跳转的路由规则，定义应用中页面跳转规则。 该对象是一个 Map<String, WidgetBuilder>。
当使用 Navigator.pushNamed 来路由的时候，会在 routes 查找路由名字，然后使用 对应的 WidgetBuilder 来构造一个带有页面切换动画的 MaterialPageRoute。如果应用只有一个界面，则不用设置这个属性，使用 home 设置这个界面即可。
```
  routes: <String, WidgetBuilder>{
    // 应用的顶级导航表格，这个是多页面应用用来控制页面跳转的，类似于网页的网址
    "/MaterialApp": (BuildContext context) => TabBarView(),
  },

```
5、一系列调试工具
```
    debugShowMaterialGrid: false, //是否显示 材料设计 基础布局网格，用来调试 UI 的工具

```
```
  showPerformanceOverlay:
      true, // 显示性能标签，https://flutter.io/debugging/#performanceoverlay
  showSemanticsDebugger: true,
  debugShowCheckedModeBanner: true,//性能调试工具

```


#### 四、一个完整的例子



```dart

import 'dart:ui';
import 'package:flutter/gestures.dart';
import 'package:flutter/material.dart';

void main() => runApp(MaterialApp(
      title: 'MaterialApp', //用于为用户识别应用程序的单行描述
      theme: ThemeData(
        //应用各种 UI 所使用的主题颜色
        primarySwatch: Colors.red,
      ),
      color: Colors.red, //操作系统界面中用于应用程序的主要颜色,在Android上，这是应用程序切换器中应用程序使用的颜色。
      home: MaterialAppDemo(), //MaterialApp 显示的主界面
      routes: <String, WidgetBuilder>{
        // 应用的顶级导航表格，这个是多页面应用用来控制页面跳转的，类似于网页的网址
        "/MaterialApp": (BuildContext context) => TabBarView(),
      },
      initialRoute: '', //第一个显示的路由名字，默认值为 Window.defaultRouteName
      navigatorObservers: List<NavigatorObserver>(),
      debugShowMaterialGrid: false, //是否显示 材料设计 基础布局网格，用来调试 UI 的工具
//      showPerformanceOverlay:
//          true, // 显示性能标签，https://flutter.io/debugging/#performanceoverlay
//      showSemanticsDebugger: true,
//      debugShowCheckedModeBanner: true,//性能调试工具
    ));

class MaterialAppDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Material Appbar'),
      ),
      body: Center(
        child: Text('MaterialApp Demo'),
      ),
    );
  }
}

```
