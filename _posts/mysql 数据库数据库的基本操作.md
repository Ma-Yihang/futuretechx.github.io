---
title: mysql 数据库（二）数据库的基本操作
tags: 用户管理，添加权限，创建，显示，使用数据库
grammar_cjkRuby: true
---
#### 一 数据库操作
1 显示数据库：`show databases;`
![enter description here](./images/1546673531355.png)
默认数据库：
　　mysql - 用户权限相关数据
　　test - 用于用户测试数据
　　information_schema - MySQL本身架构相关数据
2 创建数据库：

``` python
# utf-8
CREATE DATABASE 数据库名称 DEFAULT CHARSET utf8 COLLATE utf8_general_ci;
 
# gbk
CREATE DATABASE 数据库名称 DEFAULT CHARACTER SET gbk COLLATE gbk_chinese_ci;
```
![enter description here](./images/1546673822646.png)
3 使用数据库 ：`use db_name;`
``` cmd
mysql> use db2;
Database changed
mysql>
```
4 显示当前使用的数据库中所有的表：show tables;

``` javascript
mysql> show tables;
Empty set (0.00 sec)

mysql>
```
5 用户管理

``` javascript
创建用户
    create user '用户名'@'IP地址' identified by '密码';
删除用户
    drop user '用户名'@'IP地址';
修改用户
    rename user '用户名'@'IP地址'; to '新用户名'@'IP地址';;
修改密码
    set password for '用户名'@'IP地址' = Password('新密码')
  
PS：用户权限相关数据保存在mysql数据库的user表中，所以也可以直接对其进行操作（不建议）
```
创建用户的时候也可以约束IP地址，比如下面的：

``` cmd
create user 'cosmo'@'192.168.1.1' identified by '123123';
# IP是：192.168.1.X
create user 'cosmo'@'192.168.1.%' identified by '123123';
#所有主机都可以
create user 'cosmo'@'%' identified by '123123';
```
6 授权管理

``` javascript
show grants for '用户'@'IP地址'                -- 查看权限
grant  权限 on 数据库.表 to   '用户'@'IP地址'      -- 授权
revoke 权限 on 数据库.表 from '用户'@'IP地址'       -- 取消权限
查看，插入，更新权限
grant select,insert,update  on db1.t1 to 'cosmo'@'%';
所有权限
grant all privileges  on db1.t1 to 'cosmo'@'%';
删除所有权限
revoke all privileges on db1.t1 from 'cosmo'@'%';
```

> 对于权限参数的说明：
> all privileges  除grant外的所有权限
            select          仅查权限
            select,insert   查和插入权限
            ...
            usage                   无访问权限
            alter                   使用alter table
            alter routine           使用alter procedure和drop procedure
            create                  使用create table
            create routine          使用create procedure
            create temporary tables 使用create temporary tables
            create user             使用create user、drop user、rename user和revoke  all privileges
            create view             使用create view
            delete                  使用delete
            drop                    使用drop table
            execute                 使用call和存储过程
            file                    使用select into outfile 和 load data infile
            grant option            使用grant 和 revoke
            index                   使用index
            insert                  使用insert
            lock tables             使用lock table
            process                 使用show full processlist
            select                  使用select
            show databases          使用show databases
            show view               使用show view
            update                  使用update
            reload                  使用flush
            shutdown                使用mysqladmin shutdown(关闭MySQL)
            super                   􏱂􏰈使用change master、kill、logs、purge、master和set global。还允许mysqladmin􏵗􏵘􏲊􏲋调试登陆
            replication client      服务器位置的访问
            replication slave       由复制从属使用
对于数据库：
        对于目标数据库以及内部其他：
            数据库名.*           数据库中的所有
            数据库名.表          指定数据库中的某张表
            数据库名.存储过程     指定数据库中的存储过程
            *.*                所有数据库
对于用户和IP：
            用户名@IP地址         用户只能在改IP下才能访问
            用户名@192.168.1.%   用户只能在改IP段下才能访问(通配符%表示任意)
            用户名@%             用户可以再任意IP下访问(默认IP地址为%)


----------
7 修改密码

``` javascript
# 启动免授权服务端
mysqld --skip-grant-tables

# 客户端
mysql -u root -p

# 修改用户名密码
update mysql.user set authentication_string=password('666') where user='root';
flush privileges;
```

