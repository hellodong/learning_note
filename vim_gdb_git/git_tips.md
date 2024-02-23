
1) git tag -d 标签                          删除<br>
2) git tag 标签                             创建标签<br>
3) git checkout -b branch origin/branch     拉取远程分支<br>
4) git push --tags                          将本地分支推送到服务器<br>

[toc]
#### 拉取远程分支
git checkout -b branch origin/branch

#### 拉取远程tag
git fetch -t  
git fetch --tag

#### 添加远程本地分支
git push origin <branchName>

####　拉取本地远程分支
git checkout --track origin/<branchname>
git checkout -b <local_branchname> origin/<branchname>

#### 删除远程分支
##### git v1.7.0 之后
git push origin --delete <branchName>
##### git v1.7.0 之前
删除远程分支（推送一个空分支到远程分支，其实相当于删除远程分支)  

#### 删除远程tag
**git v1.7.0 之后**

git push origin --delete tag <tagName>
**git v1.7.0 之前**

git push origin :refs/tags/<tagname>

#### 获取当前tag
git describe --long --dirty

#### 获取某个tag的注释
git tag -l '<tagname>' -n9999
#### 取消git add
git add 后，有相关文件暂存unstage, git reset HEAD <file> 取消暂存

#### 本地向服务器推送tag
1. git push --tags 或者 git push origin --tags  推送所有tags到服务器 <br>
2. git push origin <tagName>  推送某个分支到服务器<br>

#### git项目转移
git remote remove origin  
git remote add origin [GIT URL]  
git remote -u origin master  
上述步骤如果再还原到之前git服务器可能会有问题，还没有尝试过。

#### GIT patch
使用 git format-patch 生成专用.patch文件

- 某次提交之前的几次提交:
```git
git format-patch [commite sha1 id] -n
```
- 某个提交的patch:
```git
git format-patch [commite sha1 id] -1
```
- 某两次提交的之间的所有patch
```git
git format-patch [commite id]...[commite id]
```
##### 应用patch
- 检查是否能打入:
```git
git apply --check [xxx.patch]
```
- 打入patch:
```git
git apply [xxx.patch] or
git am [xxx.patch]
```
##### 冲突解决
1) 自动合入patch不冲突的代码改动，保留冲突部分:
```git
git apply --reject [xxx.patch]
```
2) 解决完冲突后删除后缀为.rej的文件，并执行git add 放到暂存区
3) 接着执行git am --continue

- 打入patch冲突是，可以执行git am --skip 忽略冲突，也可以git am --abort 回退打入的patch.





