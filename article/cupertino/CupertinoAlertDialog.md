# CupertinoAlertDialog & CupertinoDialogAction

``CupertinoAlertDialog`` 仿生了 iOS 原生系统中的 ``Alerts`` 组件，该组件用于创建浮层的中央弹窗样式。**根据按钮数量的不同，Alerts 会自动呈现不同的横向或纵向列表样式**，如下图所示。

> 前往 [Alerts](https://developer.apple.com/design/human-interface-guidelines/ios/views/alerts/) 了解更多关于 iOS 原生 ``Alerts`` 的详细内容。

![](./flutter_img/Screen Shot 2019-07-30 at 14.58.41.png)

![](./flutter_img/Screen Shot 2019-07-30 at 14.59.07.png)

需要使用此特性，您需要在工程文件的头部引入 ``package:flutter/cupertino.dart``。同时，``CupertinoAlertDialog `` 也用于取代 ``CupertinoDialog``，``CupertinoDialog`` 已被标记为 ``@Deprecated``。

## CupertinoAlertDialog

``CupertinoAlertDialog`` 构造函数的实现如下。

```
const CupertinoAlertDialog({
Key key,
Widget title,
Widget content,
List<Widget> actions: const [],
ScrollController scrollController,
ScrollController actionScrollController
})
```

- ``title`` 为顶部标题。此 Demo 中，``title`` 为 *Allow "Maps" to access your location while you are using the app*。

- ``content`` 为标题下的信息。此 Demo 中，``content`` 为 *Your current location will be displayed on the map and used for directions, nearby search results, and estimated travel times*。

- ``actions`` 是一个 Widget List。该值承载列表中的选项按钮。此 List 的值通常使用 ``CupertinoDialogAction`` 为值。详见下方解释。

- 当顶部标题或列表选项过多时，``scrollController`` 及 ``actionScrollController`` 用于滚动控制。这两个值通常不需要设置。

## CupertinoDialogAction

``CupertinoDialogAction`` 构造函数的实现如下。

```
const CupertinoDialogAction({
VoidCallback onPressed,
bool isDefaultAction: false,
bool isDestructiveAction: false,
TextStyle textStyle,
@required Widget child
})
```

在此 demo 中，所有按钮的实体都是通过 ``CupertinoDialogAction`` 实现的。

- ``onPressed`` 用于监听点击事件。

- ``isDefaultAction`` 标记是否使用粗体，本 demo 的 *Allow Always* 按钮体现了该特性。

- ``isDestructiveAction`` 标记是否显示警告样式，即红色字体。本 demo 的 *Don't Allow* 按钮体现了该特性。

## Demo

此 demo 完整实例如下。

```
void _onButtonClick() {
  showDemoDialog(
    context: context,
    child: const CupertinoDessertDialog(),
  );
}

void showDemoDialog({BuildContext context, Widget child}) {
  showCupertinoDialog<String>(
    context: context,
    builder: (BuildContext context) => child,
  );
}

class CupertinoDessertDialog extends StatelessWidget {
  const CupertinoDessertDialog({Key key})
      : super(key: key);

  @override
  Widget build(BuildContext context) {
    return CupertinoAlertDialog(
      title: const Text(
          'Allow "Maps" to access your location while you are using the app?'),
      content: const Text(
          'Your current location will be displayed on the map and used '
          'for directions, nearby search results, and estimated travel times.'),
      actions: <Widget>[
        CupertinoDialogAction(
          isDefaultAction: true,
          child: const Text('Allow Always'),
          onPressed: () {
            Navigator.pop(context, 'Allow');
          },
        ),
        CupertinoDialogAction(
          child: const Text('Allow Once'),
          onPressed: () {
            Navigator.pop(context, 'Allow');
          },
        ),
        CupertinoDialogAction(
          isDestructiveAction: true,
          child: const Text('Don\'t Allow'),
          onPressed: () {
            Navigator.pop(context, 'Disallow');
          },
        ),
      ],
    );
  }
}

```

