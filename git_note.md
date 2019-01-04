## GIT起步
git 有三种状态:已提交(committed),已修改(modified),已暂存(staged)<br>

#### git 配置
1)/etc/gitconfig 文件: 系统上每一个用户以及他们通用配置。使用时带有 -- system选项<br>
2) ~/.gitconfig 或 ~/.config/git/config 文件.只针对当前用户. 使用时带 --global 选项<br>
3) .git/config: 针对该仓库.<br>
 每一个级别会覆盖上一级别配置, .git/config 会覆盖 ~/.config/git/config。<br>

 ##### 用户信息
 ``` json
 git config --global user.name "purefarmer"
 git config --global user.email purepurefarmer@gmail.com
 ```
 ##### 文本编辑器
 ``` json
 git config --global core.editor vim
 ```
 ##### 检查配置信息

 git config --list
