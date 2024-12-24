---
title: Flutter
date: 2024-07-2 10:2:32
tags: Flutter&Dart
---
**《Flutter跨平台开发与实战》这本书非常荒谬，非常不适合小白新手入门**
## 第一章 Flutter概述
Flutter是Google开源的应用开发框架，仅通过一套代码库，就能构建精美的、原生平台编译的多平台应用。
Flutter、React Native(包括React)等跨平台语言均支持一套代码适配各个平台，但是目前各个跨平台开发语言的热度有所不同，其中热度尤为高涨的当属Flutter了。
对比Flutter以及React Native这两个跨平台移动应用开发框架，各有优劣，下面对于他们的性能特性等进行比较对比。
### 1.1 Flutter与React Native
**Flutter：**
优点：
* 性能：Flutter使用的是Dart语言，有着自己的渲染引擎，能够提供更加接近原生应用的性能，能够制作包括流畅的动画以及高度定制的UI（并且由于更加接近底层，所以编译效率较高）
* 开发效率：Flutter支持热重载，能够快速查看代码修改后的效果，加快开发速度
* 庞大的社区：由于是由Google推出的，具有极大的体量以及使用群体，从而有着丰富的插件和扩展
缺点：
* 学习效率：对于主流的JavaScript、C等语言有着一定差距，需要学习Dart语言进行开发，相对RN需要的学习投入相对较多
* 生态系统：由于Flutter的诞生相对于RN来说较为年轻，所以在一些方面可能缺乏成熟的的方案以及解决经验

**React Native**
优点：
* 生态系统：诞生周期相对较长，因此第三方库、解决办法、社区环境相对成熟
* 灵活性：使用JavaScript进行开发，对于前端开发者来说门槛较低
缺点：
* 性能：由于JS的机制以及跨平台框架的限制，性能上相将于原生开发有一定劣势
* 学习效率：JS生态之中有着较为庞大的工具以及库，需要更多时间进行学习了解

**风口：对于Flutter来说，今年以及明年都将是一个风口，华为的HarmonyOS能够兼容Flutter进行软件开发，而今年以及明年恰好是鸿蒙开发者需求增大的一年，因此抓住这个风口，把握住机会尤为重要**
### 1.2 Flutter特性
1. 跨平台开发

支持在macOS、Windows、Linux、Android、iOS以及谷歌公司的Fuchsia操作系统上运行。同时，Flutter可以真正做到一套代码同时运行在Android、iOS和Web平台上，避免过高的开发和维护成本，节约资源。

2. 符合不同平台的用户体验

Flutter内置的Material和Cupertino风格的组件，为开发者开发Android和iOS平台风格的应用提供了便捷。

3. 响应式框架

使用Flutter的响应式框架和一系列基础组件，可以轻松地完成用户界面（UI）的构建。同时，功能强大且灵活的API可以帮助开发者解决复杂的UI构建问题。

4. 跨平台渲染引擎

与Hybird App、React Native跨平台技术采用的方案不同，Flutter使用Skia作为其二维渲染引擎，因此它不需要像React Native那样在JavaScript和Native之间通信，从而减少了性能开销。

5. 支持本地访问和插件

通过Flutter提供的插件，开发者可以访问原生平台的API，如蓝牙、相机和Wi-Fi等。同时，Flutter还可以复用Java、Swift或ObjC代码，访问原生Android和iOS系统的功能。

6. 高性能

Flutter采用GPU渲染技术，所以性能较强。使用Flutter编写的应用运行画面基本可以达到60帧/秒，因此使用Flutter开发的应用几乎可以媲美原生应用的性能。

7. 使用Dart进行应用开发

Flutter使用Dart进行应用开发。与传统的JavaScript相比，Dart在即时（Just In Time，JIT）编译模式下的速度与JavaScript基本持平，但是在静态（Ahead Of Time，AOT）编译模式下运行时，Dart的性能远高于JavaScript。
并且，Flutter使用Dart进行应用开发。与传统的JavaScript相比，Dart在即时（Just In Time，JIT）编译模式下的速度与JavaScript基本持平，但是在静态（Ahead Of Time，AOT）编译模式下运行时，Dart的性能远高于JavaScript。

