## 介绍
MediaQuery 用于查询解析给定数据的媒体信息（例如，window宽高/横竖屏/像素密度比 等信息）官方提供这个组件让开发者可以获取想要的数据。它主要用于不同尺寸大小设备的适配。

官网介绍视频：https://www.youtube.com/watch?v=A3WrA4zAaPw

## 继承关系
Object -> Diagnosticable -> DiagnosticableTree -> Widget  -> ProxyWidget -> InheritedWidget -> MediaQuery

## 构造函数

```
MediaQuery({Key key, @required MediaQueryData data, @required Widget child })
```

除上之外，MediaQuery 还有三个工厂构造函数，分别是：

#### 1. MediaQuery.removePadding
```
  factory MediaQuery.removePadding({
    Key key,
    @required BuildContext context,
    bool removeLeft = false,
    bool removeTop = false,
    bool removeRight = false,
    bool removeBottom = false,
    @required Widget child,
  }) {
    return MediaQuery(
      key: key,
      data: MediaQuery.of(context).removePadding(
        removeLeft: removeLeft,
        removeTop: removeTop,
        removeRight: removeRight,
        removeBottom: removeBottom,
      ),
      child: child,
    );
  }
```

#### 2. MediaQuery.removeViewInsets

```
  factory MediaQuery.removeViewInsets({
    Key key,
    @required BuildContext context,
    bool removeLeft = false,
    bool removeTop = false,
    bool removeRight = false,
    bool removeBottom = false,
    @required Widget child,
  }) {
    return MediaQuery(
      key: key,
      data: MediaQuery.of(context).removeViewInsets(
        removeLeft: removeLeft,
        removeTop: removeTop,
        removeRight: removeRight,
        removeBottom: removeBottom,
      ),
      child: child,
    );
  }
```

#### ~~3. MediaQuery.removeViewPadding~~ Google API 文档还有该方法，但是源码已找不到了，估计是代码已被删除但文档尚未更新。

从上述几个工厂构造函数的源码我们不难看出，实际上工厂函数其实也是通过MediaQuery.of(context)方法获取MediaQueryData 对象，然后操作MediaQueryData 对象的对应方法，去设置相关属性值，至于这两个工厂构造函数的具体作用，大家有兴趣的同学可以查阅MediaQueryData的相应源代码，或者看这篇文章：[《Flutter 基础之 MediaQueryData》](https://github.com/YYFlutter/flutter-article/blob/master/article/styling/Flutter%20%E5%9F%BA%E7%A1%80%E4%B9%8B%20MediaQueryData.md)

## 常用方法
- debugFillProperties(DiagnosticPropertiesBuilder properties) → void **添加与节点关联的其他属性。**
- updateShouldNotify(covariant MediaQuery oldWidget) → bool **系统是否应通知从此Widget基础的Widgets.**
- of(context) → MediaQueryData， **是一个静态方法,返回context所在范围的MediaQueryData对象。**
- boldTextOverride(BuildContext context) → bool **返回最近的context 中MediaQuery 对boldText的辅助功能设置，如果不存在，则返回false。**
-  platformBrightnessOf(BuildContext context) → Brightness **返回最近的MediaQuery 的platformBrightness 对象，若不存在，则返回 Brightness.light。**

## 常用属性

data → MediaQueryData 

[点我查看MediaQueryData 详细介绍](https://github.com/YYFlutter/flutter-article/blob/master/article/styling/Flutter%20%E5%9F%BA%E7%A1%80%E4%B9%8B%20MediaQueryData.md)

示例：

```
var deviceData = MediaQuery.of(context); // 返回 MediaQueryData
var width = deviceData.size.width; //返回context所在的窗口宽度
var height = deviceData.size.height;//返回context所在的窗口高度
```

### 注意事项

使用MediaQuery必须要MaterialApp 或者WidgetsApp 去包裹我们的Widget，这样才能够提供正常使用它，否则会出现错误:
```
Flutter Error: MediaQuery.of() called with a context that does not contain a MediaQuery。
```
另外，在当前小部件中使用了上一个小部件的 context，来调用 MediaQuery.of(context) 获取数据的时候，也会出现上述错误。

## 使用示例

使用MediaQuery.of方法，可以获取给定BuildContext的当前MediaQueryData。例如，要获取当前window的大小，可以使用MediaQuery.of(context).size。

```
void main() => runApp(App());

class App extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'MediaQueryDemo',
      home: HomePage(),
    );
  }
}

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final size = MediaQuery.of(context).size;

    return Container(
      child: ...,
    );
  }
}
```

## 总结

通过这篇文章的学习，我们熟悉了MediaQuery的概念及所提供的功能，通过它我们可以拿到widget窗口的宽高、横竖屏等信息。除了MediaQuery以外，实际上我们也可以通过GlobalKey来获取该widget的size。大家有兴趣也可以去了解通过GlobalKey的获取宽高的方式。
