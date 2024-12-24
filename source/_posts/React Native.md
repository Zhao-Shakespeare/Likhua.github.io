---
title: React Native
date: 2024-06-21 9:32:32
tags: React Native
---
# React Native
## 快速入门
### 简介：
学习React Native的大前提是对JavaScript的基础知识有了一定了解，在不具备开发环境的设备中，我们可以使用Snack Player的沙盒环境继续模拟开发。
### 函数式组件与Class组件：
#### 函数式组件：
函数式组件是接收`props`作为参数并返回React元素的纯函数，没有状态（state），也没有实例（instance）。下面是一个简单的例子：
```JavaScript
function FunCom(props){
    return(
        <div>
        {props.message}
        </div>
    );
}
```
##### 优缺点：
*优点：*
1. 更简洁：函数式组件不需要继承`React.Component`，编写起来更加的简洁
2. 无需`this`：避免了`this`关键字相关的问题
3. 复用性及组合性好：函数式组件更易于进行组合复用
4. 性能更好：函数时组件在渲染时开销更小
5. 支持使用Hooks：可以使用React Hooks来实现状态管理以及副作用操作
*缺点：*
1. 已被新版本解决——有限的状态管理：字React 16.8起，引入Hooks，使得函数时组件也可以管理状态和处理副作用。

#### Class组件：
类组件（Class组件）是使用ES6类来定义的组件，继承自`React.Component`,可以包含状态(state)以及生命周期方法(lifecycle methods)，下面是一个简单的例子：
```JavaScript
class ClassCom extends React.Component{
    constructor(props){
        super(props);
        this.state={
            message:"Hello World!"
        };
    }
    render(){
        return(
            <div>
                {this.state.message}
            </div>
        )
    }
}
```
*优点：*

1. 状态管理：类组件可以有自己的状态(state)和生命周期方法
2. 生命周期方法：提供了许多生命周期方法，方便执行各种操作

*缺点：*

1. 更繁琐：较于函数式组件，类组件代码更加繁琐
2. `this`关键字：可能由于`this`关键字导致一些问题
3. 性能开销：在渲染创造示例时，可能带来额外的性能开销
4. 不支持Hooks：无法使用React Hooks来进行状态管理和副作用操作(可以通过高阶组件实现)

*除非有特殊原因需要使用类组件（如某些生命周期方法的依赖），否则推荐优先使用函数式组件*

## React基础
React Native的基础是React，对于React的学习建议参考程墨的《深入浅出React和Redux》，但是这本书里缺少Hooks的相关知识，因此对于Hooks部分可以[阅读React的官方Hooks文档](https://zh-hans.react.dev/reference/react/hooks)
这里不会对React基础做出特别详细的解释说明，还是推荐大家阅读相关书籍
## 处理文本输入
在React Native中，TextInput是一个允许用户输入的基础组件。
属性：
`onChangeText`：此属性接受一个函数，而此函数会在文本变化时被调用。
`onSubmitEditing`：会在文本被提交后（用户按下软键盘上的提交键）调用。
## 使用滚动视图
`ScrollView`是一个通用的可滚动的容器，你可以在其中放入多个组件和视图，而且这些组件并不需要是同类型的。`ScrollView`不仅可以垂直滚动，还能水平滚动（使用`horizontal`属性来设置）。
`ScrollView`适合用来显示数量不多的滚动元素，放置在`ScrollView`中的<u>所有组件都会被渲染</u>，记住是<u>所有组件</u>，如果显示较长的滚动列表建议使用`FastList`组件，功能相同，性能更强。
`ScrollView`使用`pagingEnabled`属性来允许滑动手势的分页。
## 使用长列表
`FastList`组件用于显示一个垂直的滚动列表，其中的元素之间结构近似而仅数据不同。它更适用于长列表数据，元素个数可以增删，并不立即渲染所有元素，而是优先渲染屏幕上可见的元素。
两个必须的属性：
`data`：是列表的数据源
`renderItem`：从数据源中逐个解析数据然后返回一个设定好格式的组件来渲染。