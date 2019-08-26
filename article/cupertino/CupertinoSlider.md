# CupertinoSlider

``CupertinoSlider`` 仿生了 iOS 原生系统中的 ``Sliders`` 组件，该组件用于创建滑动条。如下图所示。

> 前往 [Sliders](https://developer.apple.com/design/human-interface-guidelines/ios/controls/sliders/) 了解更多关于 iOS 原生 ``Sliders`` 的详细内容。

![](./flutter_img/Screen Shot 2019-07-31 at 23.03.36.png)

需要使用此特性，您需要在工程文件的头部引入 ``package:flutter/cupertino.dart``。

## Constructors & Properties

``CupertinoSlider`` 构造函数的实现如下。

```
const CupertinoSlider({
Key key,
@required double value,
@required ValueChanged<double> onChanged,
ValueChanged<double> onChangeStart,
ValueChanged<double> onChangeEnd,
double min: 0.0,
double max: 1.0,
int divisions,
Color activeColor
})
```

- ``value`` 为初始化值。

- ``onChanged`` 当值改变时持续回调此接口。

- ``onChangeStart`` 在一次滚动周期中，第一次改变的值。

- ``onChangeEnd`` 在一次滚动周期中，最后一次改变的值。

- ``min`` 允许的最小值。

- ``max`` 允许的最大值。

- ``divisions`` 值之间的间隔。demo 效果中第二个效果。

- ``activeColor`` 滑动条的颜色。demo 效果中第二个效果。

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
        mainAxisAlignment: MainAxisAlignment.start,
        children: <Widget>[
          const Padding(padding: EdgeInsets.all(12.0)),
          Text(
            'CupertinoSlider',
            style: TextStyle(fontWeight: FontWeight.bold, fontSize: 30),
          ),
          const Padding(padding: EdgeInsets.all(12.0)),
          Column(
            mainAxisSize: MainAxisSize.min,
            children: <Widget>[
              CupertinoSlider(
                value: _value,
                min: 0.0,
                max: 100.0,
                onChanged: (double value) {
                  setState(() {
                    _value = value;
                  });
                },
              ),
              Text('普通的 Continuous: ${_value.toStringAsFixed(1)}'),
            ],
          ),
          Column(
            mainAxisSize: MainAxisSize.min,
            children: <Widget>[
              CupertinoSlider(
                activeColor: Color(0xffff0000),
                value: _discreteValue,
                min: 0.0,
                max: 100.0,
                divisions: 5,
                onChanged: (double value) {
                  setState(() {
                    _discreteValue = value;
                  });
                },
              ),
              Text('带间隔的 Discrete，只能是 20 的倍数: $_discreteValue'),
            ],
          ),
        ],
      ),
    ),
  );
}
```

