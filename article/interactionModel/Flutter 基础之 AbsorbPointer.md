## 介绍

AbsorbPointe 它是一个在命中测试期间吸收指针事件的Widget。

与 IgnorePointer 相比较，虽然这两个Widget都能阻止子树接收指针事件，但不同之处在于 AbsorbPointer 本身会参与命中测试，而 IgnorePointer 本身不会参与。这就意味着 AbsorbPointer 本身是可以接收指针事件的(其子树不行)，而 IgnorePointer 则不可以。

（注意：只有通过命中测试的Widget才能触发事件）

## 继承关系

Object -> Diagnosticable -> DiagnosticableTree -> Widget RenderObjectWidget -> SingleChildRenderObjectWidget -> AbsorbPointer

## 构造函数

```
AbsorbPointer({Key key, bool absorbing: true, Widget child, bool ignoringSemantics })
```
    
## 常用属性

- absorbing → bool
是否在命中测试期间吸收指针事件。

- ignoringSemantics → bool
编译语义树的时候, 是否忽略此呈现对象的语义。 

当 absorbing 值为tru的时候，此Widget通过终止自身的命中测试来防止其子树接收指针事件。它仍然会在布局时消耗空间，并像往常一样绘制其子对象。实际上它只是防止其子组件成为已定位事件的目标，而它自身不会，因为它从renderbox.hittest返回true。

## 使用示例

#### 1. 不填 absorbing 参数的情况：

```
@override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: getAbsorbPointerBody(),
    );
  }
  
 Widget getAbsorbPointerBody() {
    return Container(
      child: Listener(
        child: AbsorbPointer(
          child: Listener(
            child: Container(
              color: Colors.black87,
            ),
            onPointerDown: (event) => print("onReceived AbsorbPointer Child Pointer"),
          ),
        ),
        onPointerDown: (event) => print("onReceived AbsorbPointer Parent Pointer"),
      ),
    );
  }
  
```

log 输出：

```
21:13:07.305 9 info flutter.tools I/flutter ( 9081): onReceived AbsorbPointer Parent Listener
```
通过日志我们发现，AbsorbPointer 的子部件 Pointer 事件未触发。

#### 2. absorbing = false 的情况：

```
  Widget getAbsorbPointerBody() {
    return Container(
      child: Listener(
        child: AbsorbPointer(
            child: Listener(
              child: Container(
                color: Colors.black87,
              ),
              onPointerDown: (event) =>
                  print("onReceived AbsorbPointer Child Listener"),
            ),
            absorbing: false),
        onPointerDown: (event) =>
            print("onReceived AbsorbPointer Parent Listener"),
      ),
    );
  }
```

log 输出：
```
21:15:33.475 25 info flutter.tools I/flutter ( 9081): onReceived AbsorbPointer Child Listener
21:15:33.475 26 info flutter.tools I/flutter ( 9081): onReceived AbsorbPointer Parent Listener
```

从日志可以看到，AbsorbPointer Widget 的子部件中的 Pointer 事件也触发了，并且符合事件触发的时序，子部件先于父部件触发。



