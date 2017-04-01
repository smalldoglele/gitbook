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
#查看已暂存和未暂存的修改
git diff/difftool
```
+ 撤销操作