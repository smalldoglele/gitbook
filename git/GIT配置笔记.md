1. 所需软件

   * Git Bash [官方下载]
   * p4merge 免费好用的文件合并工具
    > p4merge 是另外一个商用的版本管理工具perforce的文件对比和合并工具；
    > p4merge 是免费的，但是也是包含在p4工具集合里面的，所以下载官方文件的安装包名称为p4vinst64.exe
    > 安装的时候,第二步骤是选择安装软件的界面，只需要选择p4merge这个软件即可，其他的都不需要选
2. 下载完成后将p4merge的目录加入到path中
　　
    > 主要是为了可以在命令行直接使用p4merge启动软件，方便下面的git config  配置合并工具

3. 生成ssh秘钥 ssh-keygen -t rsa
    > 生成的公钥和私钥对，可以在当前用户的`.ssh/` 下找到，以pub结尾的是公钥
4. 将公钥放到服务器上去
    > 讲公钥中的文字复制到服务器，如`gitlab`　账户>ssh keys的配置中去
5. 配置git bash ls时候文件夹/文件名称中文乱码调整

```
alias ls='ls --show-control-chars --color=auto'
```

1. 快速配置

```
###配置用户名和邮箱
git config --global user.name "walden"
git config --global user.email "smalldoglele@126.com"
####配置命令别名
git config --global alias.st status
git config --global alias.ci commit
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.dt difftool
git config --global alias.mt mergetool
####开启颜色显示
git config --global color.ui true
####　gitk显示不乱码
git config --global gui.encoding utf-8
#####注释编码设置成utf8 
git config --global i18n.commitencoding  utf-8
###在winow上使用gbk显示注释
git config --global i18n.logoutputencoding gbk
#### 解决git status中文文件名乱码
git config --global core.quotepath false
#####设置默认推送的
git branch --set-upstream-to=origin/master
####配置对比工具
git config --global diff.tool p4merge
git config --global difftool.p4merge.cmd 'p4merge $LOCAL $REMOTE'
####配置合并工具
git config --global merge.tool p4merge
git config --global mergetool.p4merge.cmd 'p4merge $BASE $LOCAL $REMOTE $MERGED'
####git 不在生成*.orig
git config --global mergetool.keepBackup false
####打开difftool的时候问是否打开对比工具
git config --global difftool.prompt false
####打开mergetool的时候 不在询问是否打开
git config --global mergetool.prompt false
####设置文件默认推送的分支
git config --global push.default matching
####给每个分支设置变基 git config branch.<branchName>.rebase true
## 如主分支设置变基
git config branch.master.rebase true
####设置每个分支新建的时候使用变基
#git config --global branch.autosetuprebase always
```