### 1.3 Flutter框架
Flutter与原生Andriod以及IOS系统一样，Flutter框架也是分层的结构，每层都建立在前一层的基础上，并且上层比下层的使用频率更高
![Flutter](assets/Flutter.png)
由图可知，Flutter框架自上而下分为Embedder层、Engine层以及Framework层。
Embedder是操作系统适配层，实现了渲染Surface设置、线程设置，以及平台插件等平台相关特性的适配；
Engine层负责徒刑绘制、文字排版，Engine层具有独立虚拟机，由他的存在，Flutter程序才能运行在不同的平台上，实现跨平台运行；
Framework层是使用Dart编写的一套基础视图库，包括了动画、图形绘制和手势识别，是使用频率最高的一层。

## 第二章 Dart基础
### 2.1 Hello World
与大多数程序语言相同，Dart将`main()`作为程序的入口，相较于Java而言，Dart简单的多。
让我们先编写一个简单的Dart
```dart
void main(){
    print('Hello World!!!');
}
```
然后打开终端输入`dart 文件名.dart`然后控制台输出"Hello World!!!"
### 2.2 Dart基础知识
#### 2.2.1 变量与常量
Dart中，变量可以使用`var` `object` `dynamic`关键字来声明，如下所示：
```dart
var name='ZhaoShouheng';
```
计算机中，变量仅存储对象的引用，因此我们可以认为这里name存储了一个String类型的对象引用，Zhaoshouheng是String类型对象的值。
如果不限定变量的类型，那么可以将变量指定为对象类型或动态类型，如下所示：
```dart
dynamic name='Zhaoshouheng';
```
还可以通过显式声明的方式来定义变量，如下所示：
```dart
String name='Zhaoshouheng';
```
在Dart中，一切皆为对象，因此未初始化的变量默认值是null，如下所示：
```dart
int lintCount;
assert(lineCount == null);//错误
```
Dart中，声明常量需要使用final或const关键字。final关键字修饰的变量（简称final变量）的值只能被设置一次，const关键字修饰的变量（简称const变量）在编译时就已经固定，实例变量可以时final变量不能时const变量。
final和const都用来声明常量，区别在于：
* const声明的常量的值需要在编译期间就能确定，也就是说不能够使用包含变量的表达式来给变量赋值；
* final关键字修饰的变量可以使用包含变量的表达式来给他赋值。
创建并设置一下final变量如下所示：
```dart
final name='Zhaoshouheng';
final String nickname='Cxk';
name='jack';//报错
```
如果需要在编译时就固定变量的值，可以使用const变量，如下所示：
```dart
const bar=100000;
const double atm = 1.0123 * bar;
```
const关键字不仅可以用于声明常量，还可以用来创建常量值，以及声明创建常量值的构造函数，如下所示：
```dart
var foo=const [];
final bar=const [];
const baz=[];
```
#### 2.2.2 内置数据类型
Dart常用的数据类型有八种，分别是：Number、String、Bool、List、Set、Map、Rune和Symbol
##### 1.Number类型
Dart中的Number类型分为整型和浮点型两种，分别使用int和double进行声明
Number类型可以进行基本的加减乘除运算以及位移操作，，还提供了字符串和数字相互转换的方法，如下所示：
```dart
var one=int.parse('1');//String类型转换为int类型
assert(one==1);//Number

var onePointOne=double.parse('1.1');//String类型转换为double类型
assert(onePointOne==1.1);

String oneAsString=1.toString();//int类型转换成String类型
assert(oneAsString=='1');

String piAsString=3.14159.toStringAsFixed(2);//double类型转换为String类型
assert(piAsString=='3.14');
```
从Dart2.1开始，使用num声明的变量如果初始化是int类型，那么它可以在初始化后转换成double类型，反之不行。如下所示：
```dart
num a=10;
a=3.14;//可以
a=20;//报错
```
##### 2.String类型
Dart的String类型是一组UTF-16的单元序列，通过单引号或者双引号进行声明，如下所示：
```dart
num a=10;
var s1='hello world';
var s2="hello world";
```
可以使用3个单引号或者3个双引号来定义多行的String类型，字符串会保持原样输出，如下所示：
```dart
var s1='''
hello
world
''';
var s2="""hello
world""";
```
可以为字符串添加一个r前缀，来创建原始raw字符串，如下所示：
```dart
var s=r"In a raw string,even \n isn't special";
```
##### 3.Bool类型
Dart的Bool类型只有true和false两个值，并且Bool值是编译时的常量。因为Dart是一个强类型检查的语言，所以只有当Bool类型的值时ture时，其结果才是true，通俗的说，在其他语言中，0是false，大于0即为true，这样的情况在Dart中并不支持。
Dart的强类型检查并不代表不能够使用if/assert，例如我们可以在Debug模式下，通过assert断言函数来判断Bool值，如下所示：
```dart
var fullName='';
assert(fullName.isEmpty);//检查空字符串

var hitPoints=0;
assert(hitPoints<=0);//检查值是否为0
```
##### 4.List类型
在Dart中，List代表列表，与数组的概念是相同的，
在Dart中，List与JavaScript中的Array类型是一样的，如下所示：
```dart
var list=[1,2,3];//创建列表
var list2=new list()//通过构造函数的方式创建列表
var list3=const[1,2,3];//创建一个不可变的列表
```
与数组的概念相同，List的索引也从0开始，第一个元素的索引是0，最后一个元素的索引是`list.length-1`。访问List长度和元素与JS中的用法一样，如下图所示：
```dart
var list=[1,2,3,4,5,6];
print(list.length);//输出6
print(list[list.length-1]);//输出6
```
##### 5.Set类型
在Dart中，Set用来表示集合。
使用Set定义的集合，它的对象不需要按照特定的规则排列，如下所示：
```dart
var hw={'hello','world'};
```
对集合的访问和操作都是通过对象来实现的，因此集合中不能有重复的对象。要创建一个空集合，可以使用带有类型参数的{},或者将{}赋值给Set类型的变量，如下所示：
```dart
var names=<String>{};//创建一个空集合
```
除外，Dart的集合还提供了add() addAll()等常用方法。
```dart
var elements=<String>{};
elements.add('hello');
elements.addAll(hw);
```
##### 6.Map类型
在Dart中，Map以键值对(key-value)的形式进行存储。key和value可以是任何类型的对象，一个Map中，key只能出现一次，但是value确可以出现多次，如下所示：
```dart
var gifts={
    'first':'cat',
    'second':'book',
    'third':'toy'
};
```
也可以通过Map的构造函数来创建，如下所示：
```dart
var gifts = Map();
gifts['first']='cat';
gifts['second']='book';
gifts['third']='toy';
```
如果想要创建一个不可变的Map对象，只需要在Map对象前添加const关键字即可，如下所示：
```dart
var gifts=const{
    'first':'cat',
    'second':'book',
    'xxx':'xxxx'
}
```
##### 7.Rune类型
在Dart中，Rune类型用来表示UTF-32字符串，并能够将文字转换成符号表情或者代表特定含义的文字。如下所示：
```dart
var clapping = '\u{1f44f}';
print(clapping);
print(clapping.codeUnits);
print(clapping.runes.toList());

Runes input = new Runes('\u2665  \u{1f605}  \u{1f60e}  \u{1f47b}  \u{1f596}  \u{1f44d}');
print(new String.fromCharCodes(input));
```
执行上面的代码，运行结果如下图所示：
```
□
[55357, 56399]
[128079]
♥  □  □  □  □  □
```
在日常编程中，如果我们需要处理包含多字节字符的文本，那么`rune`类型的使用频率可能会相对较高。然而，在大多数情况下，Dart开发者可能不需要直接与`rune`类型打交道，因为Dart的`String`类型已经提供了对Unicode字符的内置支持。
`rune`类型的使用频率取决于你的具体需求。如果你经常需要处理复杂的文本数据，特别是包含多字节字符的数据，那么`rune`类型可能会成为我们常用的一个工具。然而，对于大多数简单的文本处理任务，我们可能只需要使用`String`类型即可。
##### 8.Symbol类型
Symbol表示在Dart程序中声明的运算符或标识符。在Dart开发中，几乎很少用的Symbol类型，除非需要按照名称引用标识符的API，因为代码经过编译之后标识符的名称会发生改变，但是标识符的符号不会发生改变，如下所示：
```dart
print(#radix);//输出Symbol("radix")
print(#bar);//输出Symbol("bar")
```
#### 2.3 函数
Dart是一门面向对象的编程语言，所以函数也是对象，而函数属于Function类型，这意味着Dart可以将函数作为变量传递给另一个函数，也可以吧Dart类的实例当作方法来调用，如下所示：
```dart
var_nobleGases = {};
bool isNoble(int atomicNumber){
    return_nobleGases[atomicNumber]!=null;}
```
也可以使用箭头函数进行简化
```dart
bool isNoble(int atomicNumber)=>_nobleGases[atomicNumber]!=null;
```
##### 2.3.1 main()
任何一个应用都必须有一个入口函数，Dart应用的main()就是它的入口函数。
main()的返回值为空，参数为一个可选的`List<String>`组数。
Flutter应用的main()如下所示：
```dart
void main()=>runApp(new Myapp());
```
##### 2.3.2 函数参数
函数的参数类型有两种，分别是可选参数和必传参数
通常，必传参数会显示在参数列表的前面，后面再跟上可选参数。可选参数使用命名参数或者位置参数进行传值。

