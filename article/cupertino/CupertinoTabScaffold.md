# CupertinoTabScaffold & CupertinoTabBar & CupertinoTabView

``CupertinoTabScaffold`` 仿生了 iOS 原生系统中的 ``Tab Bars`` 组件，该组件用于创建屏幕底部的 tab 交互，及选中 tab 的布局切换。它分为两部分：底部的 tab 栏，以及剩余的空白区域。

``CupertinoTabBar`` 用于填充 ``CupertinoTabScaffold`` 中的 tab 栏，用户点击 tab 中不同的 item，以切换 ``CupertinoTabScaffold`` 中的空白区域。

``CupertinoTabView`` 则用于填充 ``CupertinoTabScaffold`` 中的空白区域，``CupertinoTabView`` 能通过参数指定需要加载的 widget，典型的用法是，当 ``CupertinoTabBar`` 的 item 被点击时，通知 ``CupertinoTabView`` 切换主界面。

需要注意的是，``CupertinoTabBar`` item 数量应当与 ``CupertinoTabView`` 所能切换的数量相等。当 ``CupertinoTabView`` 的界面被移出可视范围时，动画会被禁用。此外，虽然 ``CupertinoTabScaffold`` 底部 tab 支持制表符，但不建议这样操作。因为这违反了 iOS 交互指南。

> 前往 [iOS 人机交互指南](https://developer.apple.com/design/human-interface-guidelines/ios/bars/tab-bars/) 了解更多关于 iOS 原生 ``Tab Bars`` 的详细内容。

![](./flutter_img/Screen Shot 2019-08-01 at 17.04.23.png)

需要使用此特性，您需要在工程文件的头部引入 ``package:flutter/cupertino.dart``。

## CupertinoTabScaffold

``CupertinoTabScaffold`` 构造函数的实现如下。

```
CupertinoTabScaffold({
Key key,
@required CupertinoTabBar tabBar,
@required IndexedWidgetBuilder tabBuilder,
CupertinoTabController controller,
Color backgroundColor,
bool resizeToAvoidBottomInset: true
})
```

- ``tabBar`` 用于放置 ``CupertinoTabBar``。

- ``tabBuilder`` 用于放置 ``CupertinoTabView``。

- ``controller`` 自定义的控制器，如果您需要对切换行为自定义需求。默认情况下内置的控制器会自行管理。

- ``backgroundColor`` 背景色设置。

- ``resizeToAvoidBottomInset`` 当底部有其他内容入侵时，是否需要对界面进行重新计算。典型的情况是，底部键盘弹起时。

## CupertinoTabBar

``CupertinoTabBar`` 构造函数的实现如下。

```
const CupertinoTabBar({
Key key,
@required List<BottomNavigationBarItem> items,
ValueChanged<int> onTap,
int currentIndex: 0,
Color backgroundColor,
Color activeColor,
Color inactiveColor: CupertinoColors.inactiveGray,
double iconSize: 30.0,
Border border: const Border(top: BorderSide(color: _kDefaultTabBarBorderColor, width: 0.0, style: BorderStyle.solid))
})
```

- ``items`` 这是一个列表，用于指定每个 tab 的文字和 icon。

- ``onTap`` 当 tab 发生切换时回调。

- ``currentIndex`` 设置当前选中的 index，注意别的超过 ``items`` 的长度。

- ``backgroundColor`` tab 的背景色。

- ``activeColor`` item 被选中时元素的颜色。

- ``inactiveColor`` item 未被选中时元素的颜色。

- ``iconSize`` item 中 icon 的大小，即 ``BottomNavigationBarItem`` 中 ``activeIcon`` 的大小。

- ``border`` tab 描边的颜色。默认是 1px 的描边，一般情况不需要设置。

## CupertinoTabView

``CupertinoTabView`` 构造函数的实现如下。

```
const CupertinoTabView({
Key key,
WidgetBuilder builder,
GlobalKey<NavigatorState> navigatorKey,
String defaultTitle,
Map<String, WidgetBuilder> routes,
RouteFactory onGenerateRoute,
RouteFactory onUnknownRoute,
List<NavigatorObserver> navigatorObservers: const []
})
```

- ``builder`` 页面的构造器，通过所给予的参数决定需要构造什么样的 widget。典型的做法，即通过 ``CupertinoTabBar`` 中选中 item 的 index 做不同切换。

- ``defaultTitle`` 在路由中的默认名字。

- ``currentIndex`` 设置当前选中的 index，注意别的超过 ``items`` 的长度。

- ``routes`` 用于承载每个界面的路由信息。

- ``onGenerateRoute`` 为路由行为回调，当此行为发生异常时，则通过 ``onUnknownRoute`` 回调。

- ``navigatorObservers`` 导航器的观察者列表。

## Demo

此 demo 完整实例如下。

```
class _MyPageState extends State {
  @override
  Widget build(BuildContext context) {
    //最外层导航选项卡
    return CupertinoTabScaffold(
      //底部选项卡
      tabBar: CupertinoTabBar(
        activeColor: Color(0xffff0000),
        backgroundColor: CupertinoColors.lightBackgroundGray, //选项卡背景色
        items: [
          //选项卡项 包含图标及文字
          BottomNavigationBarItem(
            icon: Icon(CupertinoIcons.home),
            title: Text('主页'),
          ),
          BottomNavigationBarItem(
            icon: Icon(CupertinoIcons.conversation_bubble),
            title: Text('聊天'),
          ),
        ],
      ),
      tabBuilder: (context, index) {
        //选项卡绑定的视图
        return CupertinoTabView(
          builder: (context) {
            switch (index) {
              case 0:
                return HomePage();
                break;
              case 1:
                return ChatPage();
                break;
              default:
                return Container();
            }
          },
        );
      },
    );
  }
}

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CupertinoPageScaffold(
      backgroundColor: Color(0x6655500a),
      navigationBar: CupertinoNavigationBar(
        middle: Text("主页"),
      ),
      child: Center(
        child: Text(
          'This is 主页 layout',
          style: Theme.of(context).textTheme.button,
        ),
      ),
    );
  }
}

class ChatPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CupertinoPageScaffold(
      backgroundColor: Color(0xffffaaaa),
      navigationBar: CupertinoNavigationBar(
        middle: Text("聊天面板"),
        trailing: Icon(CupertinoIcons.add),
        leading: Icon(CupertinoIcons.back),
      ),
      child: Center(
        child: Text(
          'This is 聊天面板 layout',
          style: Theme.of(context).textTheme.button,
        ),
      ),
    );
  }
}
```

