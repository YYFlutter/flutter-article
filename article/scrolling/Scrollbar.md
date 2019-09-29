# Scrollbar

Scrollbar是一个Material风格的滚动指示器，如果给可滚动的组件添加上滚动条，那么就可以使用该组件，还可以使用ScrollController来监听当前滚动到的位置。如果要使用iOS的滚动条风格，就是使用CupertinoScrollbar来代替Scrollbar。

可滚动的组件添加滚动条，那么就它就要成为Scrollbar的子组件。Scrollbar对子组件是有要求的，这个子组件必须包含ScrollNotification，例如ListView或者CustomScrollView

```
class SingleChildScrollViewDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scrollbar(
        child: SingleChildScrollView(
            child: Center(
      child: Column(
        children: <Widget>[
          Container(height: 500, child: Text("hello world1")),
          Container(height: 500, child: Text("hello world2")),
          Container(height: 500, child: Text("hello world3")),
          Container(height: 500, child: Text("hello world4"))
        ],
      ),
    )));
  }
}

```
