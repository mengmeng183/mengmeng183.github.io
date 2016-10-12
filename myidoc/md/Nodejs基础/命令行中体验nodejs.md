<h1 style="font-size: 40px;text-align:center;color: #007cdc;">
    命令行中体验nodejs
</h1>
Nodejs　就是一个运行于本地的　JS　的解释器，可以让我们脱离浏览器，来使用　JS　．Node.js　就是扒了皮的　chrome.

nodejs 本质上是一个基于 Chrome V8引擎的 javascript 的执行环境，通常我们写的 js 代码是在浏览器中执行，脱离了浏览器就无法运行，这里nodejs 提供了 javascript 的运行环境，使得 js 能够脱离浏览器运行，因此可以做到利用 js 就可以来写后天等等其他事情，同时，因为 nodejs 是基于 Chrome V8引擎的单线程事件驱动、非阻塞式 I/O 的模型，使得其运行速度很快。

在浏览器中执行 js 代码我们都不陌生，直接打开调试工具就可以。

下面是如何在命令行中执行 js 代码。

```shell
# 在命令行中输入 node 进入 node 环境
node
# 可以看到命令行变为了一个尖括号开始的输入环境
# 下面就要输入 js 代码了
> var a = 1,b=2;function add(a,b){return a+b};add(a,b)
# 回车执行
3
```

是不是很神奇！！这里有一个区别。浏览器中有全局变量 `window,document`，node 没有，它有自己特殊的一些全局变量，比如 `process`。

当然，可以用 node 直接执行我们的js文件。

```js
node example.js
```
