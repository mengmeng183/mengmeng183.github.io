<h1 style="font-size: 40px;text-align:center;color: #007cdc;">
    material-ui
</h1>

[官网链接,点击进入官网](http://www.material-ui.com/#/)

**要求**

1.react项目

2.单页面应用 SPA(网站长的像原生应用)

3.node环境

安装material-ui
```
npm install material-ui --save
```
用`react-tap-event-plugin`来实现 `touch / tap / clickevents`

装`react-tap-event-plugin`
```
npm install react-tap-event-plugin --save
```

在应用的开始进行配置

/*index.js*/
```
import injectTapEventPlugin from 'react-tap-event-plugin';
injectTapEventPlugin();
```
V0.15.0之后版本需要用`MuiThemeProvider`主题

1.用`MuiThemeProvider`主题包裹
```
import React from 'react';
import ReactDOM from 'react-dom';
import MuiThemeProvider from 'material-ui/styles/MuiThemeProvider';
import MyAwesomeReactComponent from './MyAwesomeReactComponent';

const App = () => (
  <MuiThemeProvider>
    <MyAwesomeReactComponent />
  </MuiThemeProvider>
);

ReactDOM.render(
  <App />,
  document.getElementById('app')
);
```
2.主题

在App.js中导入主题
```
import getMuiTheme from 'material-ui/styles/getMuiTheme';
```
在App.js的class内
```
getChildContext() {
  return {muiTheme: getMuiTheme()};
}
```
在App.js的class外
```
App.childContextTypes = {
  muiTheme: React.PropTypes.object.isRequired,
};
```
material-ui官网-->Customization-->Themes
默认有两种主题：

- LIGHT THEME(DEFAULT)

- DARK THEME

Font icon:只有一种颜色

SVG icon:可以有多种颜色，中间有空格的用`-`连接

**定制自己的主题**

material-ui官网-->Customization-->Themes最下面
