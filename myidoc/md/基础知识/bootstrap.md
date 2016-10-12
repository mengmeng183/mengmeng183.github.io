<h1 style="font-size: 40px;text-align:center;color: #007cdc;">
    bootstrap
</h1>
[bootstrap官网](http://getbootstrap.com/)

[bootstrap中文网](http://www.bootcss.com/)

bootstrap是一个类库，写好了css，起好了名，直接使用样式

> 如果在项目中要用bootstrap,在项目开始时就要引入，否则要重新修改样式

只用css,只引入css就行了

１．[下载](http://v3.bootcss.com/getting-started/#download)
- 用于生产环境的 Bootstrap
- Bootstrap 源码
- Sass

２．使用 Bootstrap 中文网提供的免费 CDN 加速服务
```
<!-- 新 Bootstrap 核心 CSS 文件 -->
<link rel="stylesheet" href="http://cdn.bootcss.com/bootstrap/3.3.0/css/bootstrap.min.css">

<!-- 可选的Bootstrap主题文件（一般不用引入） -->
<link rel="stylesheet" href="http://cdn.bootcss.com/bootstrap/3.3.0/css/bootstrap-theme.min.css">

<!-- jQuery文件。务必在bootstrap.min.js 之前引入 -->
<script src="http://cdn.bootcss.com/jquery/1.11.1/jquery.min.js"></script>

<!-- 最新的 Bootstrap 核心 JavaScript 文件 -->
<script src="http://cdn.bootcss.com/bootstrap/3.3.0/js/bootstrap.min.js"></script>
```
３．装包
```
npm install bootstrap --save
```
**在项目中引入bootstrap**
/*index.js*/
```
import 'bootstrap/dist/css/bootstrap.min.css'; //引号内为bootstrap包所在位置
```
在导入bootstrap后如果报错说解析不了字体，那么需要配置字体

图标字体的加载可以选择file-loader 或 url-loader 进行加载，配置如下（示例配置，大家在项目中最好还是按实际情况配置）

1.安装url-loader
```
npm install --save-dev url-loader
```
2.在webpack.config.js的moduler中的loaders中增加下面的内容
```
{
  test: /\.(woff|woff2|ttf|svg|eot)(\?v=\d+\.\d+\.\d+)?$/,
  loader: "url?limit=10000"
}
```
不在react中使用bootstrap js

引入jquery和bootstrap.min.js(全部的)

可以单引bootstrap里的js文件，eg:modal.js，用到哪个引哪个
