---
title: Uniapp
date: 2024-11-13 11:21:20
tags: React Native
---
# uniapp
前提熟悉HTML、CSS、JavaScript
传统的html5只有一端支持——浏览器。但是uniapp可跨多端，虽然仍然属于前端，但是还是与传统的h5不同
如果对h5有一定了解，可以较快的入门uniapp
## 网络模型的变化
以前的网页大多是b/s，服务端代码混合在页面里；
现在还c/s，前后端分离，即通过 js api（类似于ajax的uni.request）获取json数据，将数据绑定在页面上渲染
## 文件类型变化
以前是.html文件，开发也是html，运行也是html
现在是.vue文件，开发是vue，编译后，运行时已经变成了js文件
现代前端开发，很少直接使用html，基本都是开发、编译、运行——所以uni-app有编译器、运行时的概念
## 文件内代码架构的变化
以前一个html大节点，里面有script和style节点
现在template是一级节点，用于写tag组件，script和style是并列的一级节点，也就是有3个一级节点
以前：
```html
<!DOCYTYOE html>
<html>
    <head>
        <meta charset='utf-8'/>
        <title></title>
        <script type='text/javascript'>
        
        </script>
        <script type='text/css'>
        
        </script>
    </head>
    <body>
    
    </body>
</html>
```
vue单文件组件规范：
```html
<template>
    <view>
        注意必须有一个view，并且只能拥有一个根view，所有内容写在view下面
    </view>
</template>
<script>
    export default{
    
    }
</script>
<style>

</style>
```
## 外部文件引用方式变化
以前通过script src、link href引入外部的js和css；
现在是es6的写法，通过import引入外部的js模块（不是文件）或css
以前：
```html
<script src="js/jquery-1.10.2.js" type="text/javascript"></script>
<link href="css/bootstrap.css" rel="stylesheet" type="text/css">
```
现在：
### js要require进来，变成了对象
在hello uni-app的common目录有一个工具类`util.js`，可以在hello uni-app中搜索这个例子查看
```
<script>
var util = require('../../../common/util.js');//require这个js模块
var formatedPlayTime = util.formatTime(playTime);//调用js模块方法
<script/>
```
而在这个`util.js`里，要把之前的function封装为对象的方法
```JavaScript
function formatTime(time){
    return time;//省略了逻辑
}

module.exports= {
    formatTime : formatTime
}
```
也有更高级的用法:
```JavaScript
var dateUtils=require('../../../common/util.js').dataUtils;
//直接使用js模块的属性，在hello uni-app有示例
```