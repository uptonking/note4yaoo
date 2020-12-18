---
title: cli-database
tags: [cli, database]
created: '2020-12-18T04:28:11.723Z'
modified: '2020-12-18T04:28:56.828Z'
---

# cli-database

## mysql

- 操作tips
  - 导入数据库
    - 进入mysql数据库控制台, use 数据库名， source db.sql

- 查询相关

``` SQL
-- 基本查询语句
select 字段列表 from 表名 where 条件 group by 字段 order by 字段；

-- 简单避免重复数据查询
select distinct 字段名1，字段名2 from  table_name;
```

- database相关

``` SQL
-- 查看已存在的数据库：
show databases;

--查看当前连接的数据库
select database();

-- 创建新数据库
create database testdb;

-- 删除数据库
drop database xxx; 
```

- table相关

``` SQL
-- use数据库后，可查看所有表
show tables;
show tables like 't_%';

-- 查看表定义
describe t_user;

-- 显示指定表的DDL创建语句
show create table t_user;

-- 创建一张表
create table t_user (
  id int, 
  name varchar(20)
  );

-- 清空表内容
TRUNCATE TABLE "表格名";

-- 插入一条完整数据记录
insert into 表名 values (值列表)；

-- 插入多条完整数据记录
insert into 表名 values（字段列表)， （字段列表), ......;

-- 插入一条部分数据记录
insert into t_user(id, name) values(1, "A");
insert into 表名（字段列表）values (值列表);

-- 插入多条部分数据记录
insert into 表名(字段列表) values（值列表)， （值列表), ......;

-- 更新部分数据记录
update table_name set 字段名1 = value1, 字段名2 = value2  where 条件;

-- 删除部分数据记录
delete from table_name where 条件；

-- 修改表名
alter table old_name rename new_name;
rename table old_name to new_name;

-- 在表的最后一个位置增加字段
alter table xxx add 属性名 数据类型；

-- 在表的第一个位置增加字段
alter table xxx add 属性名 数据类型 first;

-- 在表的某个位置增加字段
alter table xxx add 属性名 数据类型 after  表中已存在属性名；

-- 给表的某个字段增加默认值
alter table xxx modify 属性名 数据类型  default yy；

-- 删除表中某个字段
alter table xxx drop 属性名；
```

- 安装mysql
  - sudo apt install mysql-server
  - systemctl status mysql
  - sudo mysql_secure_installation
  - sudo systemctl restart mysql
- mysql shell
  - sudo mysql -u root -p
  - \q、quit、exit 是退出
  - status查看mysql配置信息
- 卸载mysql
  - sudo apt autoremove mysql* --purge

``` SQL
-- ERROR 1698 (28000): Access denied for user 'root'@'localhost'
  -- 若异常在命令行出现，则需要在命令前加上sudo，如sudo mysql -u root -p
  -- 若异常在dbeaver出现，则需要修改该用户或新建一个用户，使其验证方式为密码
-- MySQL8更改了root账户的授权方式，默认是auth_socket。也就是说需要通过 Unix socket 文件来验证所有连接到localhost的用户
-- 设置允许远程登录，'root'@'localhost'和'root'@'%' 是两个不同的用户
  -- 为了更清晰，最好还是新建个其他用户名
CREATE USER 'root'@'%' IDENTIFIED BY 'password';
```

- mysql元信息

``` SQL
-- 查看mysql版本及配置信息
status;

-- 查看指定数据库中的表
show tables from mysql;

-- 查看数据库连接信息
  -- 如果是root帐号，能看到所有用户的当前连接。如果是其他普通帐号，则只能看到自己占用的连接
  -- show processlist只能列出当前100条。如果想全部列出，需用full
show processlist;
show full processlist;

-- 查看字符集编码
show variables like 'character_set%';
```

- 用户权限相关

``` SQL
--查看当前登录用户
select user();

-- 查看现有用户
select user, host from mysql.user;

-- 查看及修改加密方式
select user,plugin from user;

-- 创建新用户
CREATE USER 'testuser'@'localhost' IDENTIFIED BY '111111'; 
CREATE USER 'testuser'@'%' IDENTIFIED BY '111111'; 

-- 对新增的用户更改加密方式和密码
ALTER USER 'testuser'@'localhost' IDENTIFIED WITH mysql_native_password BY '111111';
ALTER USER 'testuser'@'%' IDENTIFIED WITH mysql_native_password BY '111111';

GRANT ALL ON testdb.* TO 'testuser'@'%' WITH GRANT OPTION;
GRANT ALL ON *.* TO 'testuser'@'%' WITH GRANT OPTION;

-- 对于8.0之前的版本
GRANT ALL PRIVILEGES ON *.* TO 'admin'@'localhost' IDENTIFIED BY '111111';
```

