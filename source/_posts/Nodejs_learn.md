---
title: Nodejs
date: 2024-06-21 9:32:32
tags: Node.js
---
# Nodejs
## fs文件系统模块
fs模块是Nodejs官方提供的，用来操作文件的模块
它提供了一系列方法和属性，用来满足用户对文件的操作需求
```JavaScript
//要在 JavaScript 代码中，使用 fs 模块来操作文件，则需要使用如下的方式先导入它
const fs =require('fs')
```
### 读取指定文件中的内容
#### fs.readFile()
##### 语法格式

```JavaScript
fs. readFile(path[,options],callback)
```

##### 参数解读
* 参数1：必选参数，字符串，表示文件路径
* 参数2：可选参数，表示以什么编码格式来读取文件
* 参数3：必选参数，文件读取完成后通过回调函数拿到读取的结果

示例代码：
```JavaScript
const fs = require('fs');

fs.readFile('./files/11.txt','utf8',function(err,dataStr){
    console.log(err);
    console.log('-----');
    console.log(dataStr);
)}
```
##### 判断文件是否读取成功
可以判断err对象是否为null，从而知晓文件读取的结果：
```JavaScript
const fs = require('fs');

fs.readfile('./file/1.txt','utf8',function(err,result){
    if(err){
        return console.log('文件读取失败' + err.message);
    }
    console.log('文件读取成功，内容是：' + result);
})
```
### 向指定的文件中写入内容
#### fs.writeFile()
##### 语法格式
```JavaScript
    fs.writeFile(file,data[,options],callback)
```
##### 参数解读
* 参数1：必选参数，需要指定一个文件路径的字符串，表示文件的存放路径
* 参数2：必选参数，表示要写入的内容
* 参数3：可选参数，表示以什么格式写入文件内容，默认值是utf8
* 参数4：必选参数，文件写入完成后的回调函数
示例代码：
```JavaScript
const fs = require('fs');
fs.writeFile('F:/file/2.txt','Hello Node.js!',function(err){
    if(err){
        console.log('文件写入失败'+err.message);
    }
    console.log('文件写入成功');
})
```
#### fs模块-路径动态拼接问题
使用fs模块时，使用的操作路径以./或.../开头的相对路径时，容易出现路径动态拼接问题
* 原因：代码在运行时，会以执行node命令时所处的目录，动态拼接出被操作文件的完整路径
* 解决方案：在使用fs模块操作文件时，直接提供完整的路径，不要提供./或.../开头的路径，从而防止路径动态拼接问题
```JavaScript
//不要使用./或.../这样的相对路径
fs.readFile('./files/1.txt','utf8',function(err,dataStr){
    if(err) return consle.log('读取文件失败' + err.message)
    console.log(dataStr);
})

//__dirname表示当前文件所在目录
fs.readFile(__dirname + 'files/1.txt','utf8',function(err,dataStr){
    if(err) return console.log('读取文件失败！' + err.message)
    console.log(dataStr);
})
```
## path路径模块
path模块是Node.js官方提供的、用来处理路径的模块
它提供了一系列方法和属性，用来满足用户对路径的处理需求
例如：
* `path.join()`：用来讲多个路径片段拼接成一个完整的路径字符串
* `path.basename()`：用来从路径字符串中，将文件名解析出来
```JavaScript
const path=require('path');
```
### 路径拼接
#### path.join()
使用path.join方法，可以把多个路径片段拼接为完整的路径字符串
##### 语法格式
```JavaScript
path.join([...paths])
```
##### 参数解读
* ...paths：路径片段的序列
* 返回值

示例代码：
```JavaScript
const pathStr=path.join('/a','/b/c','../','./d','e');
console.log(pathStr);//输出\a\b\d\e

const pathStr2=path.join(__dirname,'./files/1.txt');
console.log(pathStr2)//输出 当前文件所处目录\files\1.txt
```
**注：** 今后凡事涉及到路径拼接的操作，都要使用path.join()方法进行处理，不要直接使用+字符串拼接

### 获取路径中的文件名
#### path.basename()
使用path.basename()方法，可以获取路径中的最后一部分，经常通过这方方法获取灵境中的文件名
##### 语法格式
```JavaScript
path.basename(path[,ext])
```
##### 参数解读
* `path <string>`：必选参数，表示一个路径的字符串
* `ext<string>`：可选参数，表示文件扩展名
* return：`<string>`表示路径中的最后一部分

