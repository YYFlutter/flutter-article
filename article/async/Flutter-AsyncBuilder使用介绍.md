### AsyncBuilder介绍
AsyncBuilder名字起得有点怪，实际上它是一个Widget控件[[官方文档]]([https://api.flutter.dev/flutter/widgets/FutureBuilder-class.html](https://api.flutter.dev/flutter/widgets/FutureBuilder-class.html)
)，它把异步操作与数据更新结合在一起，举个例子，以首页为例，通常显示首页的时候会先判断首页数据拉取下来了没，没有没有就显示loading，如果有就直接渲染首页数据，代码逻辑大概是这样
```java
if (data == null) {
    fetchData();
    showLoading();
} else {
    showMainPage();
    hideLoading();
}
```
可以看出来数据的获取跟ui的更新都是分开的，而AsyncBuilder正是把数据获取与数据ui更新绑定在一起，在使用AsyncBuilder时我们只需要给它传递一个Future对象，负责数据的获取，以及实现一个AsyncWidgetBuilder回调方法，负责对应ui的创建显示即可，下面具体说说它的用法。

### AsyncBuilder使用介绍
- 构造方法
```java
FutureBuilder({Key key, Future<T> future, T initialData, @required AsyncWidgetBuilder<T> builder })
```
`future` : 异步io操作的Future对象
`initialData` : 默认初始化数据
`builder` :  负责根据不同状态创建对应ui的方法实现
- Future对象
future对象的创建必须要提前，譬如可以在 State.initState State.didUpdateConfig, 或者 State.didChangeDependencies等时期创建，不能在State.build 或者StatelessWidget.build回调时去创建，如果在创建FutureBuilder时同时创建Future，那么一旦FutureBuilder的parent Widget发生变化时，异步任务都会被触发。

- AsyncWidgetBuilder 方法
AsyncWidgetBuilder是接受两个参数`BuildContext context` 跟`AsyncSnapshot<T> snapshot`并且返回一个Widget对象的方法，其中`AsyncSnapshot<T> snapshot`包含了异步io操作的一些信息回调，其中有：
1 `connectionState `：枚举对象，它的值可以是`none` `waiting ` `active ` `done ` 
2 `data `：异步io处理完时回调的数据
3 `error `：异步io处理发生错误时回调

### 完整例子
下面给出一个完整的代码例子，启动页面的时候会先显示Awaiting的状态，同时会去请求百度的页面，请求回来了就打印下数据
```java
import 'package:flutter/material.dart';
import 'dart:io';
import 'dart:convert';
/**
 * Created by nls on 2019/7/20.
 * Nothing.
 */
class FutureBuilderDemo extends StatelessWidget {
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
  var futureFetchData;
  @override
  void initState() {
    super.initState();
    futureFetchData = fetchData();
  }

  Future<String> fetchData() async {
    var httpClient = new HttpClient();
    var uri = Uri.parse('http://www.baidu.com');
    var request =  await httpClient.getUrl(uri);
    var response =  await request.close();
    var responseBody = await response.transform(utf8.decoder).join();
    return responseBody;
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("futureBuilder")),
      body: Container(
        padding: const EdgeInsets.all(10),
        child: FutureBuilder<String>(
          future: futureFetchData, // a previously-obtained Future<String> or null
          builder: (BuildContext context, AsyncSnapshot<String> snapshot) {
            switch (snapshot.connectionState) {
              case ConnectionState.none:
                return Text('Press button to start.');
              case ConnectionState.active:
              case ConnectionState.waiting:
                return Text('Awaiting result...');
              case ConnectionState.done:
                if (snapshot.hasError)
                  return Text('Error: ${snapshot.error}');
                return Text('Result: ${snapshot.data}');
            }
            return null; // unreachable
          },
        ),
      )
    );
  }
}

```
