## 一、介绍

Theme 类将主题应用于子控件，Theme（主题）它描述了应用程序的颜色和排版选择。Theme有两种：全局Theme和局部Theme。全局Theme是由应用程序根MaterialApp创建的Theme；而局部Theme是在应用程序某个区域范围中用于覆盖全局主题。

Google官网介绍：https://api.flutter.dev/flutter/material/Theme-class.html

### 构造函数

```
Theme({Key key,
@required ThemeData data,
bool isMaterialAppTheme: false, 
@required Widget child })
```

- ThemeData data: 保存 Material 主题的颜色和字体等排版样式。
- isMaterialAppTheme： 默认值是false ，表示是否为材料设计风格的主题。
- child： 子控件。


### 继承关系

Object -> Diagnosticable -> DiagnosticableTree -> Widget -> StatelessWidget  -> Theme。

## 二、ThemeData

从Theme的构造函数我们不难看出，Flutter 中是通过ThemeData去保存共享应用的主题及样式等信息的，因此我们继续翻一下官方文档，研究研究一下ThemeData包含了哪些知识点。 

**继承关系：**
Object -> Diagnosticable -> ThemeData

**构造函数：**
```
ThemeData({Brightness brightness,
MaterialColor primarySwatch, 
Color primaryColor, 
Brightness primaryColorBrightness, 
Color primaryColorLight, 
Color primaryColorDark, 
Color accentColor, 
Brightness accentColorBrightness,
Color canvasColor, 
Color scaffoldBackgroundColor, 
Color bottomAppBarColor, 
Color cardColor, 
Color dividerColor, 
Color focusColor, 
Color hoverColor, 
Color highlightColor, 
Color splashColor, 
InteractiveInkFeatureFactory splashFactory, 
Color selectedRowColor, 
Color unselectedWidgetColor, 
Color disabledColor, 
Color buttonColor, 
ButtonThemeData buttonTheme,
Color secondaryHeaderColor,
Color textSelectionColor,
Color cursorColor, 
Color textSelectionHandleColor, 
Color backgroundColor, 
Color dialogBackgroundColor, 
Color indicatorColor, 
Color hintColor, 
Color errorColor, 
Color toggleableActiveColor, 
String fontFamily, 
TextTheme textTheme, 
TextTheme primaryTextTheme, 
TextTheme accentTextTheme, 
InputDecorationTheme inputDecorationTheme, 
IconThemeData iconTheme, 
IconThemeData primaryIconTheme, 
IconThemeData accentIconTheme, 
SliderThemeData sliderTheme, 
TabBarTheme tabBarTheme,
CardTheme cardTheme, 
ChipThemeData chipTheme, 
TargetPlatform platform, 
MaterialTapTargetSize materialTapTargetSize, 
PageTransitionsTheme pageTransitionsTheme,
AppBarTheme appBarTheme,
BottomAppBarTheme bottomAppBarTheme, 
ColorScheme colorScheme, 
DialogTheme dialogTheme, 
FloatingActionButtonThemeData floatingActionButtonTheme, 
Typography typography, 
CupertinoThemeData cupertinoOverrideTheme, 
SnackBarThemeData snackBarTheme, 
BottomSheetThemeData bottomSheetTheme })
```
从其构造函数不难看出，它主要保存了各种颜色及字体、Icon样式等设置。由于属性过多，我们挑一些常用的讲一讲：

- brightness - Brightness类型，应用程序的整体主题亮度。用于按钮等小部件，以确定在不使用主色（primaryColor）或强调色（accentColor）时选择什么颜色。当亮度较暗时，画布、卡片和原色都较暗。当亮度为光时，画布和卡片的颜色是明亮的，原色的暗度根据原色亮度变化。当亮度较暗时，原色（primaryColor）与卡片和画布颜色的对比度较差;当亮度较暗时，用白色或亮蓝色来对比。
- primarySwatch - MaterialColor 类型，Material 主题中定义一种颜色，它具有十种颜色阴影的颜色样本。值越大颜色越深，10个有效的index分别为：50，100，200，…，900。默认是取中间值500。

- primaryColor - Color类型，App主要部分的背景色（ToolBar,Tabbar等）

