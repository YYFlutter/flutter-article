# Form

## 介绍
From：表单，其可对其继承于FormField的子控件进行表单校验。

## 属性

### autovalidate → bool
当此值为true时，则此表单字段将在每次更改后立即验证并更新其错误文本。
如果表单的 autocorrect（自动验证）为true，则该值将被忽略。
注意：若其子控件也设置了此值，则以子控件为准

### child → Widget
子控件

### onChanged → VoidCallback
当其子控件中有一个改变了值，此函数便会回调

## 例：

源码：
```dart
// Create a Form Widget
class MyCustomForm extends StatefulWidget {
  @override
  MyCustomFormState createState() {
    return MyCustomFormState();
  }
}

class MyCustomFormState extends State<MyCustomForm> {
  // 先定义一个GlobalKey，用来获取表单实例
  final _formKey = GlobalKey<FormState>();

  @override
  Widget build(BuildContext context) {
    // 创建一个表单Form，所有的FormField都要放在Form中才能进行验证
    return Form(
      key: _formKey,
      child: Column(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: <Widget>[
          //此处创建一个TextFormField，用于用户输入
          TextFormField(
            //校验函数
            validator: (value) {
              if (value.isEmpty) {
                return 'Please enter some text';
              }
            },
          ),
          //这里可以继续添加其它FormField控件
          Padding(
            padding: const EdgeInsets.symmetric(vertical: 16.0),
            //创建一个按钮用于点击，来校验表单
            child: RaisedButton(
              onPressed: () {
                //通过先定义一个GlobalKey来获取表单并进行校验
                //Form下面的所有FormField控件都会进行校验
                if (_formKey.currentState.validate()) {
                  //todo 。。。
                }
              },
              child: Text('Submit'),
            ),
          ),
        ],
      ),
    );
  }
}
```

