

## spark函数官方文档

最好的资料就是官方文档，遇事不决看官方的[函数文档](http://spark.apache.org/docs/latest/api/sql/index.html)







## 新建表

#### 复制表结构

新建表，并且表结构和存在的表的结构完全相同，一般用于修复数据问题

```
create table newTableName like exitTableName
location 'xxxxxx';
```



## 常见函数

#### 从json字符串中获取指定字段值

```
get_json_object(jsonstr,'$.colname')
```

注意大小写，这里的json字段是大小写敏感的





## 踩坑

#### 删除了分区但是数据没有被删除

使用大于小于的方式只会删除元数据信息，不会删除数据

```
alter table  tablename drop  partition(dt<=20200101);


```



#### 增加了列在在hive中不生效

修改表结构，在hive的历史分区中不生效，只有修改了列之后的生成的分区生效，修复的方式对表的每个分区都使用alter语句增加字段名



