---
title: ...运算符
date: 2024-11-12 19:21:00
tags: JavaScript
---
# JS改变代码的三个点——...运算符
`...`展开运算符/剩余参数运算符，具体含义取决于它的使用场景
## 场景一：展开运算符——让数据“散开”重生
### 1.在数组中使用
#### 创建数组副本
你可以使用展开运算符来创建一个数组的浅拷贝
```JavaScript
const arr = [1,2,3];
const cpoy=[...arr];//浅拷贝原数组
```
#### 合并数组
通过展开多个数组，你可以轻松合并它们
```JavaScript
const arr1 = [1,2,3];
const arr2 = [4,5,6];
const combined = [...arr1,arr2];//结果是[1,2,3,4,5,6]
```
#### 添加新元素
你可以在已有数组的基础上添加新元素
```JavaScript
const numbers = [1,2,3];
const moreNumbers = [...numbers,4,5];//结果是[1,2,3,4,5]
```
#### 函数调用时展开参数
当你有一个数组，并且希望将其元素作为单独的参数传递给函数时，可以使用展开运算符
```JavaScript
function sum(x,y,z){
    return x+y+z;
}
const args = [1,2,3];
console.log(...args);//输出6
```
###  2.在字符串中使用
#### 将字符串转换为字符数组
可以直接将字符串展开成字符数组
```JavaScript
const str = 'hello';
const chars = [...str];//['h','e','l','l','o']
```
### 3.处理迭代对象
#### Set和Mep
对于Set和Map这样的集合类型，可以使用展开运算符来创建副本或者与其他集合进行合并
```JavaScript
const set1 = new Set([1,2,3]);
const set2 = new Set([...set1],4,5);//创建一个包含新元素的副本
const map1 = new Map([['key1','value1']]);
const map2 = new Map([...map1,['key2','value2']]);//合并两个Map
```
## 场景二：剩余运算符
这个功能在函数的定义中非常有用，特别是当你不知道或者不想限制传递给函数的参数数量时。剩余参数使用三个点`...`表示，并且总是放在参数列表的最后
### 1.与普通参数结合使用
你可以在函数定义中同时使用固定参数和剩余参数，这使得你的函数更加灵活
```JavaScript
function logFirstAndRest(first,...rest){
    console.log('First:',first);
    console.log('Rest:',rest);
}
logFirstAndRest('hello','world','!');
//输出
//First:hello
//Rest:['world','!']
```
### 2.创建可变参数函数
如果你有一个函数，它的参数数量可能变化，那么你可以使用剩余参数来简化代码
```JavaScript
function sum(...numbers){
    return numbers.reduce((total,num)=>total+num,0);
}
console.log(sum(1,2,3));//输出 6
console.log(sum(1,2,3,4,5));//输出 15
```
### 3.处理回调函数中的参数
当编写接受回调函数作为参数的高阶函数时，剩余参数可以帮助你处理哪些可能会传递给回调的任意数量的参数
```JavaScript
function higerOrderFunction(callback,...args){
    callback(...args);
}
higherOrderFunction((a,b,c)=>console.log(a,b,c),1,2,3);
//输出 1 2 3
```
1. 参数传入：将`(a,b,c)=>console.log(a,b,c)`匿名函数作为参数传给`callback`函数，剩余的`1 2 3`，通过剩余运算符都传给`args`数组，最后`args`又作为参数传给`callback`
2. 结果：输出 1 2 4

### 4.解析构置