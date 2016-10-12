<h1 style="font-size: 40px;text-align:center;color: #007cdc;">
    Nodejs 模块
</h1>

js es6之前，通过 var 或者 function 可以定义一些全局变量、对象，往往在不经意之间就会出现命名冲突的现象，造成变量被覆盖，方法被重写的后果，尤其是在多人协作或者项目中引入大量的js文件时，更容易出现代码污染。nodejs 模块将执行特定功能的代码块或者代码文件看做是一个独立的模块，每一个模块有自己独立的作用域。但这些模块不是孤立的，可以存在依赖关系。

nodejs 在安装的时候同时安装了 npm 这个包管理工具，通过 npm 可以在我们的项目内引入各种各样的模块，每一个模块都是独立的，完整的。

## 模块的分类

在nodejs中，模块和文件是一一对应的，大致分为以下三类。

### 核心模块

```js
http
fs
path
...
```

### 文件模块

```js
//通过相对路径将文件模块导入，通常是自己写的模块。
var myModule = require('./example.js')
```

### 第三方模块

```js
//通过绝对路径引入第三方模块，通常是npm装的包，nodejs会自动到node_modules文件夹下去找。
var React = require('react');
//这里nodejs会去node_modules文件夹下找react文件夹下的package.json中的main字段写的入口文件
```

## 模块的流程

### 创建模块

创建一个入口 js 文件，里面加入特定的功能，可以是导出一段字符串，一个对象，一个方法等等，例如下面的 teacher.js ,我们写入了一个方法。

```js
function add(name) {
  console.log('teacher name : ' + name);
}

```

### 导出模块

通过导出模块，将这个模块与这个文件建立起一种关系。

```js
// 可以导出一个对象
module.exports={
  add,
}
// 也可以直接将这个方法导出
module.exports=add;
// 也可以定义一个新的模块属性导出，这里可以省略module
module.exports.add=add;

// 注意，对应不同的导出方式，导入后的用法也不同
```

### 加载模块

```js
var add = require('./teacher.js');
// 对应不同的导出方式，我们拿到的 add 也不同
```

### 使用模块

```js
// 对应第一种导出方式
console.log(add); //{ add: [Function: add] }
add.add('newming'); //teacher name : newming

// 对应第二种导出方式
console.log(add); // [Function: add]
add('newming'); //teacher name : newming

// 对于第三种方法，同第一中方法一样

```
