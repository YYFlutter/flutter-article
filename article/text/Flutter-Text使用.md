## Text


### 基本属性
- data:要显示的文字
- locale:用于选择区域特定字形的语言环境
- maxLines:文本要跨越的最大行数。如果文本超过给定的行数，则会根据溢出将其截断。
- overflow: 文字超出处理方式.

```dart
TextOverflow.clip(丢弃溢出的文本),  
TextOverflow.fade(将溢出的文本淡化为透明),  
TextOverflow.ellipsis(超出部分用...替代),  
TextOverflow.visible(在容器外渲染超出部分的文字)  
```

- semanticsLabel:此文本的替代语义标签。如果存在，此窗口小部件的语义将包含此值而不是实际文本。这将覆盖直接应用于TextSpans的任何语义标签。 这对于使用全文值替换缩写或缩写很有用 。（不是很理解,据说有用到TalkBack，VoiceOver上的）

- softWrap:文字过长时是否自动换行.true自动换行,false不自动换行

- strutStyle:支柱样式，它设置线相对于基线的最小高度。 Strut适用于段落中的所有行.

- style:设置文字样式.

```dart
color-文本颜色
backgroundColor-背景颜色
fontSize-字体大小
fontWeight-绘制文本时使用的字体粗细.例如FontWeight.bold
fontStyle-字体样式.normal 正常样式,italic 斜体
letterSpacing-字母之间的间隔（逻辑像素为单位）。可以使用负值来让字母更接近。
wordSpacing-单词之间添加的间隔（逻辑像素为单位）。可以使用负值来使单词更接近。
textBaseline-基线
height-此文本的高度跨度，作为字体大小的倍数
locale-用于选择区域特定字形的区域设置
foreground-文本的前景画笔,不能与color共同设置
background-文本的背景画笔
shadows-阴影效果.如BoxShadow
decoration-文本线性装饰.例如
TextDecoration.none(无),
TextDecoration.underline(下划线),
TextDecoration.overline(上划线),   
TextDecoration.lineThrough(中心划线)  
decorationColor-装饰颜色.
decorationStyle-装饰样式.
TextDecorationStyle.solid(实线),
TextDecorationStyle.double(双线),
TextDecorationStyle.dotted(点线),
TextDecorationStyle.dashed(虚线),
TextDecorationStyle.wavy(波浪线)
```

- textAlign:文字内容对齐方式.

```dart
TextAlign.center-将文本对齐容器的中心
TextAlign.right-文本对齐容器右边缘
TextAlign.left-文本对齐容器左边缘
TextAlign.justify-拉伸以结束的文本行以填充容器的宽度。即使用了decorationStyle才起效
TextAlign.start-与容器开始的边缘对齐.TextDirection.lt  模式左边缘为开始边缘,TextDirection.rtl模式时候右边缘 开始边缘
TextAlign.end-与容器末的边缘对齐.TextDirection.ltr模式右边缘为尾边缘,TextDirection.rtl模式时候左边缘为尾边缘
```

- textDirection:文字方向.

```dart
TextDirection.rtl-文字从右到左显示
TextDirection.ltr-文字从左到右显示
复制代码
textScaleFactor:字体像素缩放因子.例如1.5就会比原来字体大50%
textSpan:textSpan中的文本可以单独设置样式,text中可以嵌入多个textSpan.
textWidthBasis:一行或多行文本占用宽度的方式.

TextWidthBasis.parent-多行文本将占用父级给出的全宽,对于单行文本，将仅使用包含文本所需的最小宽度
TextWidthBasis.longestLine-宽度将使用最长的行宽度
```


### 用法

#### text创建

```dart
//显示效果如图在最后面
//r支持显示转义符号
Text(r'$$dfg', semanticsLabel: 'Double dollars')

//创建富文本,支持对不同文字设置不同的样式
Text.rich(TextSpan(
text:'test',
children: <TextSpan>[
TextSpan(text: "hello",style: TextStyle
(fontSize: 20,color: Color.fromARGB(255, 255, 0, 0)))
]
),
)
```

#### text常用属性

```dart
//显示效果如图在最后面
Container(
color: new Color.fromARGB(100, 255, 0, 0),
child: Text(
'我的Hello,!$clickIndex How are yosdvrsdrggdgas史蒂夫dfsdfgg',
maxLines: 3,
overflow: TextOverflow.ellipsis, //文字超出处理方式
softWrap: true, //文字过长是否自动换行
style: TextStyle(
fontSize: 20,
wordSpacing: 20,
fontFamily: 'Raleway',
foreground: new Paint(),
decoration: TextDecoration.lineThrough,
decorationColor: Colors.green,
decorationStyle: TextDecorationStyle.dotted,
),
textAlign: TextAlign.end, //文字内容对齐方式
textDirection: TextDirection.rtl, //文字优先填充方向
textScaleFactor: 1, //文字缩放因子,原来*textScaleFactor
textWidthBasis: TextWidthBasis.longestLine,
),
),
```

