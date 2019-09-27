## 介绍

Dismissible 是一种可以通过沿指定的方向拖动来关闭的 Widget。
比如，若我们需要向左或者向右滑动来移除一个Widget（比如很常见的“滑动删除”功能），则非常适合使用Dismissible来实现。

## 继承关系

Object -> Diagnosticable -> DiagnosticableTree -> Widget -> StatefulWidget -> Dismissible

## 构造函数

```
Dismissible({@required Key key, 
@required Widget child, 
Widget background,
Widget secondaryBackground, 
ConfirmDismissCallback confirmDismiss, 
VoidCallback onResize,
DismissDirectionCallback onDismissed,
DismissDirection direction: DismissDirection.horizontal, 
Duration resizeDuration: const Duration(milliseconds: 300),
Map<DismissDirection, double> dismissThresholds: const {}, 
Duration movementDuration: const Duration(milliseconds: 200),
double crossAxisEndOffset: 0.0, 
DragStartBehavior dragStartBehavior: DragStartBehavior.start })
```
    
## 常用属性

- background → Widget
背景部件。如果还指定了secondaryBackground，则仅在子项被向下或向右拖动时才显示此小部件。

- child → Widget 子部件。

 - confirmDismiss → ConfirmDismissCallback
使应用有机会确认或取消的回调。

- crossAxisEndOffset → double
定义取消卡片后横过主轴的结束偏移量 

- direction → DismissDirection
可以关闭 Widget 的方向。

- dismissThresholds → Map<DismissDirection, double>
必须拖动项目才能被视为已取消的偏移阈值

- dragStartBehavior → DragStartBehavior
确定处理拖动开始行为的方式。

- movementDuration → Duration
定义了卡片退回或未退回原位置的持续时间。

- onDismissed → DismissDirectionCallback
完成调整大小后，在关闭窗口小部件时调用。

- onResize → VoidCallback
当窗口小部件更改大小时调用（即在关闭前收缩时调用）。

- resizeDuration → Duration
在调用onDismissed之前，窗口小部件所需花费的收缩时间。

- secondaryBackground → Widget
堆叠在子部件后面的背景部件，当子部件被向上或向左拖动时会暴露出来。只有在同时指定了背景时才能指定它。


## 使用示例 (实现滑动删除的 sample)

(参考地址 https://flutterchina.club/cookbook/gestures/dismissible/
)
### 1. 创建item列表

第一步是创建一个我们可以滑动的列表。有关如何创建列表的更多详细说明，请按照使用长列表进行操作。

#### 创建数据源

简单起见，这里生成一个字符串列表。

final items = new List<String>.generate(20, (i) => "Item ${i + 1}");

#### 将数据源转换为List

首先，我们将简单地在屏幕上的列表中显示每个项目(先不支持滑动)。

```
new ListView.builder(
  itemCount: items.length,
  itemBuilder: (context, index) {
    return new ListTile(title: new Text('${items[index]}'));
  },
);
```

### 2. 将item包装在Dismissible Widget中

现在我们希望让用户能够将条目从列表中移除，用户删除一个条目后，我们需要从列表中删除该条目并显示一个Snackbar。 在实际的场景中，您可能需要执行更复杂的逻辑，例如从Web服务或数据库中删除条目。

这是我们就可以使用Dismissable。在下面的例子中，我们将更新itemBuilder函数以返回一个DismissableWidget。

```
new Dismissible(
  // Each Dismissible must contain a Key. Keys allow Flutter to
  // uniquely identify Widgets.
  key: new Key(item),
  // We also need to provide a function that will tell our app
  // what to do after an item has been swiped away.
  onDismissed: (direction) {
    // Remove the item from our data source
    items.removeAt(index);

    // Show a snackbar! This snackbar could also contain "Undo" actions.
    Scaffold.of(context).showSnackBar(
        new SnackBar(content: new Text("$item dismissed")));
  },
  child: new ListTile(title: new Text('$item')),
);
```

### 3. 提供滑动背景提示

现在，我们的应用程序将允许用户从列表中滑动项目，但用户并不知道滑动后做了什么，所以，我们需要告诉用户滑动操作会移除条目。 为此，我们将在滑动条目时显示指示。在下面的例子中，我们通过将背景设置为红色表示为删除操作。

为此，我们为Dismissable提供一个background参数。
```
new Dismissible(
  // Show a red background as the item is swiped away
  background: new Container(color: Colors.red),
  key: new Key(item),
  onDismissed: (direction) {
    items.removeAt(index);

    Scaffold.of(context).showSnackBar(
        new SnackBar(content: new Text("$item dismissed")));
  },
  child: new ListTile(title: new Text('$item')),
);
```


### 完整代码：

```
import 'package:flutter/foundation.dart';
import 'package:flutter/material.dart';

void main() {
  runApp(new MyApp(
    items: new List<String>.generate(20, (i) => "Item ${i + 1}"),
  ));
}

class MyApp extends StatelessWidget {
  final List<String> items;

  MyApp({Key key, @required this.items}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    final title = 'Dismissing Items';

    return new MaterialApp(
      title: title,
      home: new Scaffold(
        appBar: new AppBar(
          title: new Text(title),
        ),
        body: new ListView.builder(
          itemCount: items.length,
          itemBuilder: (context, index) {
            final item = items[index];

            return new Dismissible(
              // Each Dismissible must contain a Key. Keys allow Flutter to
              // uniquely identify Widgets.
              key: new Key(item),
              // We also need to provide a function that will tell our app
              // what to do after an item has been swiped away.
              onDismissed: (direction) {
                items.removeAt(index);

                Scaffold.of(context).showSnackBar(
                    new SnackBar(content: new Text("$item dismissed")));
              },
              // Show a red background as the item is swiped away
              background: new Container(color: Colors.red),
              child: new ListTile(title: new Text('$item')),
            );
          },
        ),
      ),
    );
  }
}
```