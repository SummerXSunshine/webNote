# GIT



#### 一次正常的git流程

```
// 切换分支到master
git checkout master/main

// 更新master分支到远程仓库最新的版本
git pull

// git log查看日志中的commit版本号是否和最新的版本号一致
git log

// 从master分支创建一个新的开发分支
git checkout -b <本地分支名>

....进行你的代码开发...

// 查看修改的文件
git status

// 添加你要提交的文件
git add <文件路径>

// 再次确认你要添加的文件
git status

// 提交你的修改，这时候会进入vim命令行模式i进行插入操作，：wq保存并退出
git commit

// 把你的分支推到远程仓库
git push origin <本地分支>:<远程分支>
```



git clone -b <仓库的分支/master> <远程仓库地址>

git commit --amend

git reset <> --soft

git reset <> --hard

git rebase HEAD ~i

#### 代码误删怎么恢复？

```nginx
git reflog

git reset HEAD
```







