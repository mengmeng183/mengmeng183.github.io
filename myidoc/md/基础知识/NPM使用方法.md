<h1 style="font-size: 40px;text-align:center;color: #007cdc;">
    NPM的使用方法
</h1>

NPM 是随同 Node 一起安装的包管里工具。

- 允许用户从NPM服务器下载别人编写的第三方包到本地使用。
- 允许用户从NPM服务器下载并安装别人编写的命令行程序到本地使用。
- 允许用户将自己编写的包或命令行程序上传到NPM服务器供别人使用。

## 1.模块初始化

创建模块，package.json 文件是必不可少的。我们可以使用 NPM 生成 package.json 文件，生成的文件包含了基本的结果。

```
npm init
```

以上的信息，你需要根据你自己的情况输入。在最后输入 "yes" 后会生成 package.json 文件。同时在这个 json 文件中可以在 script 字段定义我们自己的一些脚本。

## 2.使用 npm 命令安装模块

```
npm install <Module Name>

例如
npm install express --save
```

这时，就会在我们的工程目录下生成一个 node_modules 的文件夹，在里边就会有 express 这个包了。

如果想要用这个包，只需要在需要的地方 require 或者 import 一下就可以了。

### 本地安装

将包安装在项目内的 `node_modules` 下，如果没有这个文件夹， npm 会自动创建。可以通过 `require()` 来引入项目内的包。

```
npm install express --save  # 版本名和版本号记录在dependencies字段
npm install express --save-dev  # 版本名和版本号记录在devDependencies字段
```

### 全局安装

全局安装后可以直接在命令行里使用，不能在项目内引入。

```
# 全局安装
npm install gulp -g
```

可以使用以下命令来查看所有全局安装的模块：

```
npm ls -g
```

## 3.卸载模块

```
npm uninstall express
```

## 4.更新模块

```
npm update express
```

## 5.搜索模块

```
npm search express
```

## 6.发布模块

```
npm publish
```

这里需要注意，发布模块的话需要在 npm 官网注册账号，并且执行下面的命令。

```
npm adduser
Username: demo
Password:
Email:(this is public) 977527479@qq.com
```

## 7.其他常用命令

```
npm help
npm cache clear  #可以清空NPM本地的缓存
npm unpublish @[版本号]  #撤销发布的某个版本的模块
```