[图1](https://user-gold-cdn.xitu.io/2019/8/7/16c6b5738f62067a?imageView2/0/w/1280/h/960/ignore-error/1)

#### 与text交互

```
//显示效果如图在最后面
//支持点击事件的text
int clickIndex = 0;
GestureDetector(
onTap: () {
setState(() {
clickIndex++;
});
},
child: Container(
color: Colors.yellow,
child: Text(
r'点击我吧$clickIndex',
textAlign: TextAlign.center,
),
),
)
```

#### 背景圆角,背景渐变,点击背景反馈
```
//圆角
Container(
height: 50,
alignment: Alignment.center, //child居中
child: Text(
'我的圆角',
textAlign: TextAlign.center,
style: new TextStyle(fontSize: 15, color: Color(0xFFFFFFFF)),
),
decoration: BoxDecoration(
border: new Border.all(color: Color(0xFF00FF00), width: 2), //描边
color: Color.fromARGB(255, 255, 0, 0),
borderRadius: BorderRadius.circular(20),
shape: BoxShape.rectangle,
),
),

//背景渐变
Container(
height: 50,
alignment: Alignment.center, //child居中
child: Text(
'渐变的背景',
textAlign: TextAlign.center,
style: new TextStyle(fontSize: 15, color: Color(0xFFFFFFFF)),
),
decoration: BoxDecoration(
border: new Border.all(color: Color(0xFF00FF00), width: 2),
//描边
color: Color.fromARGB(255, 255, 0, 0),
borderRadius: BorderRadius.circular(20),
gradient: RadialGradient(colors: [
Color(0xFFF00F80),
Color(0xFF00FF00),
Color(0xFF00FF99)
], radius: 1, tileMode: TileMode.mirror),
shape: BoxShape.rectangle,
),
),

//点击背景反馈
GestureDetector(
onTapDown: (TapDownDetails details) {
setState(() {
enabled = true;
});
},
onTapUp: (details) {
setState(() {
enabled = false;
});
},
onTapCancel: (){
enabled = false;
},
onTap: (){
setState(() {
clickIndex++;
});
},
child: Container(
height: 50,
alignment: Alignment.center, //child居中
child: Text(
'点击背景反馈$clickIndex',
textAlign: TextAlign.center,
style: new TextStyle(fontSize: 15, color: Color(0xFFFFFFFF)),
),
decoration: BoxDecoration(
border: new Border.all(color: Color(0xFF00FF00), width: 2),
//描边
color: enabled
? Color.fromARGB(255, 255, 0, 0)
: Color(0x880000FF),
borderRadius: BorderRadius.circular(20),
shape: BoxShape.rectangle,
),
),
),
```

#### 支柱样式使用(参考官网)
```dart
//控制行高 = height*fontSize
Text(
'Hello, world!\nSecond line!',
style: TextStyle(
fontSize: 15,
fontFamily: 'Raleway',
shadows: shlist,
),
strutStyle: StrutStyle(
fontFamily: 'Roboto',
fontSize: 20,
height: 1.5,
),
),

//保证所以线高都是一样的不管字号设置多少
const Text.rich(
TextSpan(
text: 'First line!\n',
style: TextStyle(fontSize: 14, fontFamily: 'Roboto'),
children: <TextSpan>[
TextSpan(
text: 'Second line!\n',
style: TextStyle(
fontSize: 16,
fontFamily: 'Roboto',
),
),
TextSpan(
text: 'Third line!\n',
style: TextStyle(
fontSize: 14,
fontFamily: 'Roboto',
),
),
],
),
strutStyle: StrutStyle(
fontFamily: 'Roboto',
height: 1.5,
),
),

//重叠文字效果
const Text.rich(
TextSpan(
text: '---------         ---------\n',
style: TextStyle(
fontSize: 14,
fontFamily: 'Roboto',
),
children: <TextSpan>[
TextSpan(
text: '^^^M^^^\n',
style: TextStyle(
fontSize: 30,
fontFamily: 'Roboto',
),
),
TextSpan(
text: 'M------M\n',
style: TextStyle(
fontSize: 30,
fontFamily: 'Roboto',
),
),
],
),
strutStyle: StrutStyle(
fontFamily: 'Roboto',
fontSize: 14,
height: 1,
forceStrutHeight: true,
),
),

//锁定高度
Text.rich(
TextSpan(
text: '       he candle flickered\n',
style: TextStyle(
fontSize: 14,
fontFamily: 'Serif'
),
children: <TextSpan>[
TextSpan(
text: 'T',
style: TextStyle(
fontSize: 37,
fontFamily: 'Serif'
),
),
TextSpan(
text: 'in the moonlight as\n',
style: TextStyle(
fontSize: 14,
fontFamily: 'Serif'
),
),
TextSpan(
text: 'Dash the bird fluttered\n',
style: TextStyle(
fontSize: 14,
fontFamily: 'Serif'
),
),
TextSpan(
text: 'off into the distance.',
style: TextStyle(
fontSize: 14,
fontFamily: 'Serif'
),
),
],
),
strutStyle: StrutStyle(
fontFamily: 'Serif',
fontSize: 14,
forceStrutHeight: true,
),
),
```

#### 全部运行效果图:

[全部运行效果图](https://user-gold-cdn.xitu.io/2019/8/7/16c6b9a92b103247?imageView2/0/w/1280/h/960/ignore-error/1)
