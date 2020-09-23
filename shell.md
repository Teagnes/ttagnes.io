# 记录用到的shell命令

## 日常维护



总结日常经常使用服务器时一些排查，运维的一些命令

### 解锁密码
```
# 使用root账户登录（如果你有权限）
# 查看密码状态
passwd -S username

# 解锁
passwd -u username

# 如果有登录失败次数限制，失败若干次之后会有锁定时间，不想等可以手动重置，
pam_tally2 --user=username --reset


```




### 使用ps找到对应进程并kill

```
ps -ef| grep xxx | grep -v grep | cut -c 9-15 |xargs kill -s 9

# grep xxx 含有关键字xxx的进程
# grep -v grep 去除含有关键字grep的进程
# cut -c 9-15  截取第9到15个字符，进程号
# xargs kill -s 9  将前面的结果作为kill的参数 

```
 简化版

```
pgrep xxx  | xargs kill -s 9

```

### nginx日志超时记录

```
cat access.log  | awk '{if($6>1){print $0}}END{}' | grep "" -m50
# awk '{if($6>1){print $0}}END{}' $6 为按照空格分隔的第六个字段，即响应时间
# grep "" -m50  展示前50行


```


### 取消wget的代理
使用root账户登录修改/etc/wgetrc文件，修改https_proxy=xxxx
```
vim /etc/wgetrc

```


### 当前日期的前两天

```
date -- date'2 day ago' +%Y%m%d

```


### 网络抓包
```
# 指定来源  xxx.xxx.xxxx.xxx  保存到/tmp/xxx.cap中
tcpdump -i eth0 src host  xxx.xxx.xxxx.xxx /tmp/xxx.cap

# 指定目标  xxx.xxx.xxxx.xxx  保存到/tmp/xxx.cap中
tcpdump -i eth0 dst host  xxx.xxx.xxxx.xxx /tmp/xxx.cap

```


### 批量新建文件夹
新建dir3,dir4,dir5...dir9的文件夹
```
mkdir /dir{3...9} 
chown user:user   /dir{3...9}
```


### 端口被占用
```
lsof -i | grep 8080
```

### curl
#### 

```
get请求
curl -XGET "www.baidu.com"


curl -XPOST "www.baidu.com" -d'
    {"name":"key","address":"value1"}
    '
```



### 磁盘被写满

查找服务器大文件，尤其是在有项目日志打印不规范导致空间被占满时找大文件使用

```
# 指定路径层数为1的所有文件和目录的大小，并从大到小排序，不过这种在没有目录或者文件权限时会报错
du -h --max-depth=1 /user  | sort -hr 

# 没有目录权限时过滤标准错误流信息 ,将标准错误流信息不打印出来
du -h --max-depth=1 /user 2>/dev/null
```



### 查找删除

/tmp文件夹下文件太多时，使用rm命令会报`list too long`的错误

```
find -name "*" | xargs -i rm {}
```





### vim

```
#向下翻
ctrl + f

#向上翻
ctrl + b
```

 



### 压缩和解压

```
压缩文件
tar -zcvf  压缩文件名.tar.gz  需要压缩的文件

解压文件
tar -zxvf  需要解压的文件名.tar.gz
```



## JAVA

查找cpu占用过高问题

```
top -H -p pid

printf '%x\n' pid

jstack pid |grep 'nid' -C5 –color

# 关注各种状态的线程的个数
cat jstack.log | grep "java.lang.Thread.State" | sort -nr | uniq -c

# 查看gc
jstat -gc pid 1000


jmap -dump:format=b,file=filename pid  
#  mat  工具来查看

```