示例代码：
```JavaScript
const fpath='/a/b/c/index.html'; //文件存放的路径

var fullName = path.basename(fpath);
console.log(fullName); //输出index.html

var nameWithoutExt = path.basename(fpath,'.html');
console.log(nameWithoutExt); //输出index 
```
### 获取路径中的拓展名部分
#### path.extname()
使用path.extname()方法，可以获取路径中的拓展名部分
##### 语法格式
```JavaScript
path.extname(path)
```
##### 参数解读
* `path<string>`：必选参数，表示一个路径字符串
* return：`<string>`返回得到的扩展名字符串
示例代码：
```JavaScript
const fpath='/a/b/c/index.html'; //路径字符串

const fext=path.extname(fpath);
console.log(fext); //输出 .html
```
## http模块
http模块是Node.js官方提供的，用来创建web服务器的模块
通过http模块提供的http.creatServer()方法，就能方便的把一台普通的电脑，变成一台web服务器，从而对外提供web资源服务
```JavaScript
const path=require('http');
```
### 理解http
服务器和普通电脑的区别在于，服务器上安装了 web 服务器软件
在 Node.js 中，我们不需要使用 IIS、Apache 等这些第三方 web 服务器软件
因为我们可以基于 Node.js 提供的http 模块，通过几行简单的代码，就能轻松的手写一个服务器软件，从而对外提供 web 服务
### 创建最为基本的web服务器
#### 创建we服务器的基本步骤
① 导入http模块
② 创建web服务器实例
③ 为服务器实例绑定request事件，监听客户端的请求
④ 启动服务器
```JavaScript
const http=require('http'); //导入http模块

const server=http.createServer() //创建web服务器实例
server.on('request',(req,res)=>{ //为服务器绑定一个request事件
    //使用服务器实例的.on（）方法，为服务器绑定一request事件
    //只要有客户端来请求我们自己的服务器，就会触发request事件，从而调用这个事件处理函数
    console.log('Someon visit our web server.')
});
server.listen(3000,()=>{
    //调用server.listen（端口号，cb回调）方法，即可启动web服务器
    console.log('Server is running!');
});
```
#### req 请求对象
服务器接收到了客户端的请求-->调用通过server.on()为服务器绑定的request事件处理函数
如果想在事件处理函数中，访问与客户端相关的数据或属性，可以使用如下方式：
```JavaScript
server.on('request',(req)=>{
    //req是请求对象，它包含了与客户端相关的数据和属性，例如：
    //req.url是客户端请求的URL地址
    //req.method是客户端的method请求类型
    const str=`Your request url is ${req.url},and request method is ${}req.method`;
    console.log(str);
})
```
#### res 响应对象
在服务器的request事件处理函数中，如果想访问与服务器相关的数据或属性，可以使用如下方式：
```JavaScript
server.on('request',(req,res)=>{
    //res是响应对象，它包含了与服务器相关的数据和属性，例如：
    //要发送到客户端的字符串
    const str = `Your request url is ${req.url},and request method is ${req.method}`;
    //res.end()：向客户端发送指定的内容，并结束这次请求的处理过程
    res.end(str);
});
```
#### 解决中文乱码问题
调用res.end()时，向客户端发送中文内容的时候，会出现乱码问题，此时需要手动设置内容的编码格式：
```JavaScript
server.on('request',(req,res)=>{
    const str=`您请求的ur1地址是${req.ur1}，请求的method类型是${eq.method}`;
    //为了防止中文显示乱码的问题，需要设置响应头Content-type为text/html,charset=utf-8
    res.setHeader('Content-Type','text/html;charset=utf-8');
    //把包含中文的内容，响应给客户端
    res.end(str);
});
```
#### 根据不同的url响应不同的html内容
① 获取请求的url
② 设置默认的响应内容为404Not found
③ 判断用户请求的是否为/或/index.html首页
④ 判断用户请求的是否为/about.html关于页面
⑤ 设置Content-Type响应头，防止中文乱码
⑥ 使用res.end()把内容响应给客户端
#### 动态响应内容
```JavaScript
server.on('request',function(req,res){
    const url=req.url;//1、获取请求的url地址
    let content='<1>404 Not found!</h1>'//2、设置默认的内容为404 not found
    if(url === '/' || url === '/index.html'){
        content = '<h1>首页</h1>'；//3、用户请求的是首页
    }else if(url === '/about.html'){
        content = '<h1>关于页面</h1>';//4、用户请求的是关于页面
    }
    res.setHeader('Content-Type','text/html;charset=utf-8');//5、设置响应头，防止乱码
    res.end(content);//6、将内容发送给客户端
})
```
## Node.js中的模块
### Node.js中模块的分类
Node.js中，根据模块的来源不同，将模块大致分为3类：
* 内置模块：是由node.js官方提供的（如：fs，path，http等）
* 自定义模块：用户创建的每一个js文件，都是自定义模块
* 第三方模块：由第三方开发出来的模块，并非官方提供的内置模块，也不是用户自行创建的，使用前需要下载

