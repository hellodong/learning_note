
1) git tag -d 标签                          删除<br>
2) git tag 标签                             创建标签<br>
3) git checkout -b branch origin/branch     拉取远程分支<br>
4) git push --tags                          将本地分支推送到服务器<br>

## 拉取远程分支
git checkout -b branch origin/branch

## 添加远程本地分支
git push origin <branchName>

## 删除远程分支
### git v1.7.0 之后
git push origin --delete <branchName>
### git v1.7.0 之前
删除远程分支（推送一个空分支到远程分支，其实相当于删除远程分支)  

## 删除远程tag
### git v1.7.0 之后
git push origin --delete tag <tagName>
### git v1.7.0 之前
git push origin :refs/tags/<tagname>

## 获取当前tag
git describe --long --dirty

## 取消git add
git add 后，有相关文件暂存unstage, git reset HEAD <file> 取消暂存

## 本地向服务器推送tag
git push --tags 或者 git push origin --tags  推送所有tags到服务器 <br>
git push origin <tagName>  推送某个分支到服务器<br>

## git项目转移
git remote remove origin  
git remote add origin [GIT URL]  
git remote -u origin master  
上述步骤如果再还原到之前git服务器可能会有问题，还没有尝试过。





