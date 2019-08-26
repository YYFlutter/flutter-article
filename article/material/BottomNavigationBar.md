# Flutter 系列文章：Flutter BottomNavigationBar 控件介绍
#### 一、控件介绍
一个底部导航栏控件，用于进行不同视图的切换，底部导航栏可以由文本、图标 或者两者结合的形式组成，底部导航栏统筹与Scaffold结合使用，它通常作为Scaffold.bottomNavigationBar参数提供。
#### 二、使用方法

```
BottomNavigationBar（{
    Key key，
    @ required List < BottomNavigationBarItem > items，//放入导航栏的控件item列表长度items必须至少为2，每个项目的图标和标题不得为空，
    ValueChanged < int > onTap，//点击导航栏子item的时候的
    int currentIndex：0，//当前活动BottomNavigationBarItem的项目 索引。
    double elevation：8.0，//设置z 轴坐标，设置了并没有什么效果
    BottomNavigationBarType type，//底部导航栏的类型，有fixed和shifting两个类型，不同类型显示效果不一样
    Color fixedColor，//选中的时候的字体颜色，不能跟selectedItemColor 一起用
    Color backgroundColor，//导航栏背景颜色
    double iconSize：24.0，// icon的大小 ,设置了并木有效果
    Color selectedItemColor，//选中的时候的字体颜色，不能跟fixedColor 一起用
    Color unselectedItemColor，//未选中BottomNavigationBarItem标签 的字体大小
    IconThemeData selectedIconTheme： const IconThemeData（），//选中时的子Item的样式，这个不能跟BottomNavigationBarItem Icon 的colors 一起用，否则会以Icon 的colors为准，主题设置的不会生效，并且icon必须为官方的icon为主，否则也无法生效
    IconThemeData unselectedIconTheme： const IconThemeData（），              //未选中时的BottomNavigationBarItem.icon s中图标的大小，不透明度和颜色
    double selectedFontSize： 14.0，//选中的tab的字体的大小
    double unselectedFontSize： 12.0，//未选中BottomNavigationBarItem标签 的字体大小
    TextStyle selectedLabelStyle，//选中的时候的字体样式，设置了并没有生效
    TextStyle unselectedLabelStyle，//未选中时的字体样式，设置了并没有生效
    bool showSelectedLabels，//是否为未选择的BottomNavigationBarItem显示标签
    bool showUnselectedLabels,//是否为选定的BottomNavigationBarItem显示标签
}）

BottomNavigationBarItem({
    @required Widget icon,//设置icon图标
    Widget title,//设置标签控件
    Widget activeIcon,//选中的时候的标签控件
    Color backgroundColor,//BottomNavigationBarType为shifting时的背景颜色
  })
  
```

#### 二、常用属性
1.设置导航栏的子item控件，放入导航栏的控件item列表长度items必须至少为2，每个项目的图标和标题不得为空
```
            items: <BottomNavigationBarItem>[
              //放入导航栏的控件item列表长度items必须至少为2，每个项目的图标和标题不得为空
              BottomNavigationBarItem(
                  icon: Icon(
                    Icons.ac_unit,
//                    color: Colors.black,
                    size: 20,
                  ), //设置使用什么图标控件
                  title: Text('热门'), //设置使用什么文本控件
//                  activeIcon: getTabIcon(0), //选中时要显示的图标控件
                  backgroundColor:
                      Colors.red), //BottomNavigationBarType为shifting时的背景颜色
              BottomNavigationBarItem(
                  icon: getTabIcon(1), //设置使用什么图标控件
                  title: getTabTitle(1), //设置使用什么文本控件
                  activeIcon: getTabIcon(1), //选中时要显示的图标控件
                  backgroundColor: Colors.blue),
              BottomNavigationBarItem(
                  icon: getTabIcon(2), //设置使用什么图标控件
                  title: getTabTitle(2), //设置使用什么文本控件
                  activeIcon: getTabIcon(2), //选中时要显示的图标控件
                  backgroundColor: Colors.green)
            ],
```
2.导航栏子item点击的回调

```
            onTap: (index) {
              //点击导航栏子item的时候的
              setState(() {
                _tabIndex = index;
              });
            },
```
3.底部导航栏的类型，有fixed和shifting两个类型，不同类型显示效果不一样

```
            type: BottomNavigationBarType.fixed, //底部导航栏的类型，有fixed和shifting两个类型，不同类型显示效果不一样
```
4.选中的时候的字体颜色，不能跟selectedItemColor 一起用

```
            fixedColor: Colors.black, //选中的时候的字体颜色，不能跟selectedItemColor 一起用
```
5.设置icon大小

```
             iconSize: 200.0, // icon的大小
```
6.当前活动BottomNavigationBarItem的项目索引。

```
             currentIndex: _tabIndex
```
7.选中的tab的字体的大小

```
            selectedFontSize: 30, //选中的tab的字体的大小
```
8.导航栏背景颜色

```
             backgroundColor: Colors.lightBlueAccent, //导航栏背景颜色
```
9.选中时的子Item的样式，这个不能跟BottomNavigationBarItem Icon 的colors 一起用，否则会以Icon 的colors为准，主题设置的不会生效，并且icon必须为官方的icon为主，否则也无法生效

