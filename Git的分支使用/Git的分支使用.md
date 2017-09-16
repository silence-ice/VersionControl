#Git的分支使用
***

###分支的操作
>创建Student分支：[主要修改Student]，下面两条命令相当于`git checkout -b StudentCon`    
img

>创建Member分支：[主要修改Member]  
img

>切换到Student分支，在Member修改的内容Student是看不到的！！  
img

>合并分支 
img

>【分支命令小结】：[Git鼓励大量使用分支]
>
	a. 查看分支：git branch
	b. 创建分支：git branch <name>
	c. 切换分支：git checkout <name>
	d. 创建+切换分支：git checkout -b <name>
	e. 合并某分支到当前分支：git merge <name>
	f. 删除分支：git branch -d <name>