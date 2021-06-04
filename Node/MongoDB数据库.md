# MongoDB数据库

连接和退出数据库

```shell
#连接
mongo
#退出
exit
```

基本命令

- 查看所有数据库

```sh
show dbs
```

- 查看当前操作的数据库

```sh
db
```

- 切换到指定数据库，如果没有会新建

```sh
use 数据库名称
```

- 插入数据

```shell
db.students.insertOne({"name":"Jack"})
```

- 显示当前数据库的所有集合

```shell
show collections
```

- 查询集合中的所有数据

```sh
db.students.find()
```

通过 mongoose 操作 MongoDB数据库

```javascript
//引包
const mongoose = require('mongoose');

//连接 MongonDB 数据库
mongoose.connect('mongodb://localhost:27017/test', {useNewUrlParser: true, useUnifiedTopology: true});

//设计数据库
//MongonDB 是动态的，非常灵活，在代码中设计数据库
//mongoose 设计编写过程非常简单
/*
* 表名：Cat
* 数据结构
* */
const Cat = mongoose.model('Cat', { name: String });

//实例化 Cat
const kitty = new Cat({ name: 'Zildjian' });

//持久化保存 kitty 实例
kitty.save().then(() => console.log('meow'));
```

基本概念

- 可以有多个数据库
- 一个数据库可以有多个集合（表）
- 一个集合可以有多个文档（表记录）
- 文档结构很灵活，没有限制

#### 官方指南

设计 Schema 发布 Model

```javascript
var mongoose = require('mongoose')
//使用架构
var Schema = mongoose.Schema

//1.连接数据库
mongoose.connect('mongodb://localhost:27017/itcast', {useNewUrlParser: true, useUnifiedTopology: true});

//2.设计集合结构(表结构)
var userSchema = new Schema({
  username: {
    type: String,
    reuired: true //约束，不能为空
  },
  passworld: {
    type:String,
    required: true
  },
  email: {
    type: String
  }
})

//3.将集合结构发布为模型
/*
* mongoose.model 方法 用来将一个架构发布为 model
* 第一个参数：大写名词单数，mongoose 会自动转成 小写复数 的集合名称
* 第二个参数：架构 Schema
* 返回值：模型构造函数
* */
const User = mongoose.model('User', userSchema)

//4.使用构造函数操作 users 集合中的数据

```

##### 增加数据

```javascript
var admin = new User({
  username: 'admin',
  passworld: '123456',
  email: '123.com'
})
//持久化
admin.save((err,res) => {
  if (err) {
    console.log('保存失败');
  } else{
    console.log('保存成功');
    console.log(res);
  }
})
```

##### 查询

- 查询所有

```javascript
User.find((err,res) => {
  if (err) {
    console.log('查询失败');
  }else {
    console.log(res);
  }
})
```

- 按条件查询

```javascript
User.find({
  username: 'zs'
},(err,res) => {
  if (err) {
    console.log('查询失败');
  }else {
    console.log(res);
  }
})
```

- 按条件查询单个

```javascript
User.findOne({
  username: 'zs'
},(err,res) => {
  if (err) {
    console.log('查询失败');
  }else {
    console.log(res);
  }
})
```

##### 删除数据

- 根据条件删除所有

```javascript
ser.remove({
  username: 'zs'
},(err,res) => {
  if (err) {
    console.log('删除失败');
  }else {
    console.log('删除成功');
  }
})
```

- 根据条件删除一个

```javascript
User.findOneAndRemove({
  username: 'jack'
},(err,res) => {
  if (err) {
    console.log('删除失败');
  }else {
    console.log('删除成功');
  }
})
```

- 根据 id 删除一个

```javascript
User.findByIdAndRemove('6043507770dc2332b4a15877',(err,res) => {
  if (err) {
    console.log('删除失败');
  }else {
    console.log('删除成功');
  }
})
```



##### 更新数据

- 根据 id 更新一个

```javascript
User.findByIdAndUpdate('60433875f3065e27c05bb60b',{
  passworld: '99999999'
},(err,res) => {
  if (err) {
    console.log('更新失败');
  }else {
    console.log('更新成功');
  }
})
```

- 根据条件更新一个

```javascript
User.findOneAndUpdate({
  username: 'zs'
},{
  passworld: '555555'
},(err,res) => {
  if (err) {
    console.log('更新失败');
  }else {
    console.log('更新成功');
  }
})
```

