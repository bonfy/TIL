# 退出程序

> 2017-09-12

## peewee 的default 千万不要加 ()

在peewee 里面使用uuid，应该是蛮简单的

```python
class BaseModel(Model):

    object_id = UUIDField(default=uuid.uuid1())
    created_at = DateTimeField(default=datetime.datetime.now())
```

结果每次插入数据库的时候发现所有的 object_id 都是一样的，这个很奇怪啊，后来想了半天，估计是()惹的祸，导致每次初始化的时候就执行了,所以下次注意设置的时候还是不要带上()

正确的写法：

```python
class BaseModel(Model):
    
    object_id = UUIDField(default=uuid.uuid1)
    created_at = DateTimeField(default=datetime.datetime.now)
```

## peewee 的 create_tables

注意 create_tables 这个func,后面传的参数为list, 结果我总是这么传 create_tables(Class1, Class2), 结果报了一些莫名
的错误

正确的写法：

```python
db.create_tables([Class1, Class2])
```


