#Git常用命令
+ ###获取 Git 仓库

```
#在现有目录中初始化仓库
git init
#克隆现有的仓库
git clone git@github.com:iunionx/devdoc.git devdoc
```
+ 记录每次更新到仓库

```
#检查当前文件状态
git status
#跟踪新文件/暂存已修改文件
git add * . [文件名]
#状态简览 short
git status -s
#忽略文件
cat .gitignore
#查看已暂存和未暂存的修改 --staged 和 --cached 是同义词
git diff/difftool [--staged]
#提交更新
git commit 
git commit -m '注释'
#跳过使用暂存区域
git commit -a -m 'added new benchmarks'
##移除文件 从暂存区（和工作区）都删除
#暂存区
git rm --cached [文件名]
#从暂存区和工作区
git rm -f [文件名]
# 支持glob模式
git rm log/\*.log
#移动文件
git mv file_from file_to
```
> **glob 模式是指shell所使用的简化了的正则表达式**
+ 星号（*）匹配零个或多个任意字符；
+ [abc]匹配任何一个列在方括号中的字符（匹配其中一个字符）；
+ 问号（?）只匹配一个任意字符；
+ 字符范围,比如:[0-9],[a-z],[A-Z]

+ ###查看提交历史

```
#查看提交历史
git log
#显示内容差异的最近两次提交
git log -p -2
#简略的统计信息 新增/修改文件的个数
git log --stat
#定义日志格式
git log --pretty=oneline
git log --pretty=format:"%h - %an, %ar : %s"
#日期定义格式
git log --pretty=format:"%h - %an, %ad : %s" --date=iso
#字符图案分支
git log --pretty=format:"%h %s" --graph
#限制输出长度 最近两周内的提交
git log --since=2.weeks
# 默认日志条件是or 使用--all-match成为and
# 找出添加或移除了某一个特定函数的引用的提交
git log -Sfunction_name
#2008 年 10 月期间，Junio Hamano 提交的但未合并的测试文件
git log --pretty="%h - %s" --author=gitster --since="2008-10-01" \
   --before="2008-11-01" --no-merges -- t/
```
+ ###撤消操作

```
# 漏掉了几个文件没有提交[修补提交]
git commit --amend
#取消暂存的文件 [撤销暂存区文件]
git reset HEAD [文件名]
#撤消对文件的修改 [撤销工作区]
git checkout -- [文件名]
####撤销已经提交的文件
#将git仓库重置会上次提交点
git reset --hard HEAD^ 
git reset --soft HEAD^ 
###这里应该看注意

#提交的东西丢失了 怎么找回
git reflog --oneline 
git checkout {xxxx}
```
+ 虽然在调用时加上 --hard 选项可以令 git reset 成为一个危险的命令（译注：可能导致**工作目录中所有当前进度丢失**），但本例中工作目录内的文件并不会被修改。 
不加选项地调用 git reset 并不危险 — 它只会修改暂存区域。
+ 你需要知道 git checkout -- [file] 是一个**危险的命令**，这很重要。 你对那个文件做的任何修改都会消失 - 你只是拷贝了另一个文件来覆盖它。 除非你确实清楚不想要那个文件了，否则不要使用这个命令。
+ 记住，在 Git 中任何 **已提交的东西几乎总是可以恢复的**。 甚至那些被删除的分支中的提交或使用 --amend 选项覆盖的提交也可以恢复（阅读 数据恢复 了解数据恢复）。 然而，任何你未提交的东西丢失后很可能再也找不到了。
+ ### 远程仓库
```
#复制远程库
git clone git@github.com:iunionx/devdoc.git devdoc
#查看分支情况
git remote
#读写远程仓库使用的 Git 保存的简写与其对应的 URL
git remote -v
#添加远程仓库
#git remote add <shortname> <url> 
git remote add pb https://github.com/paulboone/ticgit
#拉取 Paul 的仓库中有但你没有的信息 pb是paul仓库的别名
#git fetch [remote-name]不合并
git fetch pb
#推送到远程仓库
#git push [remote-name] [branch-name]
git push origin master
#查看远程仓库分支具体情况
#git remote show [remote-name]
git remote show origin
####
# 远程仓库的移除与重命名
git remote rename [old_name] [new_name]
#
git remote rm paul
```
> 运行 git pull 通常会从最初克隆的服务器上抓取数据并自动尝试合并到当前所在的分支。

+ ### 打标签

> Git 使用两种主要类型的标签：轻量标签（lightweight）与附注标签（annotated）。

> 一个轻量标签很像一个不会改变的分支 - 它只是一个特定提交的引用。

> 然而，附注标签是存储在 Git 数据库中的一个完整对象。 它们是可以被校验的；其中包含打标签者的> 名字、电子邮件地址、日期时间；还有一个标签信息；并且可以使用 GNU Privacy Guard （GPG）签 > 名与验证。 通常建议创建附注标签，这样你可以拥有以上所有信息；但是如果你只是想用一个临时的标> 签，或者因为某些原因不想要保存那些信息，轻量标签也是可用的。

```
# 列出标签
git tag
git tag -l 'v1.8.5*'
```
