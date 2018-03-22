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
3.设置分支跟踪
 > 第2步推送成功后，再次推送git命令提示
```
$ git push
fatal: The current branch my-remote-br has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin my-remote-br

```
执行命令

```
   git push --set-upstream origin my-remote-br
```

















