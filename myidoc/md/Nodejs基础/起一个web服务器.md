<h1 style="font-size: 40px;text-align:center;color: #007cdc;">
    起一个web服务器
</h1>

利用 nodejs 起一个 web 服务器非常简单，拿到官网给出的 [example](https://nodejs.org/dist/latest-v4.x/docs/api/synopsis.html) 示例，在我们的项目中创建一个 example.js 文件，粘贴如下代码，到对应文件目录下，命令行中执行 `node example.js`，命令行中打印出 `Server running at http://127.0.0.1:3000/`，即成功启动了一个 web 服务器。

```js
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

这里需要注意的是，上面的 js 语句中用到了 ES6 的语法，也就是说 nodejs 本身也支持了 ES6 的语法，具体支持的程度，请查看官网。[ECMAScript 2015 (ES6) and beyond](https://nodejs.org/en/docs/es6/)

下面简单的分析下代码。

首先加载了一个 nodejs 自带的模块 `http`

```js
const http = require('http');
```

然后通过 createServer 方法来创建一个 web 服务器，通过 listen 让服务器 3000 端口监听请求，当监听到在 3000 端口的请求时，会执行匿名回调函数 ==>

```js
(req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
}
```

这里 req，res 两个参数分别为请求体和响应体。req 用来获取请求的相关信息，比如请求类型，请求是从什么地方发出的等等。req 告诉服务器给这个请求响应些内容，否则请求会处于挂起状态。这里设置了给客户端返回一个 `hello world` ，同时在返回的请求头里写入返回的状态码为 200，即成功的状态，返回的文本内容的类型是纯文本。

> 如果后台代码做了修改，需要重启服务器来执行最新代码。
