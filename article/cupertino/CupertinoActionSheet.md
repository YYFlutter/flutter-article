# CupertinoActionSheet & CupertinoActionSheetAction

``CupertinoActionSheet`` 仿生了 iOS 原生系统中的 ``Action Sheets`` 组件，该组件用于创建浮层 List 选择框。如下图所示。

> 前往 [Action Sheets](https://developer.apple.com/design/human-interface-guidelines/ios/views/action-sheets/) 了解更多关于 iOS 原生 ``Action Sheets`` 的详细内容。

![](./flutter_img/Screen Shot 2019-07-30 at 11.56.48.png)

需要使用此特性，您需要在工程文件的头部引入 ``package:flutter/cupertino.dart``。

## CupertinoActionSheet

``CupertinoActionSheet`` 构造函数的实现如下。

```
const CupertinoActionSheet({
Key key,
Widget title,
Widget message,
List<Widget> actions,
ScrollController messageScrollController,
ScrollController actionScrollController,
Widget cancelButton
})
```

- ``title`` 为顶部标题。此 Demo 中，``title`` 为 *Favorite Dessert*。

- ``message`` 为标题下的信息。此 Demo 中，``message`` 为 *Please select the best dessert from the options below*。

- ``actions`` 是一个 Widget List。该值承载列表中的选项按钮。此 List 的值通常使用 ``CupertinoActionSheetAction`` 为值。详见下方解释。

- 当顶部标题或列表选项过多时，``messageScrollController`` 及 ``actionScrollController`` 用于滚动控制。这两个值通常不需要设置。

- ``cancelButton`` 是一个 Widget，用于 cancel 事件按钮。详见 ``CupertinoActionSheetAction``。

## CupertinoActionSheetAction

``CupertinoActionSheetAction`` 构造函数的实现如下。

```
const CupertinoActionSheetAction({
@required VoidCallback onPressed,
bool isDefaultAction: false,
bool isDestructiveAction: false,
@required Widget child
})
```

在此 demo 中，四个按钮的实体都是通过 ``CupertinoActionSheetAction`` 实现的。

- ``onPressed`` 用于监听点击事件。

- ``isDefaultAction`` 标记是否使用粗体，本 demo 的 *Cannolis* 按钮体现了该特性。

- ``isDestructiveAction`` 标记是否显示警告样式，即红色字体。本 demo 的 *Trifle* 按钮体现了该特性。

## Demo

此 demo 完整实例如下。

```
void _onButtonClick() {
  setState(() {
    showDemoActionSheet(
      context: context,
      child: CupertinoActionSheet(
        title: const Text('Favorite Dessert'),
        message: const Text(
            'Please select the best dessert from the options below.'),
        actions: <Widget>[
          CupertinoActionSheetAction(
            child: const Text('Profiteroles'),
            onPressed: () {
              Navigator.pop(context, 'Profiteroles');
            },
          ),
          CupertinoActionSheetAction(
            isDefaultAction: true,
            child: const Text('Cannolis'),
            onPressed: () {
              Navigator.pop(context, 'Cannolis');
            },
          ),
          CupertinoActionSheetAction(
            isDestructiveAction: true,
            child: const Text('Trifle'),
            onPressed: () {
              Navigator.pop(context, 'Trifle');
            },
          ),
        ],
        cancelButton: CupertinoActionSheetAction(
          child: const Text('Cancel'),
          isDefaultAction: true,
          onPressed: () {
            Navigator.pop(context, 'Cancel');
          },
        ),
      ),
    );
  });
}

void showDemoActionSheet({BuildContext context, Widget child}) {
  showCupertinoModalPopup<String>(
    context: context,
    builder: (BuildContext context) => child,
  ).then((String value) {
    if (value != null) {
      setState(() {});
    }
  });
}
```

