<h1 style="font-size: 40px;text-align:center;color: #007cdc;">
    Nodejs QueryString
</h1>

QueryString 模块提供了一些公共方法去处理查询字符串。

## querystring.stringify

将一个对象序列化为一个字符串

```js
stringify方法有三个参数
querystring.stringify({ foo: 'bar', baz: ['qux', 'quux'], corge: '' })
// returns 'foo=bar&baz=qux&baz=quux&corge='

querystring.stringify({foo: 'bar', baz: 'qux'}, ';', ':')
// returns 'foo:bar;baz:qux'
```

## querystring.parse

反序列化一个查询字符串为一个对象

```js
querystring.parse('foo=bar&baz=qux&baz=quux&corge')
// returns { foo: 'bar', baz: ['qux', 'quux'], corge: '' }
```

## querystring.escape

转译

```js
querystring.escape('哈哈');

// '%E5%93%88%E5%93%88'
```

## querystring.unescape

反转译
