1. 需要下载的文件,MsysGit nodepad2 TortoiseDiff
	Git-1.9.5-preview20141217.exe 官方下载
	notepad2_4.2.25_x64.zip   nodepad2 官方下载
	p4merge 官方下载 p4vinst64.exe  安装的时候只需要选择p4merge即可
	##对比过kdiff3和diffMerge都没有p3merge使用效果好
2. 下载完成后将，nodepad2,p4merge的目录加入到path中
3. 生成ssh秘钥 ssh-keygen -t rsa 
4. 将公钥放到服务器上去
5. 配置git bash 下文件夹/文件中文显示 alias ls='ls --show-control-chars --color=auto'
7. 快速配置

```
####配置用户名和邮箱
git config --global user.name "walden wang"
git config --global user.email "walden@goldpalm.com.cn"
####配置命令别名
git config --global alias.st status
git config --global alias.ci commit
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.dt difftool
git config --global alias.mt mergetool
####设置每个分支新建的时候使用变基
git config --global branch.autosetuprebase always
####设置文件默认推送的分支
git config --global push.default matching 

####开启颜色显示
git config --global color.ui true
####gitk显示不乱码
git config --global gui.encoding utf-8
#### 解决git status中文乱码 
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
####给每个分支设置变基 git config branch.<branchName>.rebase true
## 如主分支设置变基
git config branch.master.rebase true
```
