# 《Flutter实战·第二版》
## 二、Flutter入门
### 2.2 Widget简介
#### 2.2.1 Widget概念
Flutter中的Widget概念相较于原生开发概念更加广泛，不仅仅可以表示UI元素，也可以表示一些功能性的组建——`GestureDetector(手势检测)`、`Theme(App主题传递)`等等，原生开发中的控件通常指代UI元素
Flutter中，万物皆为Widget

#### 2.2.2 Widget接口
Widget功能：描述一个UI元素的配置信息
Widget其实不是表示最终绘制在屏幕上的显示元素，所谓的配置信息就是Widget接收的参数
```Dart
@immutable //不可变——一旦 Widget 自己的属性变了自己就会被替换
abstract class Widget extends DiagnosticableTree {
//widget类继承自DiagnosticableTree，DiagnosticableTree即“诊断树”，主要作用是提供调试信息
  const Widget({ this.key });
//Key: 这个key属性类似于 React/Vue 中的key
//主要的作用是决定是否在下一次build时复用旧的widget ，决定的条件在canUpdate()方法中
  final Key? key;

  @protected
  @factory
  Element createElement();
//createElement()：正如前文所述“一个 widget 可以对应多个Element”
//Flutter 框架在构建UI树时，会先调用此方法生成对应节点的Element对象
//此方法是 Flutter 框架隐式调用的，在我们开发过程中基本不会调用到
  @override
  String toStringShort() {
    final String type = objectRuntimeType(this, 'Widget');
    return key == null ? type : '$type-$key';
  }

  @override
  void debugFillProperties(DiagnosticPropertiesBuilder properties) {
    super.debugFillProperties(properties);
    //debugFillProperties(...) 复写父类的方法，主要是设置诊断树的一些特性
    properties.defaultDiagnosticsTreeStyle = DiagnosticsTreeStyle.dense;
  }

  @override
  @nonVirtual
  bool operator ==(Object other) => super == other;

  @override
  @nonVirtual
  int get hashCode => super.hashCode;

  static bool canUpdate(Widget oldWidget, Widget newWidget) {
  //canUpdate(...)是一个静态方法，它主要用于在 widget 树重新build时复用旧的 widget 
  //只要newWidget与oldWidget的runtimeType和key同时相等时就会用new widget去更新Element对象的配置
  //否则就会创建新的Element
    return oldWidget.runtimeType == newWidget.runtimeType
        && oldWidget.key == newWidget.key;
  }
  ...
}
```
ps：`Widget`类本身是一个抽象类，其中最核心的就是定义了`creatElement()`接口，在 flutter 开发中，一般不用直接继承`Widegt`类来实现新组建，与之相反，我们通常会通过继承`StatelessWidget`或`StatefluWidget`来间接继承`widget`类
`StatelessWidget`与`StatefluWidget`都是直接继承自`widget`，这两个类也是 Flutter中极为重要的两个抽象类
#### 2.2.3 Flutter中的四棵树
Flutter框架的处理流程：
1. 根据Widget树生成一个Element树，Element树中所有节点都继承自`Element`类
2. 根据Element树生成Render树（渲染树），渲染树中的所有节点都继承自`RenderObject`类
3. 根据渲染树生成Layer树然后上屏显示，Layer树中的所有节点都继承自`Layer`类

真正的布局和渲染逻辑在Render树中，Element是Widget和RenderObject的粘合剂，可
理解为一个中间代理，假设下有Widget树：
```Dart
Container(//一个容器Widget
    color:Color.blue,//设置容器背景色
    child:Row(//可以讲Widget沿水平方向排列
        children:[
            Image.network('https://www.example.com/1.png'),//显示图片的Widget
            const Text('A'),
        ],
    ),
);
```
**如果 Container 设置了背景色，Container 内部会创建一个新的 ColorBox 来填充背景**，逻辑如下：
```Dart
if(color != null)
    current = ColoredBox(color: color!, child: current);
```
Iamge 内部会通过 RawImage 来渲染图片、Text 内部会通过 RichText 来渲染文本
![Widget_Element_renderTree](media/17315641510404/%E4%B8%89%E6%A0%91%E7%BB%93%E6%9E%84%E5%9B%BE.png)

