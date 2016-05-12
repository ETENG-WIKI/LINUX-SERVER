# mongodb与mysql对比

传统的关系数据库一般由数据库（database）、表（table）、记录（record）三个层次概念组成，MongoDB是由数据库（database）、集合（collection）、文档对象（document）三个层次组成。MongoDB对于关系型数据库里的表，但是集合中没有列、行和关系概念，这体现了模式自由的特点。


# mongodb与mysql对比

| Mysql     | Mongodb     | 说明   |
|:--------|:---------|:-------|
| mysqld |mongod| 服务器守护进程|
|mysql|mongo|客户端工具|
|mysqldump|mongodump|逻辑备份工具|
|mysql|mongorestore|逻辑恢复工具|
|...|db.repairDatabase()|修复数据库|
|mysqldump|mongoexport|数据导出工具|
|source|mongoimport|数据导入工具|
|grant * privileges on *.* to …|Db.addUser(),Db.auth()|新建用户并权限|
|show databases|show dbs|显示库列表|
|Show tables|Show collections|显示表列表|
|Show slave status|Rs.status|查询主从状态|
|Create table users(a int, b int)|db.createCollection("mycoll", {capped:true,size:100000}) 另：可隐式创建表。|创建表|
|Create INDEX idxname ON users(name)|db.users.ensureIndex({name:1})|创建索引|
|Create INDEX idxname ON users(name,ts DESC)|db.users.ensureIndex({name:1,ts:-1})|创建索引|
|Insert into users values(1, 1)|db.users.insert({a:1, b:1})|插入记录|
|Select a, b from users|db.users.find({},{a:1, b:1})|查询表|
|Select * from users|db.users.find()|查询表|
|Select * from users where age=33|db.users.find({age:33})|条件查询|
|Select a, b from users where age=33|db.users.find({age:33},{a:1, b:1})|条件查询|
|select * from users where age<33|db.users.find({'age':{$lt:33}})|条件查询|
|select * from users where age>33 and age<=40|db.users.find({'age':{$gt:33,$lte:40}})|条件查询|
|select * from users where a=1 and b='q'|db.users.find({a:1,b:'q'})|条件查询|
|select * from users where a=1 or b=2|db.users.find( {$or:[{a:1},{b:2}]} )|条件查询|
|select * from users limit 1|db.users.findOne()|条件查询|
|select * from users where name like "%Joe%"|db.users.find({name:/Joe/})|模糊查询|
|select * from users where name like "Joe%"|db.users.find({name:/^Joe/})|模糊查询|
|select count(1) from users|Db.users.count()|获取表记录数|
|select count(1) from users where age>30|db.users.find({age: {'$gt': 30}}).count()|获取表记录数|
|select DISTINCT last_name from users|db.users.distinct('last_name')|去掉重复值|
|select * from users ORDER BY name|db.users.find().sort({name:-1})|排序|
|select * from users ORDER BY name DESC|db.users.find().sort({name:-1})|排序|
|EXPLAIN select * from users where z=3|db.users.find({z:3}).explain()|获取存储路径|
|update users set a=1 where b='q'|db.users.update({b:'q'}, {$set:{a:1}}, false, true)|更新记录|
|update users set a=a+2 where b='q'|db.users.update({b:'q'}, {$inc:{a:2}}, false, true)|更新记录|
|delete from users where z="abc"|db.users.remove({z:'abc'})|删除记录|
|...|db. users.remove()|删除所有的记录|
|drop database IF EXISTS test;|use test  ,db.dropDatabase()|删除数据库|
|drop table IF EXISTS test;|db.mytable.drop()|删除表/collection|
|...|db.addUser(‘test’, ’test’) |添加用户readOnly-->false|
|...|db.addUser(‘test’, ’test’, true) |添加用户readOnly-->true|
|..|db.addUser("test","test222")|更改密码|
|...|db.system.users.remove({user:"test"})或者db.removeUser('test')|删除用户|