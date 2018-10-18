Git命令
分支操作
# 查看本地分支
git branch

# 查看远程分支
git branch -a

# 删除本地分支
git branch -D BRANCH_NAME
查看修改内容
git diff
应用场景：开发过程中，完成了一个功能，准备提交代码之前要在本地查看自己改动的文件，过滤一些因为误操作导致的文件变化

撤销操作
撤销操作

# 删除未提交的修改和新增的文件
git checkout . && git clean -xdf 

# 如果你有的修改已经加入暂存区的话,则改用此命令 
git reset —hard  && git clean -xdf
撤销add操作

# 撤销具体的文件,FILE表示具体的文件名
git rm —cached FILE

# 撤销所有文件
git rm -r —cached .
git remote用法
声明

ALIAS 即别名，默认有一个origin，新增仓库时，可以取一个其它别名
URL 即仓库的地址

给当前分支添加新的远程仓库

git remote add ALIAS URL
例如：

git remote add doc git@coding.codeages.net:FEZ/fez-doc.git
查看分支所指向的远程仓库

git remote -v
提交代码到远程仓库时

git push
默认是提交到origin 这个仓库，如果要提交到新建远程仓库，则：

git push ALIAS BRANCH
BRANCH指具体的分支

远程仓库地址变更

先删除再添加远程仓库
git remote rm ALIAS
git remote add ALIAS URL
直接修改配置文件
cd .git
vim config

# 之后修改 [remote ALIAS]下面的url即可
git stash 和 git stash pop
# 暂存改动的文件
git stash 

# 恢复改动的文件
git stash pop
应用场景：当你正在做一项复杂的工作时, 当前状态不想commit，此时其他项目发现了一个紧急的bug。 这时你想先切换到另外一个分支修复bug，那么就可以用 git stash 来保存当前的工作状态, 等你修复完bug后, 执行git stash pop操作就可以回到之前的工作状态。