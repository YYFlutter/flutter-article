# CupertinoPicker

``CupertinoPicker`` 仿生了 iOS 原生系统中的 ``Pickers`` 组件，该组件用于创建滚动的列表选择框。如下图所示。

> 前往 [Pickers](https://developer.apple.com/design/human-interface-guidelines/ios/controls/pickers/) 了解更多关于 iOS 原生 ``Pickers`` 的详细内容。

![](./flutter_img/Screen Shot 2019-07-31 at 22.30.19.png)

需要使用此特性，您需要在工程文件的头部引入 ``package:flutter/cupertino.dart``。

## Constructors & Properties

``CupertinoPicker`` 构造函数的实现如下。

```
CupertinoPicker({
Key key,
double diameterRatio: _kDefaultDiameterRatio,
Color backgroundColor: _kDefaultBackground,
double offAxisFraction: 0.0,
bool useMagnifier: false,
double magnification: 1.0,
FixedExtentScrollController scrollController,
double squeeze: _kSqueeze,
@required double itemExtent,
@required ValueChanged<int> onSelectedItemChanged,
@required List<Widget> children,
bool looping: false
})
```

- ``diameterRatio`` 表示该滚动柱子的大小。仔细观察，``CupertinoPicker`` 是一个立体的圆柱。

- ``backgroundColor`` 背景色。

- ``offAxisFraction`` 表示该滚动柱子左右偏移的角度。

- ``scrollController`` 滚动控制器。一般不需要进行设置。

- ``squeeze`` 每个 item 之间的紧凑度。

- ``itemExtent`` item 的高度。

- ``onSelectedItemChanged`` item 选择的回调。

- ``children`` 数据集。

- ``looping`` 列表是否持续循环，永无尽头。

## Demo

此 demo 完整实例如下。

```
showCupertinoModalPopup<void>(
context: context,
builder: (BuildContext context) {
return _buildColorPicker(context);
},
);

static const double _kPickerSheetHeight = 600.0;
static const double _kPickerItemHeight = 32.0;
static const List<String> coolColorNames = <String>[
  'Sarcoline',
  'Coquelicot',
  'Smaragdine',
  'Mikado',
  'Glaucous',
  'Wenge',
  'Fulvous',
  'Xanadu',
  'Falu',
  'Eburnean',
  'Amaranth',
  'Australien',
  'Banan',
  'Falu',
  'Gingerline',
  'Incarnadine',
  'Labrador',
  'Nattier',
  'Pervenche',
  'Sinoper',
  'Verditer',
  'Watchet',
  'Zaffre',
];

Widget _buildColorPicker(BuildContext context) {
  return _buildBottomPicker(
    CupertinoPicker(
      looping: true,
      itemExtent: _kPickerItemHeight,
      backgroundColor: CupertinoColors.white,
      onSelectedItemChanged: (int index) {
        setState(() => _selectedColorIndex = index);
      },
      children: List<Widget>.generate(coolColorNames.length, (int index) {
        return Center(
          child: Text(coolColorNames[index]),
        );
      }),
    ),
  );
}

Widget _buildBottomPicker(Widget picker) {
  return Container(
    height: _kPickerSheetHeight,
    padding: const EdgeInsets.only(top: 6.0),
    color: CupertinoColors.white,
    child: DefaultTextStyle(
      style: const TextStyle(
        color: CupertinoColors.black,
        fontSize: 22.0,
      ),
      child: GestureDetector(
        // Blocks taps from propagating to the modal sheet and popping.
        onTap: () {},
        child: SafeArea(
          top: false,
          child: picker,
        ),
      ),
    ),
  );
}
```

