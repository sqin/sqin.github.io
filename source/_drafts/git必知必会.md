---
title: git必知必会
tags: git
description: git必知必会
---
《Git Pro》真是一本好书，回老家的来回车程阅读了一番，厘清了很多之前模糊不清的概念。
## Git 的基础
git使用命令行可以使用其所有的功能，gui工具一般都是利用了某一些功能来实现某一种工作流的方式，gui工具会把几个命令组合起来完成某一项功能，对我们深入了解Git的实现流程是不利的，建议从命令行入手理解Git这个*文件系统/数据库系统？*
在Mac系统上安卓xcode后会自动安装git软件。
我们第一步要做的是对git做一些全局配置(git的配置有三级，第一级是在/etc/.git,对应git
 config --system，第二级实在系统根目录下。。，对应git config --global，第三级在自己的工作区下面，后面的配置会覆盖前面的配置)
到~/.ssh目录下 ssh-keygen -t rsa -C "sqin.lin@foxmail.com" ,将公钥的内容复制到GitHub的配置里面去.


```
git config --global user.name "your_name"
git config --global user.email "your_email"
```

设置命令别名,加快键入速度

```
  git config --global alias.co checkout
  git config --global alias.st status
  git config --global alias.ci commit
  git config --global alias.br branch
```

`git init`: 创建一个空的git目录
`git add`: 将未跟踪的文件加入暂存区 将解决冲突后的文件加入暂存区以便提交.注意`git add . ` 与 `git add *`的区别.
`git ci -m `: 提交文件到本地仓库
`git st`: 查看当前三个区域的状态.(工作区,缓存区,仓库)
`git diff`:查看工作区与暂存区的变化.加入 `--staged(--cached)` 参数,就是查看暂存区与仓库的变化.
`git log`:查看提交历史,`p,preety`等优化输出
`git co`:  检出dev分支`git co dev `,丢弃a文件的修改:`git co -- a` **这是个危险的命令,不要随便使用**
`git br`: 查看当前分支, `git br test`:创建一个新分支
可以用`git co -b test`快速创建一个test分支并切过去



## Git 的分支管理
`merge`:
`cherry-pick`:
`rebase`: