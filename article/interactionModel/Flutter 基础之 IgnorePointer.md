
## 介绍

IgnorePointer 是一种在命中测试期间不可见的Widget部件。通俗地来说，如果我们不想让一个 Widget 接收到触摸事件，就用 IgnorePointer 包裹起来。

与AbsorbPointer相比较，虽然这两个Widget都能阻止子树接收指针事件，但不同之处在于AbsorbPointer本身会参与命中测试，而IgnorePointer本身不会参与。这就意味着AbsorbPointer本身是可以接收指针事件的(其子树不行)，而IgnorePointer则不可以。

（注意：只有通过命中测试的Widget才能触发事件）

## 继承关系

Object -> Diagnosticable -> DiagnosticableTree -> Widget RenderObjectWidget -> SingleChildRenderObjectWidget -> IgnorePointer

## 构造函数

```
IgnorePointer({Key key, bool ignoring: true, bool ignoringSemantics, Widget child }) 
```
    
## 常用属性

- ignoring → bool
是否在命中测试期间，忽略此Widget。

- ignoringSemantics → bool
编译语义树的时候, 是否忽略此呈现对象的语义。 


当ignoring为true时，这个Widget（及其子树）对hit测试是不可见的。但它仍然在布局时消耗空间，并像往常一样绘制其子对象。并且它不能作为已定位事件的目标，因为它从renderbox.hittest返回false。

当ignoringsemantics为true时，语义层将看不到子树（例如 ccessibility 工具）。如果ignoringsemantics为空，则使用忽略的值。

## 使用示例

#### 1. 不填 ignoring 参数的情况：

```
Widget getAbsorbPointerBody() {
  return Container(
    child: Listener(
      child: IgnorePointer(
        child: Listener(
          child: Container(
            color: Colors.red,
          ),
          onPointerDown: (event)=>print("IgnorePointer Child Listener"),
        ),
      ),
      onPointerDown: (event)=>print("IgnorePointer Parent Listener"),
    ),
  );
}
```

 运行应用，无日志打印出来，说明触摸指针事件被拦截了。
 
 
 #### 2. ignoring = false 的情况：
 
 ```
 Widget getAbsorbPointerBody() {
    return Container(
      child: Listener(
        child: IgnorePointer(
            child: Listener(
              child: Container(
                color: Colors.black87,
              ),
              onPointerDown: (event) =>
                  print("onReceived IgnorePointer Child Listener"),
            ),
            ignoring: false),
        onPointerDown: (event) =>
            print("onReceived IgnorePointer Parent Listener"),
      ),
    );
    
```
log 输出：

```
21:24:57.268 37 info flutter.tools I/flutter ( 9081): onReceived IgnorePointer Child Listener
21:24:57.268 38 info flutter.tools I/flutter ( 9081): onReceived IgnorePointer Parent Listener
```

从日志可以看到，IgnorePointer Widget 的子部件中的 Pointer 事件也触发了，并且符合事件触发的时序，子部件先于父部件触发。