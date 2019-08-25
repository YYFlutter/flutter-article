## 介绍
MediaQueryData 它是MediaQuery的主要信息载体，是用于存储MediaQuery的各项数据的实体类。如果传入的context没有MediaQuery信息，则调用MediaQuery.of方法将会抛出异常。除非nullOk参数设置为true，在这种情况下它返回null。

## 构造函数

```
 MediaQueryData({Size size: Size.zero,
 double devicePixelRatio: 1.0, 
 double textScaleFactor: 1.0,
 Brightness platformBrightness: Brightness.light,
 EdgeInsets padding: EdgeInsets.zero, 
 EdgeInsets viewInsets: EdgeInsets.zero,
 EdgeInsets viewPadding: EdgeInsets.zero,
 bool alwaysUse24HourFormat: false, 
 bool accessibleNavigation: false, 
 bool invertColors: false, 
 bool disableAnimations: false,
 bool boldText: false }) 
 
 MediaQueryData.fromWindow(Window window) //基于给定窗口为MediaQuery创建数据.
```
## 属性

 - accessibleNavigation → bool **用户是否使用TalkBack或VoiceOver等辅助功能服务与应用程序进行交互。**
 - alwaysUse24HourFormat → bool **格式化时间时是否使用24小时格式。**
 - boldText → bool **是否使用了粗体字体绘制文本。**
 - devicePixelRatio → double  **单位逻辑像素的设备像素数量，即设备像素比。这个数字可能不是2的幂，实际上它甚至也可能不是整数。例如，Nexus 6的设备像素比为3.5。**
 - disableAnimations → bool  **平台是否要求尽可能禁用或减少使用动画。**
 - hashCode → int **此对象的哈希码**
 - invertColors → bool **设备是否反转平台的颜色**
 - orientation → Orientation  **屏幕方向（横向/纵向）**
 - padding → EdgeInsets **显示器的部分被系统UI部分遮挡，通常由硬件显示“凹槽”或系统状态栏**
 - platformBrightness → Brightness **当前的亮度模式**
 - size → Size **设备尺寸信息，如屏幕的大小，单位 pixels**
 - textScaleFactor → double **每个逻辑像素的字体像素数**
 - viewInsets → EdgeInsets **显示器的各个部分完全被系统UI遮挡，通常是设备的键盘**
 - viewPadding → EdgeInsets  **显示器的部分被系统UI部分遮挡，通常由硬件显示“凹槽”或系统状态栏**
 

![Insets and Padding](https://flutter.github.io/assets-for-api-docs/assets/widgets/media_query.png)

## 方法

#### copyWith

copyWith（{ Size size， double devicePixelRatio， double textScaleFactor， Brightness platformBrightness， EdgeInsets padding， EdgeInsets viewPadding， EdgeInsets viewInsets， bool alwaysUse24HourFormat， bool disableAnimations， bool invertColors， bool accessibleNavigation， bool boldText }） → MediaQueryData
 **拷贝此 MediaQueryData对象，创建一个副本，但将新字段替换为传入的给定字段。**

#### removePadding
removePadding（{ bool removeLeft：false， bool removeTop：false， bool removeRight：false， bool removeBottom：false }） → MediaQueryData
**创建此 MediaQueryData 的副本，但将给定的填充替换为零。**

#### removeViewInsets
removeViewInsets（{ bool removeLeft：false， bool removeTop：false， bool removeRight：false， bool removeBottom：false }） → MediaQueryData
**创建此 MediaQueryData 的副本，但将给定的viewInsets 替换为零。**

#### ~~removeViewPadding~~(新版本源码已找不到该方法)

