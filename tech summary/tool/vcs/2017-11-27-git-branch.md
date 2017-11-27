# git branch使用技巧

1. 获取远程所有分支： **git pull --all**，执行成功后获取所有的远程分支，但没有在本地创建与远程分支一样的分支。效果如下

    [获取所有的分支信息](../../images/vcs/git/git pull all.png)

2. 新建本地仓库分支： **git branch branchname** 
3. 切换本地分支： **git checkout branchname**
4. 更新合并远程分支
	* 获取远程所有分支： **git pull -all**
	* 创建本地分支： **git branch branchname**
	* 更新远程分支到本地： **git pull origin originbranch**
	* 切换到本地开发的分支： **git checkout branchname**
	* 合并目标分支到本地分支： **git merge sourcebranch**