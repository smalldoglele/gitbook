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
git reset --hard id
```
### release 分支合并步骤和规范
1. 通知大家将本地release --(push)--> 远程release，本地develop --(push)--> 远程develop;本次需要发到测试的内容必须提交；其他内容自己酌情提交；
2. 远程release --(pull)--> 本地release，远程develop --(pull)-->本地develop;
3. **先**本地release --(merge)--本地develop;
4. **后**本地develop --(merge)--本地release;
5. 将本地release --(push)--> 远程release，本地develop --(push)--> 远程develop;

#### 拉取远程分支并创建本地分支
1.使用该方式会在本地新建分支x，并自动切换到该本地分支x。
采用此种方法建立的本地分支会和远程分支建立映射关系。
```
git checkout -b local_brname origin/remote_brname
```
2.用该方式会在本地新建分支x不会自动切换到该本地分支x，需要手动checkout。采用此种方法建立的本地分支不会和远程分支建立映射关系。
```
git fetch origin remote_brname:local_brname
```
#### git 基本提交流程
````
#查看文件状态
git st -s
# 1 修改过得文件添加到索引区
git add .
# 2 提交文件到版本库 需要写备注
git ci 
# 3 拉取远程仓库地址
git pull 
# 4 如果出现冲突 会显示 (xxx|MERGEING) 打到合并工具
git mt
# 5 合并完成 提交文件 使用默认备注
git ci 
# 6 如果合并文件有问题 终端当前提交 从3处开始继续
git merge --abort 
# 接5 推送本地仓库到远程
git push  
````















