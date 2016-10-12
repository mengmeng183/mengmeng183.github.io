<h1 style="font-size: 40px;text-align:center;color: #007cdc;">
    mongoose
</h1>

[官网链接](http://mongoosejs.com/)

使用mongoose的前提是安装了mongodb和node.js

mongoose是node.js的库，使用时安装在项目内部安装
```
npm install --save mongoose
```

mongoose,是软件库，核心作用是数据模型对象化，是用来连接express和mongdb的,结合js代码使用

作用：把数据转化成js对象，以便我们可以用js代码来读写mongodb

### 第一步：确保mongodb已经启动，也就是确保mongo shell可以用
```
mongodb --dbpath=数据库路径
```
### 第二步：js代码中连接mongodb

> 每个项目只建立一个数据库，一个数据库中可有多外collection(集合)

**创建package.json文件**
```
echo {}>package.json //创建后package.json中是一个{}，空的对象
```
**在项目内安装mongoose**
```
npm install --save mongoose
```

**在项目内导入mongoose**
```
var mongoose = require('mongoose');
```
**与数据库建立连接**
```
mongoose.connect('mongodb://localhost:27017/data');//data为数据库名
```
/*index.js*/
```js
var mongoose = require('mongoose');//引用mongoose模块
mongoose.Promise = global.Promise; //有时命令行会提示有什么东西过期了，有一些垃圾提醒,加上它就没有了，必须放在connect前
mongoose.connect('mongodb://localhost:27017/data');//创建一个数据库连接,一但有数据保存数据库就会自动创建
var db = mongoose.connection; //db代表数据库，以后对db变量进行操作
db.on('error', console.error.bind(console, 'connection error:'));
db.once('open', function() {  //once是mongoose提供的接口
   console.log('connected!'); //后面的代码都会写到这个加调函数里
});
```
上面的代码，在命令行执行`node index.js`,在命令行打印`connected!`
### 第三步：建立数据Schema

Schema 数据概要，用来描述数据(文档document，一条记录record)结构,规定这个记录中有几个字段(field)，每个字段的名字(name,birthday...),以及字段类型(string,num...)

**了解Model模型的概念**
model是MVC之中的M，model通常会写成一个类，存放所有和数据直接相关的代码

MVC Model View Controller 模型 视图 控制器（软件架构）

/*index.js*/成功构建一条记录
```js
var mongoose = require('mongoose');
mongoose.connect('mongodb://localhost:27017/mongoose-api');//创建一个数据库连接,一但有数据保存数据库就会自动创建
var db = mongoose.connection;
db.on('error', console.error.bind(console, 'connection error:'));
db.once('open', function() {
  var catSchema = mongoose.Schema({
   name: String //定义一个属性name，类型为String
  });
  var cat = mongoose.model('cat', catSchema);//cat是数据记录的名字，是实际数据库中一条记录的名字,catSchema是数据记录的结构
  var kitty = new cat({ name: 'helloKitty' });
  console.log(kitty.name);//执行node index.js在命令行打印helloKitty
  kitty.save();//保存记录，执行完成后，数据库就有该数据了
});
```
创建一个`mongoose-api`数据库，数据库中有一个`cats`集合，集合中有一条记录`{ "_id" : ObjectId("57ec890239967118d8ec4690"), "name" : "helloKitty", "__v" : 0 }`

`var cat = mongoose.model('cat', catSchema);`第一个参数：模型对应的集合名称的单数，第二个参数：一条数据记录的结构[参考网站](http://mongoosejs.com/docs/models.html)

```js
var mongoose = require('mongoose');
mongoose.connect('mongodb://localhost:27017/mongoose-api');
var db = mongoose.connection;
db.on('error', console.error.bind(console, 'connection error:'));
db.once('open', function() {
  var userSchema = mongoose.Schema({
   userName: String,
   password:String,
   age:Number
  });
  var user = mongoose.model('user', userSchema);
  var mengmeng = new user({userName:'mengmeng',password:'123',age:12});
  console.log(mengmeng.userName,mengmeng.password,mengmeng.age);
  mengmeng.save();
});
```
在`mongoose-api`数据库增加一个`users`集合,集合中有一条记录`{ "_id" : ObjectId("57ecb636c1d1de21be1e7615"), "userName" : "mengmeng", "password" : "123", "age" : 12, "__v" : 0 }`

### 第四步：学会用js代码来增删改查

**Create 增**
1.定义schema
```js
var userSchema = mongoose.Schema({
 userName: String,
 password:String,
 age:Number
});
```
2.保存
```js
var mengmeng = new person({userName:'mengmeng',password:'123',age:12});
console.log(mengmeng.userName,mengmeng.password,mengmeng.age);
mengmeng.save(); //save()是异步的
```
**Read 查**
find() 写在db.once的回调函数中
```js
var result = user.find() //同步执行
```
```js
user.find().exec(function(err,users){ //异步执行(高手所用)，exec是执行的意思，find()返回一个对象，对象里有一个exec方法
    console.log(users);
})
```
**Update 更新**
```js
  mengmeng.userName='meng'
  mengmeng.password='abc'
  mengmeng.save()
```

```js
user.findById({_id: '57ecba5b0003da23c26e6f2b'},function(err,user){
    user.userName='rrr'
    user.save(function(err){
      console.log('更新了');
    })
  })
  //查找
  user.find().exec(function(err,users){ //异步执行
    console.log(users);
  })
```
上面最后查询到的是更新前的内容，解决办法是将查询放在save()的回调函数中
```js
//大写User表示是一个类，小写user表示是一个具体的对象
User.findById({_id: '57ecc883c11fff0d028ceab3'},function(err,user){
  user.userName='rrr'
  user.save(function(err){
    console.log('更新了');
    //查找
    User.find().exec(function(err,users){ //异步执行
      console.log(users);
    })
  })
})
```

**Remove 删**
```js
User.findById({_id: '57ecc883c11fff0d028ceab3'},function(err,user){
  user.userName='rrr'
  user.remove(function(err){
    console.log('删除了');
    //查找
    User.find().exec(function(err,users){ //异步执行
      console.log(users);
    })
  })
})
```
