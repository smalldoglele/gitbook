### 本地分支操作
1.签出本地分支
```
git checkout -b mydevelop develop
```
2.本地分支需要注意
    - 提交过的切换分支的时候
    - 未提交的切换分支的时候
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