## postgresql

- 操作tips
  - 备份单个数据库
    - pg_dump -h localhost -U postgres(用户名) 数据库名(缺省时同用户名) ()  > dum.sql
    - pg_dump -U postgres(用户名) 数据库名 | gzip > /data/dum.sql.gz
  - 恢复单个数据库
    - psql -U postgres(用户名)  数据库名(缺省时同用户名) < dum.sql
    - gunzip < /data/dum.sql.gz | psql -U postgres(用户名) 数据库名
  - 备份所有数据库
    - pg_dumpall > db.out
  - 恢复所有数据库
    - psql -f db.out postgres
    - 执行这个命令的时候连接到哪个数据库无关紧要，因为pg_dumpall创建的脚本将会包含恰当的创建和连接数据库的命令
  - 备份单表操作
    - pg_dump -U postgres -h localhost -p 5432 -t staff -f staff.sql yjl（表示数据库名称）
  - 恢复数据单表操作
    - psql -U postgres -h localhost -p 5432 -d product -f staff.sql  

- 查询相关

``` SQL
-- 基本查询
SELECT * FROM user_tbl;

-- 返回第十条开始的5条记录
select * rom tabname limit 5 offset 10;

```

- database相关

``` SQL
-- 创建新数据库
create database testdb owner testuser;
CREATE DATABASE dbName WITH  OWNER = postgres TEMPLATE = template0 ENCODING = 'UTF8';

-- 和 CREATE DATABASE 相同，也支持dropdb
createdb db_name -O db_pwd  -E UTF8 -e

```

- table相关

``` SQL
-- 创建

-- # 创建新表 
CREATE TABLE user_tbl(name VARCHAR(20), signup_date DATE);

-- 自增id，使用serial伪类型
CREATE TABLE table_name(
    id SERIAL
);
-- 相当于
CREATE SEQUENCE table_name_id_seq;
CREATE TABLE table_name (
    id integer NOT NULL DEFAULT nextval('table_name_id_seq')
);
ALTER SEQUENCE table_name_id_seq
OWNED BY table_name.id;

-- # 插入数据 
INSERT INTO user_tbl(name, signup_date) VALUES('张三', '2013-12-22');
-- # 更新数据 
UPDATE user_tbl set name = '李四' WHERE name = '张三';

-- # 删除记录 
DELETE FROM user_tbl WHERE name = '李四' ;
-- 清空表
delete from tablename

-- # 添加栏位 
ALTER TABLE user_tbl ADD email VARCHAR(40);
alter table [表名] add column [字段名] [类型];

-- # 更新结构 
ALTER TABLE user_tbl ALTER COLUMN signup_date SET NOT NULL;
-- # 更名栏位 
ALTER TABLE user_tbl RENAME COLUMN signup_date TO signup;

-- # 删除栏位 
ALTER TABLE user_tbl DROP COLUMN email;
-- # 表格更名 
ALTER TABLE user_tbl RENAME TO backup_tbl;
-- 删除表主键
alter table 表名 drop CONSTRAINT 主键名称;

-- # 删除表格 
DROP TABLE IF EXISTS backup_tbl;
```

- 安装postgresql
  - sudo apt install postgresql postgresql-contrib
  - sudo -u postgres psql -c "SELECT version(); "
  - sudo -u postgres psql
    - 以Linux用户"postgres"的身份（此时只有该用户有psql命令）执行psql客户端
    - 这里系统用户名、数据库用户名、数据库名都为postgres，故可采用简写形式
  - sudo su - postgres
    - 切换用户身份和shell环境到postgres用户，注意要加sudo，若不加则要输入密码
- psql shell
  - psql -U testuser -d testdb -h 127.0.0.1 -p 5432
  - 修改数据库管理员的密码
    - alter user postgres with password '111111'; 
  - \q：退出
  - \l：列出所有数据库
  - \du：列出所有用户
  - \conninfo：列出当前数据库和连接的信息
  - \c [database_name]：连接其他数据库
  - \d：列出当前数据库的所有表格
  - \d [table_name]：列出某一张表格的结构
  - \password：设置密码

- 用户权限相关

``` SQL
-- 创建用户
create user testuser with password '111111';

-- 和 CREATE USER 相同，也支持dropuser
createuser test_user -P

-- 授权到用户
grant all privileges on database testdb to testuser;
```
