#GIT的基本使用
***

###配置用户信息
>因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址。  
img

###创建Git仓库
>可使用原有的仓库，进入该目录使用git init命令生成.git文件，表示初始化成功。  
img  
>使用git status查看当前状态：  
IMG

###提交文件到Git暂存区中
IMG 
>出现warnning是因为：windows中的换行符为 CRLF， 而在linux下的换行符为LF，所以在执行add . 时出现提示，可使用以下解决方法：
>
	rm -rf 	.git//删除git
	git config --glocal core.autocrlf false//禁用自动换行
>	
	重新初始化
	git init
	git add .


###删除Git暂存区文件
IMG

###提交Git暂存区文件
>为什么Git添加文件需要add，commit一共两步呢？
>>因为commit可以一次提交很多文件，所以你可以多次add不同的文件。可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。
>
>>1.第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；
>
>>2.第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。  
img

###目标文件修改并查看状态
>修改之后就提示你可以对该文件进行add和commit操作。  
img  
>对比历史信息  
img  

###查看Git的log
IMG

###回滚版本号
>通过git log查看[穿梭前]的版本号，以便确定要回退到哪个版本。
>
>通过git reset --hard 版本号来进行回滚  
img  
>通过git reflog查看[所有版本]日志，以便确定要回到未来的哪个版本  
IMG

###Git删除
>
	git rm test.txt
	git commit -m "remove test.txt"

###Git撤销修改
>
	a. 场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的[修改/删除]时，用命令git checkout -- file。
	b. 场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，
		第一步用命令git reset HEAD file，就回到了场景1
		第二步按场景1操作。
	c. 场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

###Git移动文件
	git mv 原路径 目标路径

###Git的拉取和旧版本比较
IMG  
IMG  

###可视化Git：
>使用`gitk`命令  
IMG