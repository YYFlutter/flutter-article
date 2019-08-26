# CupertinoDatePicker

``CupertinoDatePicker`` 仿生了 iOS 原生系统中的 ``Pickers`` 组件，该组件用于创建多个字段的列表选择框。在 ``CupertinoDatePicker`` 中，有三种与日期相关的选择样式，分别是：

- date

- time

- date & time

如下图所示。

> 前往 [Pickers](https://developer.apple.com/design/human-interface-guidelines/ios/controls/pickers/) 了解更多关于 iOS 原生 ``Pickers`` 的详细内容。

![](./flutter_img/Screen Shot 2019-07-31 at 11.42.15.png)

> date 类型的 picker

![](./flutter_img/Screen Shot 2019-07-31 at 11.42.18.png)

> time 类型的 picker

![](./flutter_img/Screen Shot 2019-07-31 at 11.42.21.png)

> date & time 类型的 picker

需要使用此特性，您需要在工程文件的头部引入 ``package:flutter/cupertino.dart``。

## Constructors & Properties

``CupertinoDatePicker`` 构造函数的实现如下。

```
CupertinoDatePicker({
CupertinoDatePickerMode mode: CupertinoDatePickerMode.dateAndTime,
@required ValueChanged<DateTime> onDateTimeChanged,
DateTime initialDateTime,
DateTime minimumDate,
DateTime maximumDate,
int minimumYear: 1,
int maximumYear,
int minuteInterval: 1,
bool use24hFormat: false
})
```

- ``mode`` 表示需要使用的选择样式。如 demo 所示，分别使用了 ``CupertinoDatePickerMode`` 枚举中的 ``dateAndTime`` / ``date`` / ``time``。

- ``onDateTimeChanged`` 监听选择的变化。注意，在选择滚动的同时，此接口实时回调。

- ``initialDateTime`` 用于初始化显示时间。

- ``minimumDate`` 和 ``maximumDate`` 用于限定选择日期的下限和上限，此参数当 ``mode`` 为 ``dateAndTime`` 时有效。

- ``minimumYear `` 和 ``maximumYear `` 用于限定选择日期的下限和上限，此参数当 ``mode`` 为 ``date`` 时有效。

- ``minuteInterval`` 在分钟的滚轮中，分钟数的间隔。

- ``use24hFormat`` 用于表示时间是否以 24 小时显示。

## Demo

此 demo 完整实例如下。

```
DateTime dateTime = DateTime.now();

void _onButtonClick(CupertinoDatePickerMode mode) {
  setState(() {
    showCupertinoModalPopup<void>(
      context: context,
      builder: (BuildContext context) {
        return _buildBottomPicker(
          CupertinoDatePicker(
            mode: mode,
            initialDateTime: dateTime,
            onDateTimeChanged: (DateTime newDateTime) {
              setState(() => dateTime = newDateTime);
            },
          ),
        );
      },
    );
  });
}

static const double _kPickerSheetHeight = 216.0;

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

