### StreamBuilder介绍
前面介绍过FutureBuilder，它是一个Widget控件，提供了异步数据获取与ui更新的能力，StreamBuilder与FutureBuilder类似[[官方文档]]([https://api.flutter.dev/flutter/widgets/StreamBuilder-class.html](https://api.flutter.dev/flutter/widgets/StreamBuilder-class.html)
)，也是一个Widget控件，不一样的是FutureBuilder依靠Future来做异步数据获取，而StreamBuilder则是依赖Stream来做异步数据获取。

### Stream介绍
在讲StreamBuilder前得先介绍下Stream这个东西。通俗点讲，Stream就是个事件流，有点类似于RxJava，它允许我们从一端发射一个事件，从另外一端去监听事件的变化，通过Stream我们可以在Flutter上设计出基于事件流驱动的响应式代码逻辑。

### Stream的简单实用
事实上Stream并是不Flutter的产物，而是由Dart提供的，Stream是一个抽象的接口，Dart提供了StreamController接口类可以让我们方便的使用Stream，步骤大致如下：
- 创建`StreamController`
- 获取`StreamSink `用作发射事件
- 获取`Stream`用作事件的监听
- 获取`StreamSubscription `用作管理监听，关闭暂停等
```dart
  StreamSubscription<String> subscription;
  //创建StreamController
  var streamController = StreamController<String>();
  // 获取StreamSink用于发射事件
  StreamSink<String> get streamSink  => streamController.sink;
  // 获取Stream用于监听
  Stream<String> get streamData => streamController.stream;

  //监听事件
  subscription = streamData.listen((value) {
        // do something
  });

 //发射一个事件.
streamSink.add(index.toString());
```

### StreamBuilder的使用介绍
- 构造方法
```dart
StreamBuilder({Key key, T initialData, Stream<T> stream, @required AsyncWidgetBuilder<T> builder })
```
`initialData` : 默认初始化数据
`stream` : stream事件流对象
`builder` :  负责根据不同状态创建对应ui的方法实现
AsyncWidgetBuilder前面在讲FutureBuilder的时候已经介绍过，这里不再赘述。
- 其他方法
`afterConnected`:返回一个AsyncSnapshot，当订阅了stream时会回调此AsyncSnapshot
`afterData`:返回一个AsyncSnapshot，当stream有事件触发时会回调此AsyncSnapshot
`afterDisconnected`:返回一个AsyncSnapshot，当取消订阅stream时会回调此AsyncSnapshot
`afterDone`:返回一个AsyncSnapshot，当stream被关闭时会回调此AsyncSnapshot
`afterError`:返回一个AsyncSnapshot，stream发生错误时会回调此AsyncSnapshot

StreamBuilder 内部已经帮我们完成了stream的订阅与取消订阅，在initState的时候进行事件的订阅，在dispose的时候进行事件的反订阅，源码在`_StreamBuilderBaseState`里，关键过程大致如下
```dart
void initState() {
    super.initState();
    _summary = widget.initial();
    _subscribe();
  }

void dispose() {
    _unsubscribe();
    super.dispose();
  }
void _subscribe() {
    if (widget.stream != null) {
      _subscription = widget.stream.listen((T data) {
        setState(() {
          _summary = widget.afterData(_summary, data);
        });
      }, onError: (Object error) {
        setState(() {
          _summary = widget.afterError(_summary, error);
        });
      }, onDone: () {
        setState(() {
          _summary = widget.afterDone(_summary);
        });
      });
      _summary = widget.afterConnected(_summary);
    }
  }
  void _unsubscribe() {
    if (_subscription != null) {
      _subscription.cancel();
      _subscription = null;
    }
  }
```
从上面的源码里面我们也可以清楚得看见StreamBuilder的各个回调方法的调用过程。

### 完整例子
下面给出一个完整的代码例子，我们的页面在初始化的时候创建了`StreamController`，页面上面有个按钮，当点击按钮的时候就会发射出一个事件，StreamBuilder订阅了这个事件，并且把data打印出来
```dart
import 'dart:async';

import 'package:flutter/material.dart';
import 'dart:io';
import 'dart:convert';

/**
 * Created by nls on 2019/7/20.
 * Nothing.
 */
class StreamBuilderDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      theme: ThemeData(primaryColor: Colors.blue),
      home: HomeWidget());
  }
}

class HomeWidget extends StatefulWidget {
  @override
  State createState() {
    return HomeState();
  }
}

class HomeState extends State<HomeWidget> {
  var index = 0;
  StreamSubscription<String> subscription;
  //创建StreamController
  var streamController;
  // 获取StreamSink用于发射事件
  StreamSink<String> get streamSink  => streamController.sink;
  // 获取Stream用于监听
  Stream<String> get streamData => streamController.stream;

  void onFloatActionButtonPress() {
    //发射一个事件.
    streamSink.add(index.toString());
    index++;
  }

  @override
  void initState() {
    super.initState();
    streamController = StreamController<String>();
    streamSink.add("0");
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(title: Text('streamBuilder')),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            StreamBuilder<String>(
              stream: streamData,
              builder: (BuildContext context, AsyncSnapshot<String> snapshot) {
                return Text('Result: ${snapshot.data}');
              }
            )
          ],
        )
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: onFloatActionButtonPress,
          child: Icon(Icons.add))
    );
  }
}
```
