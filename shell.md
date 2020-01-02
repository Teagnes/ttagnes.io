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
# 



```



```
# 简化版
pgrep xxx  | xargs kill -s 9

```

### 查看nginx日志中访问时间超过n秒的记录

```


```








```


```
