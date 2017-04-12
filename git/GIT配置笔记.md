1. 所需软件

   * Git [官方下载]()
   * notepad2\_4.2.25\_x64.zip   nodepad2 官方下载
   * p4merge 官方下载 p4vinst64.exe p4merge

     > 对比过kdiff3和diffMerge都没有p4merge使用效果好  
     > notepad2是用来写注释的时候，可以使用utf8  
     > p4merge包含在p4vinst64中，仅仅选择p4merge即可  
     > nodepad2,p4merge要加入到环境变量中
     > **nodepad2,p4merge设置默认使用utf8编码**

2. 下载完成后将，nodepad2,p4merge的目录加入到path中
3. 生成ssh秘钥 ssh-keygen -t rsa 
4. 将公钥放到服务器上去
5. 配置git bash 下文件夹/文件名称中文乱码调整

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
####gitk显示不乱码
git config --global gui.encoding utf-8
#####注释编码设置成utf8 
git config --global i18n.commitencoding  utf-8
###在winow上使用gbk显示注释
git config --global i18n.logoutputencoding gbk
#### 解决git status中文文件名乱码
git config --global core.quotepath false
#### 提交时候使用的编辑器默认使用UTF8可以避免乱码
git config --global core.editor notepad2
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
git config --global branch.autosetuprebase always
```