```
            selectedIconTheme: IconThemeData(
              //选中时的子Item的样式，这个不能跟BottomNavigationBarItem Icon 的colors 一起用，否则会以Icon 的colors为准，主题设置的不会生效，并且icon必须为官方的icon为主，否则也无法生效
              color: Colors.yellow,
              opacity: 0.7,
            ),
```
10.选中的时候的字体颜色，不能跟fixedColor 一起用

```
            selectedItemColor: Colors.yellow, //选中的时候的字体颜色，不能跟fixedColor 一起用
```
11.选中的时候的字体样式，设置了并没有生效

```
            selectedLabelStyle: TextStyle(
                color: Colors.yellow, fontSize: 20), //选中的时候的字体样式，设置了并没有生效        
```
12.是否为未选择的BottomNavigationBarItem显示标签,设置了没有看出什么效果

```
            showUnselectedLabels:
                true, //是否为未选择的BottomNavigationBarItem显示标签,设置了没有看出什么效果
```
13.未选中BottomNavigationBarItem标签 的字体大小

```
            unselectedFontSize: 25, //未选中BottomNavigationBarItem标签 的字体大小
```
14.未选中时的BottomNavigationBarItem.icon s中图标的大小，不透明度和颜色

```
            unselectedIconTheme: IconThemeData(
              //未选中时的BottomNavigationBarItem.icon s中图标的大小，不透明度和颜色
              color: Colors.pink,
              opacity: 0.7,
            ),
```
15.当前为选中的BottomNavigationBarItem.labels 的颜色

```
            unselectedItemColor:Colors.pink, //当前为选中的BottomNavigationBarItem.labels 的颜色
```
16.未选中时的字体样式，设置了并没有生效

```
            unselectedLabelStyle: TextStyle( color: Colors.green, fontSize: 15), //未选中时的字体样式，设置了并没有生效
```
17.选中的时候的字体样式，设置了并没有生效

```
         showSelectedLabels: true, //选中的时候的字体样式，设置了并没有生效
```

#### 三、总结
1.一个基础的底部导航栏控件，selectedIconTheme，selectedLabelStyle，selectedFontSize，showUnselectedLabels 与unselect相关的属性的设置的前提是
BottomNavigationBarItem，里面没有去设置相关的颜色、属性、样式等，否则会以BottomNavigationBarItem里面的属性设置为主，特别注意selectedIconTheme，unselectedIconTheme相关必须要用flutter的Icon 控件进行设置，自己提供的图片是无法设置这些属性的。

2.一般情况下选中跟未选中的时候，字体跟对应的图标都要统一切换为某一种颜色，这里可以用selectedIconTheme，unselectedIconTheme相关的属性，但这个仅限于用系统的图标，也可以使用BottomNavigationBarItem里面设置图标、字体的方式，若是自己的图标建议使用这种方式；

```

    /*
     * 初始化选中和未选中的icon
     */
    tabImages = [
      [
        getTabImage('images/tab_ic_home.png'),
        getTabImage('images/tab_ic_home_sel.png')
      ],
      [
        getTabImage('images/tab_ic_follow.png'),
        getTabImage('images/tab_ic_follow_sel.png')
      ],
      [
        getTabImage('images/tab_ic_profile.png'),
        getTabImage('images/tab_ic_profile_sel.png')
      ]
    ];
    
  /*
   * 根据选择获得对应的normal或是press的icon
   */
  Image getTabIcon(int curIndex) {
    if (curIndex == _tabIndex) {
      return tabImages[curIndex][1];
    }
    return tabImages[curIndex][0];
  }
  
    /*
   * 获取bottomTab的颜色和文字
   */
  Text getTabTitle(int curIndex) {
    if (curIndex == _tabIndex) {
      return Text(appBarTitles[curIndex],
          style: TextStyle(fontSize: 11.0, color: const Color(0xFFFE5823)));
    } else {
      return Text(appBarTitles[curIndex],
          style: TextStyle(fontSize: 11.0, color: const Color(0xFF999999)));
    }
  }

  /*
   * 根据image路径获取图片
   */
  Image getTabImage(path) {
    return Image.asset(path, width: 23.0, height: 23.0);
  }
  
  
```

#### 四、一个完整的例子


