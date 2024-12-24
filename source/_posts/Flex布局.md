---
title: Flex布局
date: 2024-06-23 11:09:18
tags: Flex布局
comments: true
---
# Flex布局
Flex布局（弹性盒子模型），通过这个Flex模型，可以较为轻松地创建自适应于浏览器窗口的“流动布局”以及自适应字体大小的弹性布局，使得响应式布局的实现更加容易。

属性：
1. `flex-grow`:定义子元素的放大比例
2. `flex-shrink`:定义子元素的缩小比例
3. `flex-basis`:定义子元素的宽度
4. `flex`:`flex-grow`、`flex-shrink`、`flex-basis`的复合属性
5. `flex-firection`:定义子元素的排列方向
6. `flex-wrap`:定义子元素是单行显示/多行显示
7. `flex-flow`:`flex-firection`、`flex-wrap`的复合属性
8. `justify-content`:定义子元素在“横轴”上的对齐方式
9. `align-items`:定义子元素在“纵轴”上的堆砌方式

*我们只需要重点掌握flex、flex-flow、order、justify-content、align-items这5个属性就可以了，可以减少记忆负担*

在使用弹性盒子模型之前，必须为父元素定义`display:flex`，如此父元素才具有弹性盒子模型的特点。
## 放大比例：`flex-grow`
CSS3中可以使用`flex-grow`来定义弹性盒子内部子元素的放大比例。
形如：
```CSS3
flex-grow:数值;
```
`flex-grow`属性取之是一个数值，默认为0，取值为0时，表示不索取副元素的剩余空间，当取值大于0时，表示索取父元素的剩余空间（即子元素放大）。取值越大，索取越多。
**特别注意，在使用`flex-grow`时，一般是不需要对弹性盒子内部的子元素定义宽度或高度的，否则会影响flex容器的分配比例**
## 缩小比例：`flex-shrink`
CSS3中，`flex-shrink`属性用于定义弹性盒子内部子元素的缩小比例——当所有子元素宽度之和大黄鱼父元素的宽度时，子元素如何缩小自己的宽度。
形如：
```CSS3
flex-shrink:数值；
```
`flex-shrink`:默认取值是一个数值，默认值为1。取值为0时，表示子元素不缩小；取值大于1时，表示子元素按一定的比例缩小。取值越大，缩的越小。

**注：只有当所有子元素宽度之和小于弹性盒子的宽度时，flex-grow才会生效，而此时flex-shrink无效；只有当所有子元素宽度之和大于弹性盒子的宽度时，flex-shrink才会生效，而此时flex-grow无效。也就是说，flex-grow和flex-shrink是互斥的，不可能同时生效**
在我们实际开发过程中，更多时候会使用`flex-grow`，很少会使用`flex-shrink`
## 元素宽度：`flex-basis`
CSS3中，我们可以定义弹性盒子内部的子元素在分配空间之前，该子元素所占的空间大小。浏览器会根据这个属性来计算父元素是否有多余空间。

ps：说白了`flex-basis`就是`width`的替代品，都用来定义子元素的宽度。在弹性盒子中，`flex-basis`的语义会比`width`更好。
形如：
```CSS3
flex-basis:取值;
```
`flex-basis`有两个属性值:
1. 'auto':该子元素的宽度是根据内容多少来定的；
2. '长度值':单位为px，em以及百分比等。

## 复合属性：flex
CSS3中，可以使用`flex`属性来同时设置：`flex-grow``flex-shrink` `flex-basis`这三个属性，简而言之`flex`属性就是一个简写形式，是一个“语法糖”。
形如：
```CSS3
flex:grow shrink basis;
```
'grow':是`flex-grow`的取值
'shrink':是`flex-shrink`的取值
'basis':是`flex-basis`的取值
flex属性的默认值为“0 1 auto”
**在实际开发中，优先使用flex属性，而不是单独写flex-grow、flex-shrink、flex-basis这3个属性**
## 排列方向：`flex-firection`
CSS3中，可以使用`flex-direction`属性来定义弹性盒子内部“子元素”的排列方向——即定义子元素是横着排还是竖着排
形如：
```CSS3
flex-direction:取值;
```
`flex-direction`属性的取值有四个：
1. 'row':横向排序（默认值）
2. 'row-reverse':横向反向排列
3. 'column':纵向排列
4. 'colum-reverse':纵向反向排列

## 多行显示：`flex-wrap`
CSS3中，可以使用`flex-warp`属性来定义弹性盒子内部“子元素”是单行显示还是多行显示。
语法：
```CSS3
flex-warp:取值;
```
`flex-wrap`常见取值有三个：
1. 'nowrap':单行显示（默认值）
2. 'wrap':多行显示，也就是换行显示
3. 'wrap-reverse':多行显示，但是反向

## 复合属性：`flex-flow`
CSS3中，可以使用`flex-flow`属性来同时设置`flex-direction``flex-wrap`这两个属性。
形如：
```CSS3
flex-flow:direction wrap;
```
参数direction是flex-direction的取值，参数wrap是flex-wrap的取值。因此，flex-flow属性的默认值"row nowrap"。
## 排列顺序：`order`
CSS3中，我们可以使用order属性来定义弹性盒子内部“子元素”的排列顺序
形如：
```CSS3
order:整数;
```
`order`属性取值是一个正整数，即1、2、3等。
## 水平对齐：`justify-content`
CSS3中，使用`justify-content`属性来定义弹性盒子内部子元素在“横轴”上的对齐方式。
形如：
```CSS3
justify-content:取值;
```
`justify-content`取值很多，常见属性如下：
1. flex-start:所有子元素在左边（默认值）
2. center:所有子元素在中间
3. flex-end:所有子元素在右边
4. space-between:所有子元素平均分布 
5. space-around:所有子元素平均分布，但两边留有一定间距

## 垂直对齐：`align-items`
CSS3中，可以使用`align-items`属性来定义弹性盒子内部子元素在“纵轴”上的对齐方式
形如：
```CSS3
align-items:取值;
```
`align-items`属性取值很多，常见属性如下：
1. flex-start:所有子元素在上边（默认值）
2. center:所有子元素在中部
3. flex-end:所有子元素在下部
4. baseline:所有子元素在父元素的基线上
5. stretch:拉伸子元素以适应父元素高度
