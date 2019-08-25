## Padding 类 

### 介绍
它是一个Widget，写过前端代码的童鞋应该都了解这个属性，它就是设置内边距属性。通过Padding，可以有效地在子级的四周创建空的区域，内边距的空白区域，也是widget的一部分。

Padding的布局分为两种情况：

- 当child为空的时候，会创建一个宽为left+right，高为top+bottom的区域；
- 当child不为空的时候，Padding会将布局的约束传递给child，根据设置的padding属性，缩小child的布局尺寸。然后Padding将自己调整到child设置了padding属性的尺寸，在child周围创建空白区域。

此外，需要注意的是，Flutter中并没有单独的Margin控件。在Container中虽然也有margin属性，但我们看看源码关于margin的实现：
    
```
if (margin != null)
  current = new Padding(padding: margin, child: current);
```
  
从上面不难看出Flutter淡化了margin以及padding的区别，margin实质上也是由Padding Widget 来实现的。


### 设计缘由

为什么要使用一个Padding Widget组件，而不是一个 Container 容器用一个Container.padding 属性?

实际上两者的本质没有任何区别，如果你用了Container.padding 参数，那么 Container 实际上也是会帮你创建一个简单的 Padding Widget。Padding本身是非常简单的，基本上需要间距的地方，它都能够使用；如果在单一的内间距场景，使用Padding比Container的成本要小一些，因为Container里面除了Padding，它还包含了很多个widget。Padding能够实现的，Container都能够实现，只不过，Container提供的东西更多。Container 将许多更简单的小部件组合到一个 package 去进去了。

实际上，Flutter中的大多数Widgets都只是其他更简单的Widgets的组合。组合而不是继承,这是是构建Widgets的主要机制。


### 继承关系
Object -> Diagnosticable -> DiagnosticableTree -> Widget -> RenderObjectWidget -> SingleChildRenderObjectWidget -> Padding

### 构造函数
Padding（{ Key key， @ required EdgeInsetsGeometry padding， Widget child }）
创建一个携带子项的Widget，传入参数不为空，否则会报异常。

```
const Padding({
  Key key,
  @required this.padding,
  Widget child,
}) : assert(padding != null),
     super(key: key, child: child);
```

### 常用属性

- padding → EdgeInsetsGeometry

    - 插入子级的边距空间值。
    - 参数类型为EdgeInsetsGeometry，它是EdgeInsets以及EdgeInsetsDirectional的基类。在实际使用中若不涉及到国际化，例如适配阿拉伯地区等，则一般都是使用 EdgeInsets。从EdgeInsetsDirectional的命名我们可以推断，它跟方向相关。它的四个边距不限定上下左右，而是根据方向来定的，这样可以做国际化 适配。（和Android 的 paddingLeft/paddingStart 思想一致）
    - [EdgeInsets](https://api.flutter.dev/flutter/painting/EdgeInsets-class.html)，该类是用于描述 padding 的屏幕尺寸相关的类。

- child → widget
    - final, inherited
    - 子级

- hashCode → int
    - 此对象的哈希码。
    - read-only, inherited

- key → Key
    - 控制一个小部件如何替换树中的另一个小部件。[...]
    - final, inherited
    
- runtimeType → 类型
    - 表示对象的运行时类型。
    - read-only, inherited
    
### 常用方法

- **createRenderObject（BuildContext context） → RenderPadding**
    
    创建一个RenderObject 类，RenderObjectWidget表示的实例。

- **debugFillProperties（DiagnosticPropertiesBuilder properties） →void**
    
    添加与节点关联的其他属性。
    
- **updateRenderObject（BuildContext context， covariant RenderPadding renderObject） →void**

    顾名思义该方法用于将此RenderObjectWidget描述的配置，复制到给定的RenderObject 对象。该类型与此对象的createRenderObject返回的类型相同。
    

使用示例：

```
 Padding(
  padding: EdgeInsets.all(10.0),
  child: const Card(child: Text('Flutter Padding Example')),
)
```

## 总结

Padding 本身算是非常简单的Widget了，它主要用作设置子控件的内边距。Padding 能实现的，Container都能够实现。只不过，Container组合了更多的简单Widget进去，平时开发中我们可以根据实际需要来使用 Padding 或者 Container。