# MongoDB 新手快速入门

整理自尚硅谷mongodb入门和菜鸟教程

 _提醒：按最新官方文档为准。比如在3.2之后新加了很多新方法，鼓励使用新方法。_

## 安装 

安装流程见官网

重要概念区分：

- `mongod` 启动服务器

- `mongo` 启动客户端

## 图形界面

robo 3T

## 术语

- database => db

- collection == table
- document == row
- field == column
- index
- primary key

## 操作

`show dbs`

`show databases`

`use <db>`

`show collections`

不需要创建表，插入行就能自动创建表

同理，删除所有表自动删除库

`db.<collection>.drop()`

## CRUD

### 查 read

`db.<collection>.find({})`

`db.<collection>.find()`

`db.<collection>.find({name:"xxx"})`

`db.<collection>.find().limit(<num>).skip(<offset>)` #limit 和skip可以互换#

`db.<collection>.find({},{xx:1, _id:0})` #选择性显示

`db.<collection>.find({<field>:{$gt:xx,$lt:xx}})`#删选，默认&&

`db.<collection>.find({$or:[{<field>:{$gt:xx},{<field>:{$gt:xx}]})`

### 增 create

`db.<collection>.insert({xxx:xxx})`

### 删 delete

`db.<collection>.delete({})`#全部删除也必须带花

括号参数

### 改 update

`db.<collection>.update({xx:xx},{$set:{xx:xx}})`#默认重置document，因此修改必须用$set

`db.<collection>.update({xx:xx},{$push:{xx:xx}})`#添加到array

## 其他操作

###聚合 aggregation

基本逻辑是mapreduce逻辑，`$match`,`$group`,是典型的pipeline（也可叫做funtional）操作

其他操作函数

- `count()`

- `sort({field1:1, field2:-1})` 一定发生在skip和limit之前
- `$inc`

### 高级话题

- index
- 分片、备份、监控
- 原子操作
- 正则表达式

## Mongoose

### 概念

- Schema - 理解为约束，或者OD Mapping 中的O
- Model - 理解为table 或者collection

### 使用

```javascript
const mongoose = require('mongoose')

//init schema and model
const Schema = new mongoose.Schema;
const theSchema = new Schema({
  field1:String,
  field2:Int
})
const theModel = mongoose.model('item', theSchema, 'items');
##### module.exports = theModel;

##### const Item = require('item');
//init db
const db = 'mongodb://localhost:27017/db';
mongoose.connect(db, err=>{})

//CRUD
Item.find({}).exec(...)
Item.findById(...).exec(...)
item.save(function(err, item){s})

```

