# CupertinoButton

``CupertinoButton`` 仿生了 iOS 原生系统中的 ``Buttons`` 组件，该组件用于创建按钮。如下图所示。

> 前往 [Buttons](https://developer.apple.com/design/human-interface-guidelines/ios/controls/buttons/) 了解更多关于 iOS 原生 ``Buttons`` 的详细内容。

![](./flutter_img/Screen Shot 2019-07-30 at 15.48.21.png)

需要使用此特性，您需要在工程文件的头部引入 ``package:flutter/cupertino.dart``。

## Normal Style

``CupertinoButton`` 有两种按钮样式可用。第一种是没有背景描边的 Button，即 demo 截图中上面两个按钮样式。在内部实现中，是通过控制内部成员变量 ``_filled`` 来控制的，详情请阅读源码。Normal Style 的构造函数的实现如下。

```
const CupertinoButton({
Key key,
@required Widget child,
EdgeInsetsGeometry padding,
Color color,
Color disabledColor,
double minSize: 44.0,
double pressedOpacity: 0.1,
BorderRadius borderRadius: const BorderRadius.all(Radius.circular(8.0)),
@required VoidCallback onPressed
})
```

- ``child`` 用于承载需要在按钮中放置的内容。

- ``padding`` 指定了内容与边界的距离。

- ``color`` 及 ``disabledColor `` 分别指定了按钮启用和禁用时的背景色。

- ``minSize`` 按钮的最小 size。

- ``pressedOpacity `` 按下时的透明度。

- ``borderRadius `` 按钮的圆角数据。

## Filled Style

这是 ``CupertinoButton`` 的第二种样式。这是我们跟平时更为常见的样式，含有背景描边的 Button。构造函数的实现如下。

```
const CupertinoButton.filled({
Key key,
@required Widget child,
EdgeInsetsGeometry padding,
Color disabledColor,
double minSize: 44.0,
double pressedOpacity: 0.1,
BorderRadius borderRadius: const BorderRadius.all(Radius.circular(8.0)),
@required VoidCallback onPressed
})
```

他通过 filled 方法来实现另一个构造。所有属性的含义与 Normal Style 是一致的。

## Demo

此 demo 完整实例如下。

```
@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: Text(widget.title),
    ),
    body: Center(
      child: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: <Widget>[
          const Padding(padding: EdgeInsets.all(12.0)),
          Align(
            alignment: const Alignment(0.0, -0.2),
            child: Row(
              mainAxisSize: MainAxisSize.min,
              children: <Widget>[
                CupertinoButton(
                  child: const Text('Cupertino Button'),
                  onPressed: () {
                    setState(() {});
                  },
                ),
                const CupertinoButton(
                  child: Text('Disabled'),
                  onPressed: null,
                ),
              ],
            ),
          ),
          const Padding(padding: EdgeInsets.all(12.0)),
          CupertinoButton.filled(
            child: const Text('With Background'),
            onPressed: () {
              setState(() {});
            },
          ),
          const Padding(padding: EdgeInsets.all(12.0)),
          const CupertinoButton.filled(
            minSize: 300,
            child: Text('Disabled'),
            onPressed: null,
          ),
        ],
      ),
    ),
  );
}
```

