### 本地分支操作
1.签出本地分支
```
git checkout -b mydevelop develop
```
2.本地分支需要注意
    - 提交过的切换分支的时候,工作区间不会带过来
    - 未提交的切换分支的时候,未提交的会带过来
    
3.合并本地分支到develop
```
git checkout develop
git merge mydevelop
#或者 远程分支不要rebase
git rebase mydevelop 
```
> merge和rebase的区别 
> 快推和非快推的区别

4.删除本地分支
```
#安全 如果这份分支没有合并到其他分支上 不能删除
git branch -d mydevelop 
#强制 确认这个分支不合并到其他分支上要丢弃
git branch -D mydevelop
```
### 远程分支操作

1.创建从master分支签出本地分支my-remote-br
```
git co -b my-remote-br master
```
2.将本地分支my-remote-br推送到远程服务器的my-remote-br
```
git push origin my-remote-br

```
3.设置本地分支跟踪远程分支，
 > **该操作的目的是为了使用pull/push的时候，不使用额外的参数，就可以将
 > 本地推送到远程同名分支上**
 > 第2步推送成功后，再次推送,git会有如下提示
 > $ git push
 > fatal: The current branch my-remote-br has no upstream branch.
 > To push the current branch and set the remote as upstream, use

```
    git push --set-upstream origin my-remote-br
```
**执行命令上面的命令，将推送分支跟踪到远程分支**

4.验证跟踪是否成功,如下命令表示设置成功
```
$ git push
Everything up-to-date
$ git pull
Already up to date.
```
### 常见问题与解决方法
1.git br -r 看不到别人新建的远程分支

解决方案：使用git fetch命令同步远程仓库header到本地仓库后，可以看到远程分支；tab键自动提示也可是使用了
2.git 版本回退信息
解决方案:
```
#回退到上一个版本
git reset --hard HEAD^
#回退到某个版本
git rest --hard id
```
















