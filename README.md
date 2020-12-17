# compus-admin

## front

> 这是一个极简的 vue admin 管理后台。它只包含了 Element UI & axios & iconfont & permission control & lint，这些搭建后台必要的东西。

[线上地址](http://panjiachen.github.io/vue-admin-template)


目前版本为 `v4.0+` 基于 `vue-cli` 进行构建。


## 基础模板

- [vue-admin-template](https://github.com/PanJiaChen/vue-admin-template)

## 指导课程
- [校园管理项目实训](https://www.jianshu.com/c/2de175e814cc)

## 指导老师
- [简书@去年的牛肉](https://www.jianshu.com/u/b7ea376b2dca)

## Build Setup

```bash
# 克隆项目
git clone https://github.com/aoteman-web/Campus-Admin.git

# 进入项目目录
cd campus-admin/front

# 安装依赖
npm install

# 建议不要直接使用 cnpm 安装以来，会有各种诡异的 bug。可以通过如下操作解决 npm 下载速度慢的问题
npm install --registry=https://registry.npm.taobao.org

# 启动服务
npm run dev
```

浏览器访问 [http://localhost:9528](http://localhost:9528)

## backstage

1、在 [mongodb](https://account.mongodb.com/) 搭建云端服务器

搭建[教程](https://blog.csdn.net/aoteman_web/article/details/111166499) ：https://blog.csdn.net/aoteman_web/article/details/111166499

2、构建koa2项目

```bash
# 全局安装koa-generator
npm install -g koa-generator

# 构建koa2项目
cd campus-admin/backstage

# 安装依赖
npm install

# 启动服务
npm run dev
```
3、连接数据库（服务器）

新建一个db目录，在db/config.js文件下输入以下连接代码
```javascript
module.exports = {
    dbs: 'mongodb+srv://<username>:<password>@cluster0.mw8jo.mongodb.net/<databaseName>?retryWrites=true&w=majority'
}
```
4、添加/修改配置文件

db/models/user.js
```javascript
const mongoose = require('mongoose')
const feld={
    name: String,
    age: Number,
    //人物标签
    labels:Number
}
//自动添加更新时间创建时间:
let personSchema = new mongoose.Schema(feld, {timestamps: {createdAt: 'created', updatedAt: 'updated'}})
module.exports= mongoose.model('User',personSchema)
```

app.js
```javascript
const mongoose = require('mongoose')
const dbconfig = require('./db/config')
mongoose.connect(dbconfig.dbs, {useNewUrlParser: true,useUnifiedTopology: true})
const db = mongoose.connection
db.on('error', console.error.bind(console, 'connection error:'));
db.once('open', function() {
  console.log('mongoose 连接成功')
});
```
出现以下界面即代表连接数据库成功
https://riyugo.com/i/2020/12/17/farrab.png

## 部分页面
首页
https://riyugo.com/i/2020/12/17/fj6hqz.png

添加学院
https://riyugo.com/i/2020/12/17/fj6ddx.png

学院管理
https://riyugo.com/i/2020/12/17/fj6g0b.png