- primaryColorBrightness - Brightness类型，primaryColor的亮度，用于确定设置在primaryColor上部的文本和图标颜色(如:工具栏文本(toolbar text))。

- primaryColorLight - Color类型，primaryColor的较浅版本

- primaryColorDark - Color类型，primaryColor的较深版本

- accentColor - Color类型，前景色(按钮、文本、覆盖边缘效果等)
- accentColorBrightness - Brightness类型，accentColor的亮度。用于确定位于accentColor上部的文本和图标颜色(例如，浮动操作按钮(FloatingButton)上的图标)

- canvasColor - Color类型，MaterialType.canvas Material的默认颜色。

- scaffoldBackgroundColor - Color类型，作为Scaffold下的Material默认颜色，用于materia应用程序或app内页面的背景色。

- bottomAppBarColor - Color类型，bottomAppBarColor的默认颜色。这可以通过指定BottomAppBar.color来覆盖。

- cardColor - Color类型，用在卡片(Card)上的Material的颜色。

- dividerColor - Color类型，分隔符(Dividers)和弹窗分隔符(PopupMenuDividers)的颜色，也用于ListTiles和DataTables的行之间。要创建使用这种颜色的合适的边界，请考虑Divider.createBorderSide。

- highlightColor - Color类型，用于墨水喷溅动画或指示菜单被选中时的高亮颜色

- splashColor - Color类型，墨水溅出的颜色

- splashFactory - InteractiveInkFeatureFactory类型，定义InkWall和InkResponse产成的墨水喷溅时的外观。

- selectedRowColor - Color类型，用于高亮选定行的颜色。

- unselectedWidgetColor - Color类型，小部件处于非活动(但启用)状态时使用的颜色。例如，未选中的复选框。通常与accentColor形成对比。

- disabledColor - Color类型，无效的部件(widget)的颜色，不管它们的状态如何。例如，一个禁用的复选框(可以选中或不选中)。

- buttonColor - Color类型，Material中RaisedButtons使用的默认填充色。

- buttonTheme - ButtonThemeData类型，定义按钮小部件的默认配置，如RaisedButton和FlatButton。

- secondaryHeaderColor - Color类型，有选定行时PaginatedDataTable标题的颜色

- textSelectionColor - Color类型，文本字段(如TextField)中文本被选中的颜色。

- cursorColor - Color类型，在 Material-style 文本字段(如TextField)中光标的颜色。

- textSelectionHandleColor - Color类型，用于调整当前选定文本部分的句柄的颜色。

- backgroundColor - Color类型，与primaryColor对比的颜色(例如 用作进度条的剩余部分)。

- dialogBackgroundColor - Color类型，Color类型，Dialog元素的背景色

- indicatorColor - Color类型，TabBar中选项选中的指示器颜色。

- hintColor - Color类型，用于提示文本或占位符文本的颜色，例如在TextField中。

- errorColor - Color类型，用于输入验证错误的颜色，例如在TextField中。

- toggleableActiveColor - Color类型，用于突出显示切换Widget（如Switch，Radio和Checkbox）的活动状态的颜色。

- fontFamily - String类型，字体类型

- textTheme - TextTheme类型，与卡片和画布对比的文本颜色

- primaryTextTheme - TextTheme类型，与primary color形成对比的文本主题。

- accentTextTheme - TextTheme类型，与accent color形成对比的文本主题。

- inputDecorationTheme - InputDecorationTheme类型，InputDecorator、TextField和TextFormField的默认InputDecoration值基于此主题。

- iconTheme - IconThemeData类型，与卡片和画布颜色形成对比的图标主题。

- primaryIconTheme - IconThemeData类型，与原色(primary color)形成对比的图标主题。


- accentIconTheme - IconThemeData类型,与前景色(accent color)形成对比的图标主题。

- sliderTheme - SliderThemeData类型，SliderThemeData类型，用于渲染Slider的颜色和形状。

- tabBarTheme - TabBarTheme类型, 一个主题，用于自定义选项卡栏指示器的尺寸、形状和颜色。

- chipTheme - ChipThemeData类型,用于Chip的颜色和样式

- platform - TargetPlatform类型,widget应该适应目标的平台。