```

import 'dart:ui';
import 'package:flutter/material.dart';

void main() => runApp(MaterialApp(
      title: 'BottomNavigationBar',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: BottomNavigationBarPage(),
    ));

// This app is a stateful, it tracks the user's current choice.
class BottomNavigationBarPage extends StatefulWidget {
  BottomNavigationBarPage({Key key, this.uid}) : super(key: key);
  final int uid;

  @override
  _BottomNavigationBarPageState createState() =>
      _BottomNavigationBarPageState();
}

class _BottomNavigationBarPageState extends State<BottomNavigationBarPage>
    with SingleTickerProviderStateMixin {
  int _tabIndex = 0;
  var tabImages;
  var appBarTitles = ['首页', '发现', '我的'];
  /*
   * 存放三个页面，跟fragmentList一样
   */
  var _pageList;

  /*
   * 根据选择获得对应的normal或是press的icon
   */
  Image getTabIcon(int curIndex) {
    if (curIndex == _tabIndex) {
      return tabImages[curIndex][1];
    }
    return tabImages[curIndex][0];
  }

  /*
   * 获取bottomTab的颜色和文字
   */
  Text getTabTitle(int curIndex) {
    if (curIndex == _tabIndex) {
      return Text(appBarTitles[curIndex],
          style: TextStyle(fontSize: 11.0, color: const Color(0xFFFE5823)));
    } else {
      return Text(appBarTitles[curIndex],
          style: TextStyle(fontSize: 11.0, color: const Color(0xFF999999)));
    }
  }

  /*
   * 根据image路径获取图片
   */
  Image getTabImage(path) {
    return Image.asset(path, width: 23.0, height: 23.0);
  }

  void initData() {
    /*
     * 初始化选中和未选中的icon
     */
    tabImages = [
      [
        getTabImage('images/tab_ic_home.png'),
        getTabImage('images/tab_ic_home_sel.png')
      ],
      [
        getTabImage('images/tab_ic_follow.png'),
        getTabImage('images/tab_ic_follow_sel.png')
      ],
      [
        getTabImage('images/tab_ic_profile.png'),
        getTabImage('images/tab_ic_profile_sel.png')
      ]
    ];
    /*
     * 三个子界面
     */
    _pageList = [
      Center(
        child: Text('第一页'),
      ),
      Center(
        child: Text('第二页'),
      ),
      Center(
        child: Text('第三页'),
      ),
    ];
  }

  @override
  Widget build(BuildContext context) {
    //初始化数据
    initData();
    return Scaffold(
        body: _pageList[_tabIndex],
        bottomNavigationBar: Container(
          child: BottomNavigationBar(
            items: <BottomNavigationBarItem>[
              //放入导航栏的控件item列表长度items必须至少为2，每个项目的图标和标题不得为空
              BottomNavigationBarItem(
                  icon: Icon(
                    Icons.ac_unit,
//                    color: Colors.black,
                    size: 20,
                  ), //设置使用什么图标控件
                  title: Text('热门'), //设置使用什么文本控件
//                  activeIcon: getTabIcon(0), //选中时要显示的图标控件
                  backgroundColor:
                      Colors.red), //BottomNavigationBarType为shifting时的背景颜色
              BottomNavigationBarItem(
                  icon: getTabIcon(1), //设置使用什么图标控件
                  title: Text('控件'), //设置使用什么文本控件
//                  activeIcon: getTabIcon(1), //选中时要显示的图标控件
                  backgroundColor: Colors.blue),
              BottomNavigationBarItem(
                  icon: getTabIcon(2), //设置使用什么图标控件
                  title: getTabTitle(2), //设置使用什么文本控件
                  activeIcon: getTabIcon(2), //选中时要显示的图标控件
                  backgroundColor: Colors.green)
            ],
            onTap: (index) {
              //点击导航栏子item的时候的
              setState(() {
                _tabIndex = index;
              });
            },
            elevation: 150, //设置z 轴坐标，设置了并没有什么效果
            type: BottomNavigationBarType
                .fixed, //底部导航栏的类型，有fixed和shifting两个类型，不同类型显示效果不一样
            fixedColor: Colors.black, //选中的时候的字体颜色，不能跟selectedItemColor 一起用
            iconSize: 200.0, // icon的大小
            currentIndex: _tabIndex, //当前活动BottomNavigationBarItem的项目 索引。
            selectedFontSize: 30, //选中的tab的字体的大小
//            backgroundColor: Colors.lightBlueAccent, //导航栏背景颜色
            selectedIconTheme: IconThemeData(
              //选中时的子Item的样式，这个不能跟BottomNavigationBarItem Icon 的colors 一起用，否则会以Icon 的colors为准，主题设置的不会生效，并且icon必须为官方的icon为主，否则也无法生效
              color: Colors.yellow,
              opacity: 0.7,
            ),
//            selectedItemColor: Colors.yellow, //选中的时候的字体颜色，不能跟fixedColor 一起用
            selectedLabelStyle: TextStyle(
                color: Colors.yellow, fontSize: 20), //选中的时候的字体样式，设置了并没有生效
            showUnselectedLabels:
                true, //是否为未选择的BottomNavigationBarItem显示标签,设置了没有看出什么效果
            unselectedFontSize: 25, //未选中BottomNavigationBarItem标签 的字体大小
            unselectedIconTheme: IconThemeData(
              //未选中时的BottomNavigationBarItem.icon s中图标的大小，不透明度和颜色
              color: Colors.pink,
              opacity: 0.7,
            ),
            unselectedItemColor:
                Colors.pink, //当前为选中的BottomNavigationBarItem.labels 的颜色
            unselectedLabelStyle: TextStyle(
                color: Colors.green, fontSize: 15), //未选中时的字体样式，设置了并没有生效
            showSelectedLabels: true, //选中的时候的字体样式，设置了并没有生效
          ),
        ));
  }
}



```
