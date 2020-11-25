hive和spark





##### 删除了分区但是数据没有被删除

使用大于小于的方式只会删除元数据信息，不会删除数据

```
alter table  tablename drop  partition(dt<=20200101);


```



##### 增加了列在在hive中不生效

修改表结构，在hive的历史分区中不生效，只有修改了列之后的生成的分区生效，修复的方式对表的每个分区都使用alter语句增加字段名





## 常见函数

> 从json字符串中获取指定字段值

```
get_json_object(jsonstr,'$.colname')
```

注意大小写，这里的json字段是大小写敏感的

