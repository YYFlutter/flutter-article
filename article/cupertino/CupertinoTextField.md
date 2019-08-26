# CupertinoTextField

``CupertinoTextField`` 仿生了 iOS 原生系统中的 ``UITextField`` 组件，该组件用于创建输入框。

值得注意的是，**Flutter 几乎把整个 iOS 键盘输入特性搬了过来，包括长按空格键移动光标这一牛逼特性**。你可以使用此 widget 实现几乎仿真 iOS 的交互体验，最后不要忘记释放 ``TextEditingController``。

> 前往 [UITextField](https://developer.apple.com/documentation/uikit/uitextfield) 了解更多关于 iOS 原生 ``UITextField`` 的详细内容。

![](./flutter_img/Screen Shot 2019-08-01 at 21.51.30.png)

需要使用此特性，您需要在工程文件的头部引入 ``package:flutter/cupertino.dart``。

## Constructors & Properties

``CupertinoSwitch`` 构造函数的实现如下。

```
const CupertinoTextField({
Key key,
TextEditingController controller,
FocusNode focusNode,
BoxDecoration decoration: _kDefaultRoundedBorderDecoration,
EdgeInsetsGeometry padding: const EdgeInsets.all(6.0),
String placeholder,
TextStyle placeholderStyle: const TextStyle(fontWeight: FontWeight.w300, color: _kInactiveTextColor),
Widget prefix,
OverlayVisibilityMode prefixMode: OverlayVisibilityMode.always,
Widget suffix,
OverlayVisibilityMode suffixMode: OverlayVisibilityMode.always,
OverlayVisibilityMode clearButtonMode: OverlayVisibilityMode.never,
TextInputType keyboardType,
TextInputAction textInputAction,
TextCapitalization textCapitalization: TextCapitalization.none,
TextStyle style,
StrutStyle strutStyle,
TextAlign textAlign: TextAlign.start,
bool readOnly: false,
bool showCursor,
bool autofocus: false,
bool obscureText: false,
bool autocorrect: true,
int maxLines: 1,
int minLines,
bool expands: false,
int maxLength,
bool maxLengthEnforced: true,
ValueChanged<String> onChanged,
VoidCallback onEditingComplete,
ValueChanged<String> onSubmitted,
List<TextInputFormatter> inputFormatters,
bool enabled,
double cursorWidth: 2.0,
Radius cursorRadius: const Radius.circular(2.0),
Color cursorColor,
Brightness keyboardAppearance,
EdgeInsets scrollPadding: const EdgeInsets.all(20.0),
DragStartBehavior dragStartBehavior: DragStartBehavior.start,
bool enableInteractiveSelection,
ScrollController scrollController,
ScrollPhysics scrollPhysics
})
```

- ``autocorrect`` 是否启用语法自动修正。

- ``autofocus`` 当文本框获得焦点时，是否自动弹出键盘。否则只有用户点击时才会弹出。

- ``clearButtonMode`` 在空间尾部增加一个清除按钮。

- ``controller`` 文本的输入控制器。如果你有需要监听用户的输入行为，则需要自定义。

- ``cursorColor`` 光标的颜色。

- ``cursorRadius`` 光标的圆角半径。

- ``cursorWidth`` 光标的宽度。

- ``decoration`` 控件文本输入后框的框装饰。默认情况下有一个圆角矩形灰色边框，可以为空。

- ``enabled`` 如果为 false 则为禁用此输入框，并且背景为灰色。此时 touch 事件都将不会响应。

- ``enableInteractiveSelection`` 默认为 true，用户可以长按文字进行复制粘贴等操作。反之为 false。

- ``inputFormatters`` 提供你的格式验证和重写算法。widget 会依照你所提供的顺序执行。

- ``keyboardAppearance`` 键盘的外观，仅 iOS 可用。

- ``keyboardType`` 键盘的类型。

- ``maxLength`` 最大允许的字符数。

- ``maxLengthEnforced`` 如果为 true，则强行阻止其超过最大数限制，否则仅仅是警告。默认为 false。

- ``maxLines`` 为最大允许的行数，``minLines`` 则为最小允许的行数。

- ``obscureText`` 是否使用隐藏文本。例如，输入密码时。

- ``onChanged`` 当文本发生变化时回调。

- ``onEditingComplete`` 当用户按下键盘的「完成（Done）」时回调。

- ``placeholder`` 当文本框无内容时的浅色占位符。

- ``placeholderStyle`` 浅色占位符的样式。

- ``prefix`` 在文本框头部显示的前缀小控件，``prefixMode`` 设置前缀小控件的显示方式。

- ``readOnly`` 此编辑框是否仅仅是只读的模式。

- ``showCursor`` 光标是否显示。

- ``suffix`` 在文本框尾部显示的后缀小控件，``suffixMode`` 设置后缀小控件的显示方式。

- ``textAlign`` 在水平的方向上，文本要以何种方式对齐。

- ``textCapitalization`` 指定键盘的大小写显示模式。

- ``textInputAction`` 键盘右下角的「Enter」按钮应当显示什么文字。例如，「完成」，「加入」等样式。

## Demo

此 demo 完整实例如下。

```
class MyPrefilledText extends StatefulWidget {
  @override
  _MyPrefilledTextState createState() => _MyPrefilledTextState();
}

class _MyPrefilledTextState extends State<MyPrefilledText> {
  TextEditingController _textController;

  @override
  void initState() {
    super.initState();
    _textController = TextEditingController(text: 'input here!');
  }

  @override
  Widget build(BuildContext context) {
    return CupertinoTextField(
      clearButtonMode: OverlayVisibilityMode.always,
      keyboardAppearance: Brightness.dark,
      controller: _textController,
        cursorRadius: Radius.circular(40),
      cursorWidth: 8,
      cursorColor: Color(0xffff0000),
      autocorrect: true,
    );
  }
}
```

