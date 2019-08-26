# CupertinoSwitch

``CupertinoSwitch`` 仿生了 iOS 原生系统中的 ``Switches`` 组件，该组件用于创建开关按钮。

开关本身不维护任何状态，外部唯一能感知的，只要开关状态被切换时的回调监听。因此，当开关状态变化时，你应当实时修改你的值。同样，当你的值发生变化时，应当及时更新开关状态。

> 前往 [Switches](https://developer.apple.com/design/human-interface-guidelines/ios/controls/switches/) 了解更多关于 iOS 原生 ``Switches`` 的详细内容。

![](./flutter_img/Screen Shot 2019-08-01 at 15.27.03.png)

需要使用此特性，您需要在工程文件的头部引入 ``package:flutter/cupertino.dart``。

## Constructors & Properties

``CupertinoSwitch`` 构造函数的实现如下。

```
const CupertinoSwitch({
Key key,
@required bool value,
@required ValueChanged<bool> onChanged,
Color activeColor,
DragStartBehavior dragStartBehavior: DragStartBehavior.start
})
```

- ``value`` 用于指定初始化状态为 on 或 off。

- ``onChanged`` 用于监听按钮的变化。**如果此值为 null，按钮则会自动变为 disable**。

- ``activeColor`` 按钮的颜色。

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
            'CupertinoSwitch',
            style: TextStyle(fontWeight: FontWeight.bold, fontSize: 30),
          ),
          const Padding(padding: EdgeInsets.all(12.0)),
          CupertinoSwitch(
            dragStartBehavior: DragStartBehavior.down,
            value: _switchValue,
            activeColor: Color(0xffff0000),
            onChanged: (bool value) {
              setState(() {
                _switchValue = value;
              });
            },
          ),
          Text("Enabled - ${_switchValue ? "On" : "Off"}"),
          CupertinoSwitch(
            value: true,
            activeColor: Color(0xffff0000),
            onChanged: null,
          ),
          Text('Disabled - On'),
          CupertinoSwitch(
            value: true,
            onChanged: null,
          ),
          Text('Disabled - On'),
          CupertinoSwitch(
            value: false,
            onChanged: null,
          ),
          Text('Disabled - Off'),
        ],
      ),
    ),
  );
}
```