- materialTapTargetSize - MaterialTapTargetSize类型,配置特定材料部件的hit测试大小。

- pageTransitionsTheme - PageTransitionsTheme类型,每个目标平台的默认MaterialPageRoute转换。

- colorScheme
ColorScheme类型,一组13种颜色，可用于配置大多数组件的颜色属性。

- typography - Typography类型,用于配置TextTheme、primaryTextTheme和accentTextTheme的颜色和几何文本主题值。

## 三、Theme.of 方法

它是一个 static 方法。子控件通过使用Theme.of来获取当前主题的ThemeData对象，当控件使用Theme.of时，如果主题稍后更改，则会自动重建以便可以应用更改。我们可以通过Theme.of查看当前应用程序的配色方案。

ThemeData.of 方法代码：
```
ThemeData of (
BuildContext context, {
bool shadowThemeOnly: false
})
```

ThemeData数据来自最近的给定上下文的Theme实例。如果给定的 context 包含在提供MaterialLocalizations的Localizations部件中，则返回的数据将根据最近的可用MaterialLocalizations进行本地化。如果给定的构建上下文中没有主题，则默认为新的ThemeData.fallback。

示例用法如下：
```
@override
Widget build(BuildContext context) {
  return Text(
    'Theme Example',
    style: Theme.of(context).textTheme.title,
  );
}
```
到这里我们已经知道如何去设置flutter主题了，在flutter中，主题又分全局主题和局部主题。接下来我们讲解一下这两种方式的适用场景及区别。

## 四、全局主题

在创建应用全局主题时，我们提供一个ThemeData对象给MaterialApp即可，如果构造函数没有设置ThemeData，则Flutter会创建一个默认的主题。下面我们实践一下，写个自定义全局主题的简单示例：

```
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
          brightness: Brightness.light, //指定亮度主题，有白色/黑色两种可选。
          primaryColor: Colors.blue[800], //这里我们选蓝色为基准色值。
          accentColor: Colors.lightBlue[100]), //这里我们选浅蓝色为强调色值。
      home: ThemeTest(),
    );
  }
}

class ThemeTest extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("ThemeTest"), //页面标题
      ),
      body: Container(
        color: Theme.of(context).primaryColor, //内容背景颜色
        margin: EdgeInsets.all(100.0),
        padding: EdgeInsets.all(10.0),
        child: Text(
          "MaterialApp Theme Color", //内容文本
          style: TextStyle(
              fontSize: 20, color: Theme.of(context).accentColor), //内容文本颜色，引用的是accentColor。
          textAlign: TextAlign.center,
        ),
      ),
    );
  }
}
```
效果图如下：