Dart中的可选参数分为可选命名参数和可选位置参数两种
可选命名参数的参数部分使用{}包裹，如下所示：
```dart
void param(int num,{String name,int range}){//可选命名参数
}
param(10,range:1);
```
可选位置参数的参数部分使用[]包裹，如下所示：
```dart
void param(int num,[String where,int range]){//可选位置参数
}
param(10,'shenzhen',10);
```
除了可选参数外，有的函数的参数是必传的。
在Dart中，必传参数需要使用@required修饰符，如下所示：
```dart
void enableFlags({bool bold,bool hidden,@required bool circle}){//必传参数
}
enableFlags(bold:true,circle:true);
```
也可以给函数的参数设置默认值，如下所示：
```dart
void say(String from,[String device="andriod",String id]){ }
```
##### 2.3.3 返回值
几乎所有的函数都会有一个返回值，如果没有明确指定返回值，那么函数体会隐式地添加一个"ruturn null;"语句，如下所示：
```dart
foo(){}
assert(foo() == null);
print(foo() == null);
```
运行上面的代码，控制台会返回正确的信息
##### 2.3.4 匿名函数
与其他编程语言相同，Dart也支持匿名函数。
匿名函数通常以lambda表达式或者闭包的形式存在，一个宁明函数可以有0个或者多个参数，参数之间使用逗号分隔，匿名函数的格式如下所示：
```dart
([[Type] paragm1[,...]]){
    //函数体
}；
```
下面是一个包含无参数类型item的匿名函数。
```dart
var list=['apples','bananas','oranges'];
list.forEach((item){
    print('${list.indexOf(item)}:$item');
})
```
上面的例子中，list数组里的每个元素都会调用这个匿名函数来输出元素位置和对应位置的值。
输出结果如下所示：
```
null
0:apples
1:bananas
2:oranges
```
#### 2.4 Dart运算符
大家知道，计算机程序的最小单位是表达式，表达式主要由操作数和运算符组成。操作数可以是变量、常量、类、数组和方法，甚至还可以是表达式，而运算符则用来执行程序代码的相关运算。
Dart支持各种类型的运算符，并且部分运算符还支持重载操作。
##### 2.4.1 算数运算符
Dart支持的算数运算符有+、—、*、/、~/、-expr和%等
* +：加法
* -：减法
* *：乘法
* /：除法
* ~/：除法，取整
* expr：取负
* %：取余
除此之外，Dart还支持自增和自减运算符
* ++var：先执行自执行操作
* var++：先使用值在执行自增操作
* --var：先执行自减操作
* var--：先使用值再执行自减操作

