#SVN冲突
***

###发生冲突原因
>工程师A修改了a.txt的第一行，提交了。
>
>工程师B也修改了a.txt的第一行，然后执行svn up，这时SVN提示了：（以下，你开始扮演工程师B的角色了）
>
	$ svn up
	在 “a.txt” 中发现冲突。
	选择: (p) 推迟，(df) 显示全部差异，(e) 编辑,
	(mc) 我的版本, (tc) 他人的版本,
	(s) 显示全部选项:

###解决冲突
>1.如果坚持使用自己的版本，输入mc即可。
>
>2.如果使用别人版本，输入tc即可。
>
>3.第三个方案是商量好，重新修改：
>
	○ 选择p（推迟），即引入冲突到本地，不过不会影响到SVN服务器端，可以放心。
	○ 这时，会生成几个文件：
	a.txt  a.txt.mine  a.txt.r6328  a.txt.r6336
	○ 其中a.txt中包含了工程师A、B的所有修改，以<<<<<<<、=======、>>>>>>>分隔。
		i. a.txt.mine是工程师B的修改，也就是未update前的a.txt。
		ii. a.txt.r6328 是工程师A提交前的版本，即未导致冲突的版本。
		iii.a.txt.r6336是工程师A提交后的版本，即导致冲突的版本。
>>修改好使用以下命令删除冲突文件和重新提交文件
>
	[root@ecloud weixin]# svn resolve --accept working Application/Home/Controller/WeiXinController.class.php
	svn ci -m "some confilct" Application/Home/Controller/WeiXinController.class.php
IMG