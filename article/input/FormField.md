# FormField

## 介绍

FromField是一个抽象类，可用于表单校验。比如：发起一个请求，或者进行下一步时，可以在提交前进行一些校验，来保证表单中数据的合法性。
FromField中的数据可以是用户输入的，也可以是其它来源

其继承类有：

## 属性

### autovalidate → bool
当此值为true时，则此表单字段将在每次更改后立即验证并更新其错误文本。
不设置或设置为false时，必须调用 FormFieldState.validate 进行验证。
如果表单的 autocorrect（自动验证）为true，则该值将被忽略。

### builder → FormFieldBuilder < T >
返回表示此表单字段的窗口小部件的函数。它作为输入传递表单字段状态，包含该字段的当前值和验证状态。

### enabled → bool
使能，其决定用户是否可输入

### initialValue → T
初始化值，可用于设置表单的默认值

### onSaved → FormFieldSetter < T >
通过FormState.save保存表单时使用最终值调用的可选方法。

### validator → FormFieldValidator < T >
验证输入的可选方法。如果输入无效，则返回要显示的错误字符串，否则返回null。

## 例：
FromField是一个抽象类，这里我们用其继承类TextFormField

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
          Padding(
            padding: const EdgeInsets.symmetric(vertical: 16.0),
            //创建一个按钮用于点击，来校验表单
            child: RaisedButton(
              onPressed: () {
                //通过先定义一个GlobalKey来获取表单并进行校验
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