### 加载模块
使用require()方法，可以加载需要的内置模块、用户自定义模块、第三方模块进行使用。
```JavaScript
const fs=require('fs');//加载内置fs模块
const custom=require('./cystom.js');//加载用户自定义模块
const moment=require('moment');//加载第三方模块
```
### 模块作用域
#### 什么是模块作用域
和函数作用域类似，在自定义模块中定义的变量、方法等成员，只能在当前模块内被访问，这种模块级别的访问限制叫做模块作用域
#### 模块作用域的优点
防止全局变量污染的问题
#### 向外共享模块作用域中的成员
##### module对象
在每个.js自定义模块中都有一个module对象，它里面存储了和当前模块有关的信息
##### module.exports对象
在自定义模块中，可以使用module.exports对象，将模块内的成员共享出去，供外界使用
外界用require()方法导入自定义模块时，得到的就是module.exports所指向的对象
##### 共享成员时的注意点
使用require()方法导入模块时，导入的结果**永远以module.exports指向的对象为准**
##### exports对象
由于moudle.exports写起来较为复杂，node提供了exports对象简化共享成员的代码
默认情况下，exports/module.exports指向同一个对象
最终共享的结果，还是以module.exports指向的对象为准
##### exports和module.exports的使用误区
谨记，require()模块时，得到的永远是module.exports指向的对象

#### Node.js中的模块化规范
Node.js遵循了CommonJS模块化规范
CommonJS规定了模块的特性和各模块之间如何相互依赖
CommonJS规定：
1. 每个模块内部，module变量代表当前模块
2. module变量是一个对象，它的exports属性（即module.exports）是对外的接口
3. 加载某个模块，其实是加载该模块的module.exports属性。require()方法用于加载模块

## 模块的加载机制
### 优先从缓存中加载
模块子第一次加载后会被缓存——多次调用require()不会导致模块的代码被执行多次
**注：** 不论是内置模块、用户自定义模块、还是第三方模块，他们都会优先从缓存中加载，从而提高模块的加载效率
### 内置模块的加载机制
内置模块是由Node.js官方提供的模块，内置模块的加载优先级最高
例如，require('fs')始终返回内置的fs模块，即使在node_module目录下有相同名字的包也叫fs
### 自定义模块的加载机制
使用requre()加载自定义模块时，必须指定以./或../开头的路径标识符
在加载自定义模块时，如果没有指定./或../这样的路径标识符，则node会把它当做内置模块或第三方模块进行加载
同时，在使用require()导入自定义模块时，如果省略了文件的扩展名，则Node.js会按顺序分别尝试加载以下的文件：
1. 按照确切的文件名进行加载
2. 补全.js扩展名进行加载
3. 补全.json扩展名进行加载
4. 补全.node扩展名进行加载
5. 加载失败，终端报错

### 第三方模块的加载机制
如果传递给require()的模块标识符不是一个内置模块，也没有以'./'或'../'开头，则Node.js会从当前模块的父目录开始，尝试从/node_modules文件中加载第三方模块
如果没有找到对应的第三方模块，则移动到再上一层父目录中进行加载，直到文件系统的根目录
例如，假设在'C：\Users\itheima\project\foo.js’'文件里调用了require('tools')，则Node.js会按以下顺序查找：
1. C:\Users\itheima\project\node_modules\tools
2. C:\Users\itheima\node_modules\tools
3. C:lUserslnode_modulesl\tools
4. C:\node_modules\tools

### 目录作为模块
当把目录作为模块标识符，传递给require()进行加载的时候，有三种加载方式：
1. 在被加载的目录下查找一个叫做package.json的文件，并寻找main属性，作为require()加载的入口
2. 如果目录里没有package.json文件，或者main入口不存在或无法解析，则Node.js将会试图加载目录下的index.js文件
3. 如果以上两步都失败了，则Node.js会在终端打印错误消息，报告模块的确实：Error:Cannot find module 'xxx'

