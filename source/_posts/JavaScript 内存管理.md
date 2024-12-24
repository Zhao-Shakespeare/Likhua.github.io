# JavaScript内存管理
## JS如何管理内存
JavaScript与很多现代编程语言相同，使用内存自动管理：JS会自动完成垃圾回收
即：我们在程序运行时无需手动分配和释放内存
自动内存管理（垃圾回收）主要通过“标记-清除”完成，分为两个阶段：
1. 标记阶段：垃圾收集器从根对象开始，标记所有可到达或可访问的对象
2. 清除阶段：任何未标记（即可无法访问）的对象都被视为“垃圾”，并且其内存将被释放

自动的内存管理无法解决所有场景下的内存问题，在某些特殊情况下就会导致内存泄漏的出现
## 内存泄露
对于内存泄漏，我们需要知道内存泄露和内存溢出的差异性
* 内存溢出：程序运行过程中需要使用的内存大于系统能够提供的内存，即：系统内存不足
* 内存泄露：当一块内存（通常是变量）未被释放（垃圾回收），同时我们也无法访问到它时
### 具体的内存泄露问题
#### 1.未清理的定时器或回调
* 场景：使用`setInterval`或`setTimeout`，但在组件小会或不再需要时没有清理
* 结果：定时器依旧存在，引用被保留，导致无法释放内存

实例如下：
```JavaScript
function startTimer(){
    setInterval(()=>{
        console.log('xxx');
    },1000);   
}
//如果调用此函数后不清理定时器，这会造成内存泄漏
```
修复实例如下：
```JavaScript
const timer=setInterval(()=>{
    console.log("Timer running...");
},1000);
clearInterval(timer);//组件销毁时清理
```
#### 2.DOM引用未释放
* 场景：保留对已移除DOM元素的引用
* 结果：虽然DOM节点从页面上被删除，但JavaScript中仍有对它的引用，导致内存泄露
实例如下：
```JavaScript
let element = document.getElementById('leak');
document.body.removeChild(element);
//仍然引用element，导致内存无法释放
```
修复实例如下：
```JavaScript
element = null;
```
#### 3.闭包中的多余引用
* 场景：闭包内的变量保留了对外部对象的引用，导致对象无法被垃圾回收
* 结果：长时间的引用链阻止了内存的释放
实例如下：
```JavaScript
function creatClosure(){
    const largeObject = new Array(1000).fill('leak');
    return function(){
        console.log(largeObject);
    };
}
const closure = createClosure();
//即使closure不再使用，largeObject依然存在
```
修复实例如下：
```JavaScript
function creatClosure(){
    let largeObject = new Array(1000).fill('leak');
    return function(){
        console.log(largeObject);
        largeObject = null;//主动引用清除
    }
}
```
#### 4.全局变量或未声明变量
* 场景：未使用`var`，`let`或`const`定义变量，导致变量挂载在全局作用域
* 结果：全局变量生命周期与页面一致，无法被垃圾回收
实例如下：
```JavaScript
function leak(){
    leakVariable='I am a leak';//隐式全局变量
}
leak();
```
修复实例如下：
```JavaScript
function noLeak(){
    let localVariable="I am safe";//使用局部作用域变量
}
```
#### 5.事件监听未清理
* 场景：在DOM元素上绑定了事件监听器，但没有在元素销毁时移除
* 结果：监听器仍然存在，组织DOM元素被回收
实例如下：
```JavaScript
const button = document.getElementById('myButton');
button.addEventListener('click',()=>console.log('点击！'));
document.body.removeChild(button);
//内存泄露：button和监听器仍被引用
```
修复实例如下：
```JavaScript
const button = document.getElementById('myButton');
const handler = () => console.log('点击！');
button.addEventListener('click',handler);
button.removeEventListener('click',handler);//组件销毁时移除
document.body.removeChild(button);
```
#### 6.忘记清理Map/Set中的键或值
* 场景：`Map`或`Set`中的键/值对象未手动移除
* 结果：即使这些对象不再需要，也会因其被引用而无法回收
实例如下：
```JavaScript
const map = new Map();
const obj = {key:'value'};
map.set(obj,'data');
//即使obj不再使用，map仍然引用它
```
修复实例如下：
```JavaScript
map.delete(obj);//手动清除不需要的键
```
#### 7.闭环引用
* 场景：两个对象互相引用，导致垃圾回收无法判断它们是否可释放
* 结果：循环引用造成内存泄露
实例如下：
```JavaScript
function ClicularReference(){
    const obj1={};
    const obj2={};
    obj1.ref=obj2;
    boj2.ref=obj1;
}
```
修复实例如下：
```JavaScript
//如果可能，避免互相引用，或通过WeakMap/WeakSet管理对象
const obj1= new WeakMap();
const obj2={};
obj1.set(obj2,'value');
```

