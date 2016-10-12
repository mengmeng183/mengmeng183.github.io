<h1 style="font-size: 40px;text-align:center;color: #007cdc;">
    mongodb
</h1>

## 1. 什么是MongoDB
[官网链接](https://docs.mongodb.com/)
- MongoDB是一个基于分布式文件存储的开源数据库系统
- MongoDB 将数据存储为一个文档，数据结构由键值(key=>value)对组成。MongoDB 文档类似于 JSON 对象。字段值可以包含其他文档，数组及文档数组。

[学习链接](http://haoqicat.com/react-express-api/2-mongodb)

## 2. MongoDB安装
### 2.1 [windows安装](https://docs.mongodb.com/v3.0/tutorial/install-mongodb-on-windows/)
[Windows官方安装指南](https://docs.mongodb.org/v3.0/tutorial)

### 2.2 mac安装
[Mac官方安装指南](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/)

1. 先安装homebrew
```
http://brew.sh/
```

2. 使用brew安装mongodb
```
brew install mongodb
```

3. 再安装可视化工具
 [Robomongo]( https://robomongo.org/)

### 2.3 [Ubuntu安装](https://docs.mongodb.com/v3.0/tutorial/install-mongodb-on-ubuntu/)
1.
```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
```
2.Ubuntu 14.04
```
echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.0.list
```
3.
```
sudo apt-get update
```
4.
```
sudo apt-get install -y mongodb-org
```

## 3. mongodb启动与连接

### 3.1 windows启动服务器端

在~下创建一个data文件夹（数据库建在哪下面的路径就写哪）

```
mongod --dbpath=./data //在27017端口起一个数据库
```

- 如果出现`waiting for connections on port 27017`就表示**启动成功**,已经在27017端口上监听了客户端的请求
- 注意：`--dbpath`后的值表示数据库文件的存储路径,而且后面的路径必须事先创建好，必须已经**存在**，否则服务开启失败
- 注意：这个命令窗体绝对**不能关**,关闭这个窗口就相当于停止了`mongodb`服务
- 也可以在命令后面加上参数 `--port 27017` 来指定端口

### 3.2 启动客户端连接服务器
启动操作界面：１．用户图形接口GUI   ２．命令行接口CLI

对于mongodb我们使用mongo shell这个命令行来操作

命令窗体中输入 mongo --host=127.0.0.1 或者 mongo 按回车键（`mongo`启动mongo shell,去操作数据库）

> 备注：--host后的值表示服务器的ip地址


## 4. MongoDB基本概念
- **数据库** MongoDB的单个实例可以容纳**多个**独立的数据库，比如一个学生管理系统就可以对应一个数据库实例(数据库是mongodb中的顶级存储单位)
- **集合** 数据库是由集合组成的,一个集合用来表示一个**实体**,如学生集合
- **文档** 集合是由文档组成的，一个文档表示一条**记录**,比如一位同学张三就是一个文档

<img src="http://7xjf2l.com1.z0.glb.clouddn.com/mongodbstructure.jpg">
<img src="http://7xjf2l.com1.z0.glb.clouddn.com/mongovue.png">

## 5. 数据库操作
### 5.1 使用数据库
**语法**
```
use database_name      //database_name代表数据库的名字
```
注：如果此数据库存在，则切换到此数据库下,如果此数据库还不存在也可以切过来

**实例**
切换到 `person`数据库下
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-8.png">

### 5.2 查看所有数据库
**语法**
```
show dbs
```

> 备注: 我们刚创建的数据库person 如果不在列表内， 要显示它，我们需要向 person 数据库插入一些数据 db.person.insert({name:"zhangSan",age:30})(在person数据库下创建了一个person集合，在集合中添加了一条记录)

<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-7.png">

### 5.3 查看当前使用的数据库
**语法**
```
db 或 db.getName()
```
> 注：db代表的是当前数据库 也就是person这个数据库

**实例**

<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-9.png">

### 5.4 删除数据库
**语法**
```
db.dropDatabase() //删除当前数据库
```

**实例**

<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/mongodb-shanChuShuJuKu-1.png">


## 6. 集合操作
### 6.1 查看帮助
**语法**
```
db.worker.help()
```

**实例**
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-13.png">

### 6.2 查看数据库下的集合
**语法**
```
show collections
```

**实例**

<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-11.png">

### 6.3 创建集合

一个数据库可建无数个集合

**创建一个空集合**
```
db.createCollection(collection_Name)      collection_Name集合的名称，集合的名称要是一个小写的复数形式
```
![db2](http://odowb0dhc.bkt.clouddn.com/db2.png)
**创建集合并插入一个文档**
- collection_Name集合的名称
- document要插入的文档

```
db.collection_Name.insert(document)
```

<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-14.png">

**删除集合**
```
db.items.drop()
```
**集合重命名**

![db8](http://odowb0dhc.bkt.clouddn.com/db8.png)
## 7. 插入文档
 ### 7.1 insert
 **语法**
```
 db.collection_name.insert(document)
 ````
 **参数**
 - collection_name 集合的名字
 - document 插入的文档

**实例**
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-15.png">

> 每当插入一条新文档的时候mongodb会自动为此文档生成一个`_id`属性,_id一定是唯一的，用来唯一标识一个文档
>  _id也可以直接指定，但如果数据库中此集合下已经有此_id的话插入会失败

**查看集合里的内容**
```
db.posts.find()
```

![db3](http://odowb0dhc.bkt.clouddn.com/db3.png)

**按条件查看集合里的内容**
```
db.props.find({name:'mengmeng'})
```
![db4](http://odowb0dhc.bkt.clouddn.com/db4.png)

### 7.2 save
 **语法**
```
db.collection_name.save(document)
```

**参数**
- collection_name 集合的名字
- document 插入的文档

> 注：如果不指定 _id 字段 save() 方法类似于 insert() 方法。如果指定 _id 字段，则会更新（覆盖）该 _id 的数据。


**实例**
```
db.person.save({name:"xiaoHong",age:50})
```
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/mongodb-baoCun-1.png">
```
db.person.save({_id:ObjectId("562c9caf671c978b6596e825"),name:"xiaoHong",age:10})
```
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/mongodb-baoCun-2.png">

## 8. 更新文档
**语法**
```
db.collection.update(
   <query>,
   <updateObj>,
   {
     upsert: <boolean>,
     multi: <boolean>
   }
)
```

**参数说明**
- query  查询条件,指定要更新符合哪些条件的文档
- update  更新后的对象或指定一些更新的操作符
     -  $set直接指定更新后的值(如果更新的属性存在，直接更新，若不存在在后面增加该属性)
     ![db6](http://odowb0dhc.bkt.clouddn.com/db6.png)
     -  $inc在原基础上累加(只能对数值型进行累加)
     ![db5](http://odowb0dhc.bkt.clouddn.com/db5.png)
- upsert  可选，这个参数的意思是，如果不存在符合条件的记录时是否插入updateObj.  默认是false,不插入。
- multi  可选，mongodb 默认只更新找到的第一条记录，如果这个参数为true,就更新所有符合条件的记录。


**实例**
将document数据中name是liSi 的数据的name修改为liSi_update
```
db.worker.update({name:'liSi'},{$set:{name:'liSi_update'}})
```

> 注：如果有多条name是liSi的数据只更新一条,如果想全部更新需要指定{multi:true}的参数

<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-18.png">


## 9. 文档的删除
remove方法是用来移除集合中的数据

**语法**
```
db.collection.remove(
   <query>,
   {
     justOne: <boolean>
   }
)
```

**参数说明**

- query :（可选）删除的文档的条件。
- justOne : （可选）如果设为 true 或 1，则只删除匹配到的多个文档中的第一个

不加参数删除集合内所有
```
db.collection.remove({})   //删除所有
```

**实例**
删除worker集合里name是fJianZhou的所有Document数据
```
db.worker.remove({name:'fJianZhou'})
```
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-19.png">
删除person集合里name是xiaoHong的第一条数据
```
db.person.remove({name:"xiaoHong"},1)
```
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/mongodb-shanChuShuJu-1.png">

## 10. 查询文档
### 10.1 find
**语法**
```
db.collection_name.find()
```

**参数**
- collection_name 集合的名字

**实例**
查询worker下所有的文档
```
db.worker.find()
```

### 10.2 查询指定列
**语法**
```
db.collection_name.find({queryWhere},{key:1,key:1})
```

**参数列表**
- collection_name  集合的名字
-  queryWhere 参阅查询条件操作符
- key 指定要返回的列
  - 1 表示要显示
  - 0 表示不要显示

**实例**
```
db.worker.find({},{age:1}) 查询指定列
```
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/mongodb-FindWhere-1.png">

### 10.3 findOne
查询匹配结果的第一条数据
**语法**
```
db.collection_name.findOne()
```
**实例**
```
db.worker.findOne()
```
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/mongodb-baoCun-3.png">

### 10.3 find().count()
查询匹配结果的数目
![db7](http://odowb0dhc.bkt.clouddn.com/db7.png)
## 11. 条件操作符
条件操作符用于比较两个表达式并从mongoDB集合中获取数据

<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/mongodb-where-1.png">

### 11.1 大于操作符
**语法**
```
db.collectoin_name.find({<key>:{$gt:<value>}})
```

**参数**
- collectoin_name  集合名称
- key   字段
- value   值

**实例**
```
db.worker.find({age:{$gt:30}}) //查询age 大于 30的数据
```
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-2.png">


### 11.2 大于等于操作符
**语法**
```
db.collectoin_name.find({<key>:{$gte:<value>}})
```

**参数**
- collectoin_name 集合名称
- key  字段
- value  值

**实例**
```
db.worker.find({age: {$gte: 30}}) 查询age 3大于等于30 的数据
```
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-4.png">

### 11.3 小于操作符
**语法**
```
db.collectoin_name.find( {<key>:{$lt:<value>}})
```

**参数**
-  collectoin_name集合名称
-  key 字段
-  value 值

**实例**
```
db.worker.find({age: {$lt: 30}}) 查询age 小于30的数据
```
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-3.png">

### 11.4 小于等于操作符
**语法**
```
db.collectoin_name.find({<key>:{$lte:<value>}})
```

**参数**
- collectoin_name集合名词
- key字段
- value值

**实例**
```
db.worker.find({age: {$lte: 30}}) 查询age 小于等于30的数据
```
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-5.png">

### 11.5 同时使用 $gte和$lte
**语法**
```
db.collectoin_name.find({<key>:{$gte:<value>},<key>:{$lte:<value>}})
```

**参数**
- collectoin_name 集合名称
- key 字段
- value 值

**实例**
查询age 大于等于 30 并且 age 小于等于 50  的数据
```
db.worker.find({age: {$gte: 30, $lte: 50}})
```
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-6.png">

### 11.6 等于
**语法**
```
db.collectoin_name.find({<key>:<value>,<key>:<value>})
```

**参数**
- collectoin_name集合名词
- key字段
- value值

**实例**
查询age = 30的数据
```
db.worker.find({"age": 30})`
```
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-1.png">

### 11.7 使用 _id进行查询
**语法**
```
db.collectoin_name.find({"_id" : ObjectId("value")})
```

**参数**
- value  `_id`的值

**实例**
查询_id是 562af23062d5a57609133974 数据
```
db.worker.find({"_id" : ObjectId("562af23062d5a57609133974")})
```
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-9.png">

### 11.8 查询结果集的条数
**语法**
```
db.collectoin_name.find().count()
```

**参数**
- collectoin_name 集合名称

**实例**
```
db.worker.find().count()
```
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-17.png">

### 11.9 正则匹配
**语法**
```
db.collection.find({key:/value/})
```

**参数**
- collectoin_name 集合名称
- key 字段
- value 值

**实例**
查询name里包含zhang的数据
```
db.worker.find({name:/value/})
```
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-10.png">

查询某个字段的值当中是否以另一个值开头
```
db.worker.find({name:/^zhang/})
```
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-11.png">

## 12. 与和或
### 12.1 and
find方法可以传入多个键(key)，每个键(key)以逗号隔开

**语法**
```
db.collection_name.find({key1:value1, key2:value2})
```

**实例**
查询name是zhangRenYang并且age是30的数据
```
db.worker.find({name:'zhangRenYang',age:30})
```
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/mongodb-andfind-1.png">

### 12.2 or
**语法**
```
db.collection_name.find(
   {
      $or: [
         {key1: value1}, {key2:value2}
      ]
   }
)
```

**实例**
查询age = 30 或者 age = 50  的数据
```
db.worker.find({$or:[{age = 30},{age = 50}]})
```
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-8.png">

### 12.3 and和or联用
**语法**
```
db.collection_name.find(
   {
     key1:value1,
     key2:value2,
     $or: [
         {key1: value1},
         {key2:value2}
     ]
   }
)
```

**实例**
查询 name是zhangRenYang 并且 age是30 或者 age是 50 的数据
```
db.worker.find({name:'zhangRenYang',$or:[{age:30},{age:50}]})
```
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/mongodb-andOr-1.png">

## 13. 分页查询
### 13.1 limit
读取指定数量(前几条)的数据记录
**语法**
````
db.collectoin_name.find().limit(number)
```
** 参数**
- collectoin_name集合
- number读取的条数

**实例**
查询前3条数据
```
db.worker.find().limit(3)
```
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-14.png">


### 13.2 skip
跳过指定数量的数据，skip方法同样接受一个数字参数作为跳过的记录条数
**语法**
```
db.collectoin_name.find().skip(number)
```
**参数**
- collectoin_name集合
- number跳过的条数

**实例**
查询3条以后的数据
```
db.worker.find().skip(3)
```
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-15.png">

### 13.3 skip+limit
通常用这种方式来实现分页功能
**语法**
```
db.collectoin_name.find().skip(skipNum).limit(limitNum)
```
**参数**
- collectoin_name 集合名称
- skipNum 跳过的条数
- limitNum 限制返回的条数

**实例**
查询在4-6之间的数据
```
db.worker.find().sort({age:-1})
```
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-16.png">

### 13.4 sort排序
sort()方法可以通过参数指定排序的字段，并使用 1 和 -1 来指定排序的方式，其中 1 为升序排列，而-1是用于降序排列。
**语法**
```
db.collectoin_name.find().sort({key:1})
db.collectoin_name.find().sort({key:-1})
```
**参数**
- collectoin_name集合
-  key表示字段

**实例**
查询出并升序排序 {age:1}  age表示按那个字段排序 1表示升序
```
db.worker.find().sort({age:1})
```
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-12.png">

## 操作mongodb简单流程
### 创建存储数据的文件夹
```
$ mkdir -p data/db
```
### 启动mongodb
```
$ mongod --dbpath=./data/db
```
### 开启mongo shell
```
$ mongo
```
### 创建一个数据库
```
$ use digicity-express-api
```
数据库是 mongodb 中的顶级存储单位，之下一级就是 **集合** 。
### 创建一个集合
```
$ db.createCollection(‘posts’)
```
### 插入数据记录
一个集合（例如，posts ），里面可以插入多个数据记录。
```
$ db.posts.insert({title: 'myTitle', content: 'myContent'})
```
### 查看集合中的所有记录
```
$ db.posts.find()
```
### 修改一条记录（了解内容）
```
db.posts.update({_id: ObjectId('xxx')}, {$set: {title: 'mongodb'}})
```
### 删除一条记录
```
db.posts.remove({_id: ObjectId('xxx')})
```
### 删除 posts 集合中的所有记录
```
db.posts.remove({})
```
### 删除数据库
假设我们的数据库叫做 digicity-express-api
```
use digicity-express-api
db.dropDatabase()
```
## 用JS代码操作mongodb
我们主要基于一个JS库的帮助,[mongoose](http://mongoosejs.com/),它可以作为一个npm的包来安装

解释一下，一个**js库**就是一组**js接口**的集合．库，英文翻译为library．

![002-mongoose.png](https://github.com/mengmeng183/mengmeng183.github.io/blob/master/myidoc/static/img/002-mongoose.png?raw=true)

下面我们来动手做一个 express+mongoose 的小 demo 。

### 先写一个最简单的 express 程序
index.js 如下：
```
var express = require('express');
var app = express();

app.post('/posts', function(req, res){
  console.log('hello');
});

app.listen(3000, function(){
  console.log('running on port 3000.....');
});
```
相应的 curl 测试命令是
```
curl --request POST localhost:3000/posts
```
如果可以在运行 `node index.js` 的位置看到 `hello` 表示我们这一步胜利完成。

![003-curl.png](https://github.com/mengmeng183/mengmeng183.github.io/blob/master/myidoc/static/img/003-curl.png?raw=true)

###　安装mongoose
作为一个npm包进行安装，[link](https://www.npmjs.com/package/mongoose)
```
npm install --save mongoose
```
### 在 js 代码中导入 mongoose
```
var mongoose = require('mongoose');
```
### 进行数据库的连接
```
mongoose.connect('mongodb://localhost:27017/express-api');
```
mongoose.connect　接口用来连接我们系统上安装的 mongodb　数据库

如何定位数据库的所在位置
- 一种逻辑上可行的方案，就是用数据存储的文件夹的位置（比如我们前面采用的　data/db　文件夹），但是实际上 mongodb有其他方案
- mongodb　的软件，运行起来类似一个网站，用链接来访问.(mongodb://localhost:27017)

但是，链接之后，要跟上具体的数据库的名字．我们每次链接都是链接到一个数据库．比如我们这是就是express-api(一般与项目名同名)．

如何验证链接成功呢？用下面的代码
```
var db = mongoose.connection;
db.on('error', console.log);
db.once('open', function() {
  console.log('success!')
});
```
看到 `success!` 字样表示链接成功。
###  定义数据的概要 Schema
数据天然的具有一定的结构，比如，人员名单中，自然的会涉及姓名，年龄，籍贯等信息．在 mongodb　这里，一个人员的信息会被作为一条记录来保存．所有信息的类型会对应成字段名，由于是跟计算机打交道，每个字段还要涉及它的数据类型(number,string...).

那么　Schema 就是用来规定一个记录的各个字段的，字段名＋数据类型的.

```
var mongoose = require('mongoose');
var Schema = mongoose.Schema;

var PostSchema = mongoose.Schema({
   title:{ type:String, required:true},
   category:{type:String},
   content:{type:String}
  },
  { timestamps: true }
);
```
上面的代码，规定出了我们的记录能够保存哪些数据．
### 创建数据模型 model
数据库的结构是，一个数据库，里面会包含多个集合，一个集合会包含多条数据记录．

那么现在，我们数据要往哪个数据库中存？这个问题已经通过前面的`mongoose.connect(xxx)`语句指定了．

但是数据要保存到哪个集合还没有指定．所以我们的 model 创建语句如下
```
var Post = mongoose.model('Post',PostSchema);
```
上面`.model()`的第一个参数，`Post`就为我们指定了集合的名字，会对应数据库中的 posts 这个集合．第二个参数是数据 Schema ，就是前在我们定义的．

到这里，所有数据存储的基础设施全部就绪．
### 实例化 model 得到数据对象
现在我们要把实际要存储的数据放到一个　model 的实例（对象）之中了．
```
var post = new Post({title:"myTitle",category:"myCategory",content:"myContent"});
```
### 对象之上呼叫 save()
```
post.save(function(err){
  if(err) return console.log(err);
  console.log('saved!');
})
```
这样可以把数据保存到数据库中．
