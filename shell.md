## 记录用到的shell命令



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

### 查看nginx日志中访问时间超过n秒的记录

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


### 查看8080端口被什么应用占用
```
lsof -i | grep 8080
```

### curl
get请求
```
    curl -XGET "www.baidu.com"

```

post请求
```
    curl -XPOST "www.baidu.com" -d'
    {"name":"key","address":"value1"}
    
    '

```


