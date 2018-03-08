### 本地分支操作
1.签出本地分支
```
git checkout -b mydevelop develop
```
2.本地分支需要注意
    1.提交过的切换分支的时候
    2.未提交的切换分支的时候
3.合并本地分支到develop
```
git checkout develop
git merge mydevelop
#或者
git rebase mydevelop 
```