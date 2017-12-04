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

5. 合并可能冲突的分支
    例如需要将一个分支与另一个分支合并，并且两者之间可能存在冲突 
    - 将远程分支都更新到本地 
    
	```
		1. git branch --list
		2. git branch <本地分支> 
		3. git merge <远程分支>，产生冲突见下图
		4. 解决冲突
		5. 解决冲突可以通过VI也可以通过IDE，Eclipse下个人建议通过：选中文件->右键->team-merge tool，查看本地分支与远程分支的冲突点以及修改点，以免忽略远程修改的地方.
		6. 解决冲突后重新提交修改后的文档即可。如果命令行，需要重新add冲突文件，如果是IDE需要在git视图下，找到修改的文件，右键添加到index中
	```
	 [冲突界面](../../images/vcs/git/merge_conflict.png)
 