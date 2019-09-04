---
title: Git必知必会
tags: Git
description: Git必知必会
---
《Git Pro》真是一本好书，回老家的来回车程阅读了一番，厘清了很多之前模糊不清的概念。
## Git 的基础
git使用命令行可以使用其所有的功能，gui工具一般都是利用了某一些功能来实现某一种工作流的方式，gui工具会把几个命令组合起来完成某一项功能，对我们深入了解Git的实现流程是不利的，建议从命令行入手理解Git这个*文件系统/数据库系统？*
在Mac系统上安装Xcode后会自动安装git。
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
  git config --global alias.last "log -1 HEAD"
```

`git init`: 创建一个空的git目录
`git clone URL `: 将远程仓库所有的东西都克隆一份到目录下的.git目录下,并将当前HEAD指向的快照展示出来,可以直接用于开发.  
`git add`: 将未跟踪的文件加入暂存区 将解决冲突后的文件加入暂存区以便提交.注意`git add . ` 与 `git add *`的区别,`add .`将除了.gitignore指定的文件外所有的未跟踪和修改的放进暂存区，`add * -f` 则会忽略.gitignore的作用.
`git ci -m `: 提交文件到本地仓库
`git st`: 查看当前三个区域的状态.(工作区,缓存区,仓库)
`git diff`:查看工作区与暂存区的变化.加入 `--staged(--cached)` 参数,就是查看暂存区与仓库的变化.
`git log`:查看提交历史,可以`-p,--preety=oneline,-1，--graph`等优化输出
`git co`检出dev分支`git co dev`,`git co -- a`丢弃a文件的修改:**这是个危险的命令,不要随便使用，如果误用了只能依靠编辑器找回修改**.用`git co -b test`快速创建一个test分支并切过去
`git br`: 查看当前分支, `git br test`创建一个新分支,`git br -a `查看所有本地和远程的分支,`git br --merge`查看已经合并的分支，`git br --no-merge`查看未合并 的分支,`git br -f br_name some-sha1`强制修改当前br_name指向的节点
`git reset HEAD`: `git reset HEAD -- file`回退暂存区的文件修改 , 回退本地历史,可以使用HEAD^或HEAD~1等操作回退指定次数,
`git revert`: 回退到上一次的修改，产生一个新的节点，与上上个节点的内容一致。之后可push到远端同步回退。与reset的区别在于reset用于local的回退，而revert用于远端的回退。
`git push`的标准语法是：`git push <origin> <place>`，例如`git push origin master`的意思是**切到本地仓库中的“master”分支，获取所有的提交，再到远程仓库“origin”中找到“master”分支，将远程仓库中没有的提交记录都添加上去**
`git fetch`: 把远端仓库有,而本地仓库没有的内容拉下来,更新本地仓库的远程指针（如origin/master）但是不做合并
`git pull`: 把远端仓库有,而本地仓库没有的内容拉下来,并尝试做一次三方合并，相当于先`git fetch`后再做一次`git merge origin/master`，`git pull --rebase`拉下远端仓库内容后做一次变基合并
`git rm [FILE]`: 不再跟踪某个文件并从当前目录完全删除. 如果只是想不跟踪,继续存留在目录里,可以使用`git rm --cached [FILE]`
`git mv [FILE] [FILE_NEW]`: git mv 是一个命令的组合,等价于以下操作:

```
mv [FILE] [FILE_NEW]
git rm [FILE]
git add [FILE_NEW]
```


`git merge`: 如果没有冲突,那么就是将当前的HEAD和分支快速前进(fast-forward) 到 被合并分支的最新位置.如果有冲突,会做一个三方合并,然后生成一个节点.这个合并后的节点将会有两个父节点。
`git cherry-pick`: 将一些提交复制到当前所在的位置（HEAD）下面。
`git rebase`: `git rebase master test`等价于
```
git checkout test
git rebase master
```
`HEAD`:`^`和`~`移动指针操作符， `HEAD^` 当前指针的上一个位置,`HEAD^^`是上两个位置.可以使用~来简化,HEAD~2.`HEAD^2`对于合并后有多个父节点，这个表示第二个父节点，即不在同一条线上的父节点。

