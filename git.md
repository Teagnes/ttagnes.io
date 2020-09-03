# git 学习



### 分支

```
# 查看本地分支和远程分支的映射关系
git branch -vv

# 查看远程分支
git branch -r

# 拉取远程分支dev并新建本地分支dev (自动切换到dev上)
git fetch
git checkout -b dev origin/dev

或者
git branch --track origin/dev


$ git push <远程主机名> <本地分支名>:<远程分支名>
git push origin dev:dev
```





### 提交过程

- 各个阶段查看暂存区
- 当前哪些被修改
- 指定文件回退
- 指定文件被修改了哪些内容
- 指定文件和历史版本对比





### 一般开发流程

- 远程新建分支

  - 一般在github或者gitlab上直接新建即可

- 拉取分支到本地

  ```shell
  git branch --track origin/dev
  ```

  

- 开发功能并提交

- 多个功能rebase

- 合并到主干

- 删除开发分支







