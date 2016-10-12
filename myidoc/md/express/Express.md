# Express框架
[Express官网](http://expressjs.com/)

Node.js web application framework --Nodejs技术的web应用框架

React是一个前端框架，Express是后台（服务器）框架

客户端向服务器端请求页面过程：

客户端向服务器发送带参（eg:用户名）请求 alibaba.com

将参数传给代码-->1.查询数据库，2.把数据插入html模板-->生成html

首先执行的代码是路由代码，然后执行其它代码

express作用：1.查询数据库，2.把数据插入html模板

### 动手做
创建express-api文件夹
```
mkdir express-api
```
#### 将普通项目变为nodejs项目

```
npm init // 创建package.json文件
```
```
name 项目名 express-api

version 版本 最早版本一般为0.0.1

description 描述 eg:express api with React

entry point 默认入口点 index.js

test command 测试

git repository  git仓库地址

keywords 关键字

author 作者

license 协议
```

安装express

```
npm install --save express
```
创建index.js

```js
console.log('hello express');
```
在命令行执行node index.js(在node下执行index.js),在浏览器访问127.0.0.1:3000或localhost:3000,在命令行输出hello express

3000端口是测试端口,127.0.0.1代表本地机器,对应的域名为localhost

console本意是“控制台”，在前台运行时就是chrome devtools(开发者工具) 的 console,在后台运行，就是命令行界面

http请求=Verb+Path(最基本的)

http请求=get/post/...+/about

```js
var express = require('express')
var app = express()

app.get('/', function (req, res) {
  res.send('Hello express')
})

app.get('/ppp', function (req, res) {
  res.send('Hello ppp')
})

app.listen(3000)
```
命令行执行`node index.js`,浏览器访问localhost:3000显示`Hello express`,访问localhost:3000/ppp显示`Hello ppp`

express的代码是要在服务器上运行的，所以上面的代码用来接收请求，常用的请求有两种get(只读请求，返回响应请求)和post(要往服务器写东西)

- GET  从指定的资源请求数据。
- POST 向指定的资源提交要被处理的数据

首先执行的代码是路由代码，然后执行其它代码

#### 什么是路由? router?

基本意思：根据http请求，决定哪个页面要显示

拓展意思：根据http请求，决定哪段代码要执行

express路由跑在服务器上，响应客户端发出的request，决定哪部分代码要被执行（做任务分发）

routes 会同时出现在 express 后台和 react 前台，作用相同

> 根据请求路径（包括 http 动词）的不同，决定要触发哪一部分代码

但是，客户端路由，可以认为是“页面路由”，而服务器端的路由，可以叫做”API 路由“ 。

```js
var express = require('express')
var app = express()

app.get('/liyuexi', function (req, res) {
  console.log('hello liyuexi');
})

app.get('/mengmeng', function (req, res) {
  console.log('hello mengmeng');
})
app.listen(3000)
```
命令行执行`node index.js`,浏览器访问localhost:3000/liyuexi,在命令行显示`Hello liyuexi`,访问localhost:3000/mengmeng,在命令行显示`Hello mengmeng`

```js
app.listen(3000,function(){
  console.log('running on port 3000...plz visit http://localhost:3000');
})
```
命令行执行`node index.js`时会显示`running on port 3000...plz visit http://localhost:3000`，看起来更明白。

#### 如何让express写的应用程序返回html页面
```js
var express = require('express')
var app = express()

app.get('/', function (req, res) {
  var page = '<html>'+
                '<body>' +
                  '<h1> index.html</h1>' +
                '</body>' +
              '</html>'
  res.send(page)
})

app.get('/about.html', function (req, res) {
  var page = '<html>'+
                '<body>' +
                  '<h1> about.html</h1>' +
                '</body>' +
              '</html>'
  res.send(page)
})

app.listen(3000,function(){
  console.log('running on port 3000...plz visit http://localhost:3000');
})
```
命令行执行node index.js，浏览器访问localhost:3000时显示h1的`index.html`,浏览器访问localhost:3000/about.html时显示h1的`about.html`

#### 读取请求参数

request = verb + path

参数(parameters)作为path来传入后台，这样，可以实现前台数据传入后台代码中

```js
var express = require('express')
var app = express()

app.get('/:name', function (req, res) {
  console.log(req.params);
  var userName = req.params.name;
  var page = '<html>'+
                '<body>' +
                  '<h1>' +
                  userName + '的购物车' +
                  '</h1>' +
                '</body>' +
              '</html>'
  res.send(page)
})
app.listen(3000,function(){
  console.log('running on port 3000...plz visit http://localhost:3000');
})
```
命令行执行node index.js，浏览器访问localhost:3000/mengmeng时显示h1的`mengmeng的购物车`,localhost:3000/后面是xxx就会显示`xxx的购物车`
```
console.log(req.params); -->{ name: 'mengmeng' }
```
#### CURL（后台接口调试工具）小教程

**模拟get请求**
```
var express = require('express')
var app = express()

app.get('/:name', function (req, res) {
  var userName = req.params.name;
  var page = '<html>'+
                '<body>' +
                  '<h1>' +
                  userName + '的购物车' +
                  '</h1>' +
                '</body>' +
              '</html>'
  res.send(page)
})
app.listen(3000,function(){
  console.log('running on port 3000...plz visit http://localhost:3000');
})
```
```
$ curl --request GET localhost:3000/mengmeng
```
命令行会显示`<html><body><h1>mengmeng的购物车</h1></body></html>`

**模拟post请求**
```
var express = require('express')
var app = express()

app.post('/:name', function (req, res) {
  res.send("a POST request received " + req.params.name)
})

app.listen(3000,function(){
  console.log('running on port 3000...plz visit http://localhost:3000');
})

```
```
$ curl --request POST localhost:3000/mengmeng
```
命令行会显示`a POST request received mengmeng`