#### 2.2.4 StatelessWidget
##### 1.简介
它继承自`widget`类，重写了了`creatElement()`方法：
```Dart
@override//检验是否重写——提示下文方法可能是重写的
StatelessElement cratElement()=>StatelessElement(this);
```
`StatelessElement`间接继承自`Element`类，与`StatelessWidget`相对应（作为其配置数据）
`StatelessElement`用于不需要维护状态的场景，它通常在`build`方法中通过嵌套其他widget来构建UI，在构建过程中会递归其嵌套的widget，例如：
```Dart
class Echo extends StatelessWidget{
    const Echo({
    Key?key,
    required this.text,
    this.backgroundColor=Colors.grey,
    }):super(key:key);
    
    final String tex;
    final Color backgroundColor;
    
    @override
    Widegt build(BuildContext){
        return Center(
            child:Container(
                color:backgroundColor,
                child:Text(text),
            )
        );
    }
}
```
widget 的构造函数参数应使用命名参数，命名参数中的必需要传的参数要添加required关键字，这样有利于静态代码分析器进行检查；在继承 widget 时，第一个参数通常应该是Key。另外，如果 widget 需要接收子 widget ，那么child或children参数通常应被放在参数列表的最后。同样是按照惯例， widget 的属性应尽可能的被声明为final，防止被意外改变。
我们可以通过下面的方法来使用：
```Dart
Widget build(BuildContext context){
    return Echo(text:"Hello World");
}
```

##### 2.Context
每一个widget都会对应一个context对象，每一个widget都是widget树上的一个节点
`context`是当前widget树中位置中执行‘相关操作’的一个句柄（handle）
* ps：句柄（Handle）是一个是用来标识对象或者项目的标识符，可以用来描述窗体、文件等值得注意的是句柄不能是常量
例如，它提供了从当前widget开始向上遍历widget树以及按照widget类型查找父级widget的方法，如下：
```Dart
class ContextRoute extends StatelessWidget{
    @override
    Widget build(BuildContext context){
        return Scaffold(
            appBar:AppBar(
                title:Text("Context测试"),
            ),
            body:Container(
                child:Builder(builder:(context){
                     // 在 widget 树中向上查找最近的父级`Scaffold`  widget 
                    Scaffold scaffold = context.findAncestorWidgetOfExactType<Scaffold>();
                    // 直接返回 AppBar的title， 此处实际上是Text("Context测试")
                    return (scaffold.appBar as AppBar).title
                }),
            ),
        );
    }
}
```
#### 2.2.5 StatefulWidget
与`StatelessWidget`相同，`StatefulWidget`也是继承自`widget`类，重写了`creatElement()`方法，不同的是返回的`Element`对象不同，另外`StatefulWidget`类中添加了一个新的接口`createSate()`
`StatefulWidget`类的定义：
```Dart
abstract class StatefulWidget extends Widget{
    const StatefulWidget({Key key}):super(key:key);
    
    @override
    StatefulElement creatElement()=>StatefulElement(this);
    @protected
    State createState();
}
```
* `StatefulElement`间接继承自`Element`类，与`StatefulWidget`相对应（作为其配置数据），`StatefulElement`中可能会多次调用`creatState()`来创建状态(State)对象
* `createState()` 用于创建和 StatefulWidget 相关的状态，它在StatefulWidget 的生命周期中可能会被多次调用

#### 2.2.6 State
##### 1.简介
一个StatefulWidget类会对应一个State类，State表示与其对应的StatefulWidget要维护的状态
State中保存的状态信息可以：
1. 在widget构建时可以被同步读取
2. 在widget生命周期中可以被改变，当State被改变时，可以手动调用其`setState()`方法通知Flutter框架状态发生改变——Flutter框架收到消息后，会重新调用其`build`方法构建widget树，进而更新UI


State中两个常用属性：
* `widget`：表示与该State实例关联的widget实例，又Flutter框架动态设置。*这种关联并非永久的*，因为在应用生命周期，UI树上某一个节点的widget实例在重新构建时可能发生变化，**但State实例只会在第一次插入树中时被创建**，当在重新构建时，如果widget被修改了，Flutter框架会动态设置State.widget为新的widget实例
* `context`：StatefulWidget对应的 BuildContext，作用同StatelessWidget 的BuildContext

##### 2.State生命周期
**理解State生命周期对于flutter开发相当重要**