##### 2.4.2 关系运算符
关系运算符是用来表示两个操作数或表达式关系的运算符，dart的关系运算符主要由==、!=、>、<、>=、>=构成，如下所示：
##### 2.4.3 类型判定运算符

Dart的类型判定运算符由as、is和is!运算符构成，主要用于在运行时的进行类型检查，如下所示：
* as：判断是否属于某种类型
* is：对象具有指定的类型，返回true
* is!：对象具有指定的类型，返回false
其中，使用as运算符可以将对象强制转换成指定类型，如下所示：
```dart
var a = 123;
print((a as num) is num);
```
##### 2.4.4 位运算符
在Dart中，运算符主要有&、~、|、^、<<、>>构成。
如下所示：
```dart
final value = 0x22;
final bitmask = 0x0f;
print((value&bitmask)==0x02);//按位与
print((value~bitmask)==0x20);//按位取反
print((value|bitmask)==0x2f);//按位或
print((value^bitmask)==0x2d);//按位异或
print((value<<4)==0x220);//按位左移
print((value>>4)==0x02);//按位右移
```
##### 2.4.5 逻辑运算符
Dart的逻辑运算符由&&、||、!构成，如下所示：
```dart
var a=12;
print(a>10&&a<11);//false
print(a>10||a<11);//true
print(!(a>10));//false
```
##### 2.4.6 赋值运算符
在Dart中，最常见的赋值运算符是=。初次之外，赋值运算符还包括复合运算符，常见的复合运算符包括-=、/=、%=、>>=、^=、*=、~/=、<<=、&=、|=
如下所示：
```dart
var nullVar;
var intVar=12;
nullVar??=inVar;
print(nullVar);
var strVar=intVar>10?"a":"b";
print(strVar);
```
##### 2.4.7 条件表达式
Dart提供了三目表达式和??运算符来代替if-else条件表达式，如下所示：
```dart
condition ? expr1 : expr2//三目运算符
expr1 ?? expr2//??运算符
```
通常，如果判定条件是Bool值，可以考虑使用?:运算符，如果判定是否为null，则可以考虑使用??运算符。
##### 2.4.8 级联运算符
Dart中的级联运算符用..表示，级联运算符可以对同一个对象进行一系列操作。
级联运算符不仅可以调用函数，还可以访问同一对象上的字段属性。级联运算符可以简化语法，如下所示：
```dart
querySelector('#confirm')//获取对象
..text='确定';
..classes.add('important')
..onClick.listen((e)=>window.alert('确定'));
```
上面的例子里，第一句用`querySelector()`，该函数会返回获取的对象，然后为该对象设置文本值和执行导入，最后为该对象添加一个点击监听事件。如果不使用级联运算符的话，上面的实例可以写为：
```dart
var button=querySelector('#confirm');
button.text='Confirm';
button.classes.add('important');
button.onClick.listen((e)=>window.alert('Confirmed!'));
```
并且级联运算符还支持嵌套，如下所示：
```dart
final addressBook=(AddressBookBuilder()
..name='jeeny';
..phone=(PhoneNumberBuilder()
    ..number='123-456-7890'
    ..lable='home')
    .build())
.build();
```
**《Flutter跨平台开发与实战》这本书非常荒谬，非常不适合小白新手入门**