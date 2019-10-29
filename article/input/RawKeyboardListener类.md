# RawKeyboardListener

## 介绍
RawKeyboardListener 可以用来监听手机物理按钮，相当于原生的onKeyDown和onKeyUp函数

## 构造函数
```
const RawKeyboardListener({
    Key key,
    @required this.focusNode,//焦点结点
    @required this.onKey,//按键接收处理事件
    @required this.child,//接收焦点的子控件
  })
```

## 常用属性

### focusNode
focusNode是焦点节点，用于获取焦点，可以主动获取和被动获取
```
//主动获取焦点
FocusScope.of(context).requestFocus(focusNode0);
//自动获取焦点
FocusScope.of(context).autofocus(focusNode0);
```

### onKey
onkey是最关键的属性，用来回调物理按键的点击事件，所有按键事件的相关处理全部要在这个函数下处理。

## 使用示例

```
RawKeyboardListener(
      focusNode: focusNode0,
      child: Text("123456"),
      onKey: (RawKeyEvent event) {
        if (event is RawKeyDownEvent && event.data is RawKeyEventDataAndroid) {
          RawKeyDownEvent rawKeyDownEvent = event;
          RawKeyEventDataAndroid rawKeyEventDataAndroid = rawKeyDownEvent.data;
          print("keyCode: ${rawKeyEventDataAndroid.keyCode}");
          switch (rawKeyEventDataAndroid.keyCode) {
            case 19: //KEY_19
              // code
              break;
            case 20: //KEY_21
              break;
            default:
              break;
          }
        }
      },
    )
```