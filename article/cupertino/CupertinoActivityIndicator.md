# CupertinoActivityIndicator

``CupertinoActivityIndicator`` 仿生了 iOS 原生系统中的 ``Activity Indicators`` 组件，该组件用于创建 Loading。如下图所示。

> 前往 [Activity Indicators](https://developer.apple.com/design/human-interface-guidelines/ios/controls/progress-indicators/#activity-indicators) 了解更多关于 iOS 原生 ``Activity Indicators`` 的详细内容。

![](./flutter_img/Screen Shot 2019-07-30 at 13.21.47.png)

需要使用此特性，您需要在工程文件的头部引入 ``package:flutter/cupertino.dart``。

## Constructors & Properties

``CupertinoActionSheet`` 构造函数的实现如下。

```
const CupertinoActivityIndicator({
Key key,
bool animating: true,
double radius: _kDefaultIndicatorRadius
})
```

- ``animating`` 用于指示 Loading 图标是否需要转动。

- ``radius`` 指定了 Loading 的半径。

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
          CupertinoActivityIndicator(),
          CupertinoActivityIndicator(radius: 30, animating: false,),
          CupertinoActivityIndicator(radius: 100,),
        ],
      ),
    ),
  );
}
```

