#Git常用命令
+ 仓库操作

```
#在现有目录中初始化仓库
git init
#克隆现有的仓库
git clone git@github.com:iunionx/devdoc.git devdoc
```
+ 提交操作

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

+ 日志

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
```
+ 撤销操作