# SingleChildScrollView

只能容纳一个子组件的滚动组件，当子组件超过父容器时就可以滚动，它相当于Android中的ScrollView

```
class SingleChildScrollViewDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return SingleChildScrollView(
        child: Center(
      child: Column(
        children: <Widget>[
          Container(height: 500, child: Text("hello world1")),
          Container(height: 500, child: Text("hello world2")),
          Container(height: 500, child: Text("hello world3")),
          Container(height: 500, child: Text("hello world4"))
        ],
      ),
    ));
  }
}
```