## Express
### 初识Express
#### 什么是Express
定义：Express是基于Node.js平台，快速、开放、极简的Web开发框架
即：Express类似于http模块，是专门用来创建Web服务器的
Express的本质：就是一个npm上的第三方包，提供了快速创建Web服务器的便捷方法
#### Express能做什么
对于前端程序员来说，最常见的两种服务器，分别是：
* Web网站服务器：专门对外提供Web网页资源的服务器
* API接口服务器：专门对外提供API接口的服务器
使用Express可以方便、快速的创建Web网站的服务器或API接口的服务器
#### Express的基本使用
##### 安装
```
npm i express
```
##### 创建基本的Web服务器
```JavaScript
//1、导入express
const rxpress =require('express');
//2、创建web服务器
const app = express()
//3、调用app.listen(端口号xxx,启动成功后的回调函数callback())，启动服务器
app.listen(80,()=>{
    console.log('express server running at http://127.0.0.1');
})
```
##### 监听GET请求
通过app.get()方法，可以监听客户端的GET请求，具体的语法格式：
```JavaScript
app.get('请求URL',function(req,res){
    //处理函数
})
```
* 参数1：客户端请求的URL地址
* 参数2：请求对应的处理函数
* req：请求对象（包括与请求相关的属性与方法）
* res：响应对象（包含与响应相关的属性和方法）
##### 监听POST请求
通过app.post()方法，可以监听客户端的POST请求，具体的语法格式：
```JavaScript
app.post('请求URL',function(req,res){
    //处理函数
})
```
* 参数1：客户端请求的URL地址
* 参数2：请求对应的处理函数
* req：请求对象（包括与请求相关的属性与方法）
* res：响应对象（包含与响应相关的属性和方法）

##### 把内容响应给客户端
通过res.send()方法，可以把处理好的内容发送给客户端
```JavaScript
app.get('/user',(req,res)=>{
    //向客户端发送JSON对象
    res.send({
        name:'tiedan',
        age:22,
        gender:'男'
    })
app.post('/user',(req,res)=>{
    //向客户端发送文本内容
    res.send('请求成功');
})
```
##### 获取URL中携带的查询参数
通过req.query对象，可以访问到客户端通过查询字符串的形式，发送到服务器的参数
```JavaScript
app.get('/',(req,res)=>{
    //req.query默认是一个空对象
    //客户端使用?name=tiedan&age=22这种查询字符串的形式，发送到服务器参数
    //可以通过req.query对象访问到，例如：
    //req.query.name    req.query.age
    console.log(req.query)
})
```
##### 获取URL中的动态参数
通过req.params对象，可以访问到URL中，通过“:”匹配到的动态参数：
```JavaScript
//URL地址中，可以通过“:参数名”的形式，匹配动态参数值
app.get('/user/:id',(req,res)=>{
    //req.params默认是一个空对象
    //里面存放着通过 : 动态匹配到的参数值
    console.log(req.params)
})
```
#### 托管静态资源
##### express.static()
通过它，我们可以非常方便地创建一个静态资源服务器
通过如下代码，就可以将public目录下的图片、CSS文件、JavaScript文件对外开放访问了：
```JavaScript
app.use(express.static('public'))
```
此时就可以通过 端口/文件夹 来访问public目录中的所有文件了
##### 托管多个静态资源目录
如果需要托管多个静态资源目录，可以多次调用express.static()函数
```JavaScript
app.use(express.static('public'));
app.use(express.static('file'));
```
访问静态资源文件时，express.static()函数会根据目录的添加顺序查找所需的文件
##### 挂载路径前缀
如果希望在托管的静态资源访问路径之前，挂载路径前缀，则可以使用如下的方式：
```JavaScript
app.use('/public',express.static('public'));
```
如此就可以通过带有/public前缀地址来访问public目录中的文件了

#### nodemon
##### 为什么使用nodemom
编写调试Node.js项目时，如果修改了项目代码，需要频繁的手动关闭再启动，非常繁琐
使用nodemon，能够监听文件的变动，代码被修改后，nodemon会帮助重启项目，方便开发调试
##### 使用nodemon
我们可以将node命令替换为nodemon命令，使用nodemon app.js来启动项目。这样做的好处是：代码被修改之后，会被nodemon监听到，从而实现自动重启项目的效果
```
node app.js
//将上面的终端命令，替换为下面的终端命令，即可实现自动重启项目的效果
nodemon app.js
```
### Express路由
#### 路由的概念
##### Express中的路由
在Express中国，路由指的是客户端的请求与服务器处理函数之间的映射关系
Express中的路由分3部分组成，分别是：请求的类型，请求的地址，处理函数
格式：
```JavaScript
app.METHOD(PATH,HANDLER)
```
##### Express中的路由的例子
```JavaScript
//匹配GET请求，且请求URL为/
app.get('/',function(req,res){
    res.send('Hello World!!!');
});

//匹配POST请求，且请求URL为/
app.post('/',function(req,res){
    res.send('Got a POST request');
})
```
##### 路由的匹配过程
![](media/17320052934134/17329682230108.png)

#### 路由的使用
##### 简易方法
在Express中使用路由最简单的方式，就是把路由挂在到app上，示例代码：
```JavaScript
const express = require('express');
//创建web服务器，命名为app
const app = express()

//挂载路由
app.get('/',(req,res)=>{res.send('Hello World.')});
app.post('/',(req,res)=>{res.send('Post Request.')});

//启动web服务器
app.listen(80,()=>{
consol.log('The Server is running');
})
```

