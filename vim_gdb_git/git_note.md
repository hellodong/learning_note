GIT起步
--------
git 有三种状态:已提交(committed),已修改(modified),已暂存(staged)<br>

#### git 配置
1)/etc/gitconfig 文件: 系统上每一个用户以及他们通用配置。使用时带有 -- system选项<br>
2) ~/.gitconfig 或 ~/.config/git/config 文件.只针对当前用户. 使用时带 --global 选项<br>
3) .git/config: 针对该仓库.<br>
 每一个级别会覆盖上一级别配置, .git/config 会覆盖 ~/.config/git/config。<br>
 

 #### 用户信息配置

 ``` json
 git config --global user.name "purefarmer"
 git config --global user.email purepurefarmer@gmail.com
 ```

 #### 设置文本编辑器

 ``` json
 git config --global core.editor vim
 ```

 #### 检查配置信息

 git config --list

 #### git remote prune origin
会与远程库进行一次同步，最终清理掉版本库中的dev分支，但�?地工作区�?的dev分支并不会删�?

#### git log --stat
查看所有提交�?�录的文件修�?

#### 修改remote url
git remote set-url origin (url)

### stash 使用
当前未提交的修改先存储起来，工作区干净以后可以切换到其他分支修改bug。完成线上bug修改后再回到dev分支下通过**git stash pop**就可以返回之前修改
- *git stash*, 将当前分支的修改存储起来
- *git stash pop*, 将存储起来的修改取出来
- *git stash list*, 查看一共有多少存储起来的修改
- *git stash save [stashMsg]*, 功能与*git stash*一样，附带存储 信息
- *git stash apply stash@{index}*, 将存储的
- *git stash drop stash@{index}*

#### 打补丁
git diff "commit or branch" patch, 生成一个标准的patch

git apply patch, 将patch 运用到当前分支

git format-patch -M <commit or branch>, 生成的patch文件不仅有diff内容，还有提交者和时间。需要使用git am 来应用

git am "patch name"

#### git clone 拉取指定分支
git clone -b <branch> <url>, 初次拉代码时，拉取指定分支到本地

#### 删除远程分支
git push origin --delete "remote_branch", 删除远程分支

#### git config --global credential.helper store
https 免密码下拉代码，在本地存储git仓库的用户合密码

#### SSL certificate problem: unable to get local issuer certificate
git 无法获取本地CA公钥:
```shell
fatal: unable to access 'https://cnhzlpvbktmirror01.ecitele.com:8443/scm/npti/npti.src.git/': SSL certificate problem: unable to get local issuer certificate
```
最优解决方案是添加服务器公钥:
- 从域名那拿公钥: openssl s_client -connect cnhzlpvbktmirror01.ecitele.com:8443 -showcerts < /dev/null | openssl x509 -outform PEM > /tmp/server.crt
- 将拿到的公钥添加到<git>/mingw64/ssl/certs/ca-bundle.crt 文件末尾

