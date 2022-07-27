> 初始化git

git init

> 拉默认分支的代码（克隆）

git clone

> 拉指定分支的代码

git clone -b 分支 

> git 添加文件到暂存区

git add .

> git提交暂存区到本地仓库。

git commit -m ''

> git 下载远程代码并合并

git pull

> git 上传远程代码并合并

git push

> git 查看历史提交记录

git log

> git 隐藏当前的工作现场。在开发过程中，在一个分支开发新的功能，还没开发完毕，做到一半时有反馈需要处理紧急bug，但是新功能开发了一半又不想提交。

git stash  

> git 恢复最新的进度到工作区

git stash pop

> git 切换分支

git checkout 分支

> git 切换并创建分支

git checkout -b 分支

> git 查看分支

git branch

git config --global user.name 'name'

git config --global user.email '邮箱'