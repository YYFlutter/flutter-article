# CupertinoPageScaffold & CupertinoNavigationBar

``CupertinoPageScaffold`` 是一个层级非常低的容器。这意味着大多数布局都以它作为根基。作为底层通用容器，看似强大，其实功能非常简单，只提供了几个接口。这使得其作用非常稳固，且不会被滥用。

``CupertinoNavigationBar`` 仿生了 iOS 原生系统中的 ``UINavigationBar`` 组件，该组件用于创建页面的顶部导航栏。通常 ``CupertinoNavigationBar`` 放置在 ``CupertinoPageScaffold`` 的顶部。导航栏由多个小部件组成，**在正确的设计指导中，您应该始终将其放置于顶部**，并且不得作出透明处理——因为他会自动对背景进行高斯模糊。

> 前往 [UINavigationBar](https://developer.apple.com/documentation/uikit/uinavigationbar) 了解更多关于 iOS 原生 ``UINavigationBar`` 的详细内容。

![](./flutter_img/Screen Shot 2019-07-31 at 17.31.15.png)

需要使用此特性，您需要在工程文件的头部引入 ``package:flutter/cupertino.dart``。

## CupertinoPageScaffold

``CupertinoPageScaffold`` 构造函数的实现如下。

```
const CupertinoPageScaffold({
Key key,
ObstructingPreferredSizeWidget navigationBar,
Color backgroundColor,
bool resizeToAvoidBottomInset: true,
@required Widget child
})
```

``CupertinoPageScaffold`` 布局分为两部分，一部分是顶部的导航栏，另一部分是剩余的主界面，即 ``child``。

- ``navigationBar`` 用于放置导航栏，详细定义见 ``CupertinoNavigationBar`` 部分。

- ``backgroundColor`` 设置主布局的背景色。

- ``resizeToAvoidBottomInset `` 当底部被遮挡后，是否重新计算布局大小。例如，当键盘从底部升起。

## CupertinoNavigationBar

``CupertinoNavigationBar`` 构造函数的实现如下。

```
const CupertinoNavigationBar({
Key key,
Widget leading,
bool automaticallyImplyLeading: true,
bool automaticallyImplyMiddle: true,
String previousPageTitle,
Widget middle,
Widget trailing,
Border border: _kDefaultNavBarBorder,
Color backgroundColor,
EdgeInsetsDirectional padding,
Color actionsForegroundColor,
bool transitionBetweenRoutes: true,
Object heroTag: _defaultHeroTag
})
```

- ``leading`` 用于设置左侧组件，``automaticallyImplyLeading`` 则用于设置组件是否可见。

- ``automaticallyImplyMiddle`` 设置中间的组件是否可见。

- ``previousPageTitle`` 当通过路由前往下一级菜单后，「返回」按钮所显示的文字。

- ``middle`` 中间的文字。

- ``border`` 设置导航栏的边框，默认情况下是为 1px 的描边。

- ``backgroundColor`` 设置导航栏背景色。

- ``padding`` 导航栏中的元素距离距离边缘的 padding 值设置。

- ``actionsForegroundColor`` 左侧组件的颜色。

## Demo

此 demo 完整实例如下。

```
class _MyPageState extends State {
  @override
  Widget build(BuildContext context) {
    return ChatPage();
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

