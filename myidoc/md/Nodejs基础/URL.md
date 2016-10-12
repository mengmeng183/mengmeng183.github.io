<h1 style="font-size: 40px;text-align:center;color: #007cdc;">
    Nodejs URL
</h1>

## url.parse

将一个URL地址解析为一个对象

```js
命令行中执行node，进去node环境
~ node
> url.parse('http://www.imooc.com:8080/video/6710?from=newming&course=node#floor1');

Url{
	protocol : 'http:',
	slashes : true,
	auth : null,
	host : 'www.imooc.com',
	port : '8080',
	hostname : 'www.imooc.com',
	hash : '#floor1',
	search : '?from=newming&course=node',
	query : 'from=newming&course=node',
	pathname : '/video/6710',
	path : '/video/6710?from=newming&course=node',
	href : 'http://www.imooc.com/video/6710'
}
```

## url.format

将一个URL对象格式化为一个URL字符串

```js
~ node
> url.format({
	protocol : 'http:',
	slashes : true,
	auth : null,
	host : 'www.imooc.com',
	port : '8080',
	hostname : 'www.imooc.com',
	hash : '#floor1',
	search : '?from=newming&course=node',
	query : 'from=newming&course=node',
	pathname : '/video/6710',
	path : '/video/6710?from=newming&course=node',
	href : 'http://www.imooc.com/video/6710'
})

'http://www.imooc.com:8080/video/6710?from=newming&course=node#floor1'
```

## url.resolve

url.resolve(from, to)

Take a base URL, and a href URL, and resolve them as a browser would for an anchor tag. Examples:

```js
url.resolve('/one/two/three', 'four')         // '/one/two/four'
url.resolve('http://example.com/', '/one')    // 'http://example.com/one'
url.resolve('http://example.com/one', '/two') // 'http://example.com/two'
```
