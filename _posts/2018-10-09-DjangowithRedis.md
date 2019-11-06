---
layout:     post
title:      Django项目中使用Redis
subtitle:    "Django，Redis"
date:       2018-10-09
author:     Cosmo-Ma
header-img: img/post-default.jpg
catalog: true
tags:
    - Python
---

## 1 redis 
Redis 是一个 key-value 存储系统，常用于缓存的存储。django-redis 基于 BSD 许可, 是一个使 Django 支持 Redis cache/session 后端的全功能组件.
### 1.1 为何要用 django-redis ?
- 持续更新
- 本地化的 redis-py URL 符号连接字符串
- 可扩展客户端
- 可扩展解析器
- 可扩展序列器
- 默认客户端主/从支持
- 完善的测试
- 已在一些项目的生产环境中作为 cache 和 session 使用
- 支持永不超时设置
- 原生进入 redis 客户端/连接池支持
- 高可配置 ( 例如仿真缓存的异常行为 )
- 默认支持 unix 套接字
- 支持 Python 2.7, 3.4, 3.5 以及 3.6
## 2 redis 的使用
### 2.1 安装
安装 django-redis 最简单的方法就是用 pip :

``` javascript
pip install django-redis
```
### 2.2 作为 cache backend 使用配置
为了使用 django-redis , 你应该将你的 django cache setting 改成这样:

``` accesslog
CACHES = {
    "default": {
        "BACKEND": "django_redis.cache.RedisCache",
        "LOCATION": "redis://127.0.0.1:6379/1",
        "OPTIONS": {
            "CLIENT_CLASS": "django_redis.client.DefaultClient",
        }
    }
}
```
为了更好的互操作性并使连接字符串更加 “标准”, 从 3.8.0 开始 django-redis 使用 redis-py native url notation 作为连接字符串.

``` groovy
redis://[:password]@localhost:6379/0
rediss://[:password]@localhost:6379/0
unix://[:password]@/path/to/socket.sock?db=0
```
支持三种 URL scheme :
- redis://: 普通的 TCP 套接字连接
- rediss://: SSL 包裹的 TCP 套接字连接
- unix://: Unix 域套接字连接
### 2.3 作为 session backend 使用配置
Django 默认可以使用任何 cache backend 作为 session backend, 将 django-redis 作为 session 储存后端不用安装任何额外的 backend

``` makefile
SESSION_ENGINE = "django.contrib.sessions.backends.cache"
SESSION_CACHE_ALIAS = "default"
```
### 2.4 使用
好了，现在连接和配置都已经完成了，那么在项目中该如何使用呢？接下来看下面这段例子吧。

``` sql
from django.conf import settings
from django.core.cache import cache
#read cache user id
def read_from_cache(self, user_name):
    key = 'user_id_of_'+user_name
    value = cache.get(key)
    if value == None:
        data = None
    else:
        data = json.loads(value)
    return data
#write cache user id
def write_to_cache(self, user_name):
    key = 'user_id_of_'+user_name
    cache.set(key, json.dumps(user_name), settings.NEVER_REDIS_TIMEOUT)
```
通过上面的这两个方法就可以实现对redis的读取操作了，只需要将需要的字段当参数传入到方法中就好了。