![theme.jpg](https://upload-images.jianshu.io/upload_images/4835249-c6801844621ce36f.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 五、局部主题

局部主题是在应用程序某些区域中，用于覆盖全局主题。我们定义好一个主题后，就可以在Widget的build方法中通过Theme.of(context)方法来使用它。Theme.of(context)将查找Widget树并返回树中最近的Theme。如果Widget之上有一个单独的局部Theme定义，则返回该主题的值；如果不是，则返回App全局主题。我们讲一下主要的几种创建方法：

### 5.1 重新创建Theme对象

通过重新创建Theme的方式，创建一个实例, 并重新创建ThemeData，赋值给data。然后指定child  Widget，将ThemeData传递给Theme Widget，代码如下：
```
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
        title: 'Flutter Demo',
        theme: ThemeData(
            brightness: Brightness.light, //指定亮度主题，有白色/黑色两种可选。
            primaryColor: Colors.blue[800], //这里我们选蓝色为基准色值。
            accentColor: Colors.lightBlue[100]), //这里我们选浅蓝色为强调色值。
        home: Theme(
            data: ThemeData(accentColor: Colors.yellow),
            child: ThemeTest())); //创建局部主题，将accentColor设置为黄色
  }
}

class ThemeTest extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("ThemeTest"),
      ),
      body: Container(
          color: Theme.of(context).primaryColor,
          margin: EdgeInsets.all(100.0),
          padding: EdgeInsets.all(10.0),
          child: Text(
            "MaterialApp Theme Color",
            style: TextStyle(
                fontSize: 20, color: Theme.of(context).accentColor), //应用局部主题颜色
            textAlign: TextAlign.center,
          )),
    );
  }
}
```

效果图如下：

![局部主题-黄色.jpg](https://upload-images.jianshu.io/upload_images/4835249-85aa2cb31eadc7eb.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 局部主题不生效问题

这里有个小坑点需要注意，我们需要在Widget的父层Widget去设置局部Theme，才会生效；如果我们直接在局部Theme的child 属性指定的Widget中去使用的话，会拿到系统的全局Theme.

如下示例：

```
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
          brightness: Brightness.light, //指定亮度主题，有白色/黑色两种可选。
          primaryColor: Colors.blue[800], //这里我们选蓝色为基准色值。
          accentColor: Colors.white), //设置为白色。
      home: ThemeTest(),
    );
  }
}

class ThemeTest extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("ThemeTest"),//页面标题
      ),
      body: Container(
          color: Theme.of(context).primaryColor,
          margin: EdgeInsets.all(100.0),
          padding: EdgeInsets.all(10.0),
          child: Theme(
              data: ThemeData(accentColor: Colors.red), //设置红色
              //创建accentColor 为绿色的局部主题，若局部主题Theme 的Child 是 Text，则Text引用局部主题色不会生效，拿到的还是局部Themes上层的值，即全局主题的值。
              child: Text(
                "MaterialApp Theme Color",
                style: TextStyle(
                    fontSize: 20, color: Theme.of(context).accentColor), //应用主题色
                textAlign: TextAlign.center,
              ))),
    );
  }
}
```

效果图如下：

![局部主题不生效.jpg](https://upload-images.jianshu.io/upload_images/4835249-df55b70de492e8d9.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

可以从截图看到，Text显示的颜色依旧是白色，并未变成我们所期望的红色,因此我们使用的时候需要额外注意这点。


### 5.2 扩展父主题

除了 创建Theme 对象的方式去使用局部主题，我们可以通过使用copyWith方法来实现，这样的话，我们去修改父主题时，无需覆盖所有的主题属性，只需要将我们想改动的属性指定即可。

将原先的:

```
data: ThemeData(accentColor: Colors.yellow)
```

改成：

```
Theme.of(context).copyWith(accentColor: Colors.yellow)
```
这样一来，我们的局部主题除了accentColor改成了指定值，其他属性依然可以使用它上一层 Theme的属性值，而不是变成系统默认的。


### 5.3 根据设备平台设置不同主题

除了上述两种方法之外，我们还可以根据设备的平台类型（iOS，Android和Fuchsia）去提供不同的主题：

```
import 'package:flutter/foundation.dart';
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
 
final ThemeData iOSTheme = ThemeData(
    brightness: Brightness.light,
    primaryColor: Colors.grey[600],
    accentColor: Colors.white,
  );

final ThemeData androidTheme = ThemeData(
    brightness: Brightness.dark,
    primaryColor: Colors.yellow[300],
    accentColor: Colors.deepPurple[800],
  );
  
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        brightness: Brightness.light,
        primaryColor: Colors.grey[100],
        accentColor: Colors.white,
      ),
      home: Theme(
          data: defaultTargetPlatform == TargetPlatform.android
              ? androidTheme
              : iOSTheme,
          child: ThemeTest()),
    );
  }
}

class ThemeTest extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("ThemeTest"),
      ),
      body: Container(
          color: Theme.of(context).primaryColor,
          margin: EdgeInsets.all(100.0),
          padding: EdgeInsets.all(10.0),
          child: Text(
            "MaterialApp Theme Color",
            style:
                TextStyle(fontSize: 20, color: Theme.of(context).accentColor),
            textAlign: TextAlign.center,
          )),
    );
  }
}


```

Android 端效果图：

![Android 端局部主题](https://upload-images.jianshu.io/upload_images/4835249-c7ee507fe2b4e099.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

iOS 端效果图：

![iOS 端局部主题](https://upload-images.jianshu.io/upload_images/4835249-9f9656893f18a1ac.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 六、总结
本篇文章主要讲述了Theme 的一些常用方法及属性。同时对全局主题、局部主题、不同平台主题的设置方法也做了较详细的实践示例。flutter 中对主题的设置相对而言比较灵活，