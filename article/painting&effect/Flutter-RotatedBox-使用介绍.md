### RotatedBox介绍
RotatedBox是个可以旋转其子widget的窗口小部件(widget)，不像Transform是在控件绘制前对其进行矩阵变换，RotatedBox是在控件layout的时候就对其子widget进行旋转处理，这意味着RotatedBox控件所需要的空间大小跟旋转子widget所需要的空间大小一样。

### RotatedBox使用
下面的代码段是展示了如何使用RotatedBox来旋转Text控件
```dart
RotatedBox(
  quarterTurns: 3, // 90°的整数倍
  child: const Text('Hello World!'),
)
```
### 完整例子
```dart
import 'package:flutter/material.dart';

/**
 * Created by nls on 2019/7/20.
 * Nothing.
 */
class RotatedBoxDemo extends StatelessWidget {


  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      theme: ThemeData(primaryColor: Colors.blue),
      home: HomeWidget(),
    );
  }
}

class HomeWidget extends StatefulWidget {

  @override
  State createState() {
    //return HomeState();
    return RotatedBoxState();
  }
}

class RotatedBoxState extends State<HomeWidget> {

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(title: Text('RotatedBoxDemo'),),
        body: Container(
          alignment: Alignment.center,
          child: RotatedBox(
            quarterTurns: 3, // 90°的整数倍
            child: const Text('Hello World!'),
          ),
        ));
  }
}
```
效果如下：
![](https://upload-images.jianshu.io/upload_images/2829725-d3b536fa1ab2db5a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

