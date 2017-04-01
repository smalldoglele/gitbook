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
# glob模式
```
>glob模式:
>
>
+ 撤销操作