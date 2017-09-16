#Git关联远程仓库
***

###本地代码上传到远程仓库
>生成ssh密钥：因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的。  
>img  
>img  
>
>将github_rsa.pub的密码复制到github中，配置ssh key的时候勾选下面的Allow write access就可以了，否则没有读写权限。  
>img

###关联远程仓库
>关联远程仓库  
>img  
>img  

>第一次使用加上了-u参数，是推送内容并关联分支。  
>推送成功后就可以看到远程和本地的内容一模一样，下次只要本地作了提交，就可以通过命令：`$ git push origin master`，如果是其他分支比如dev，就用`git push origin dev`    
>img  
>img  

###小结
>1.要关联一个远程库，使用命令git remote add origin git@server-name:path/repo-name.git；   
>
>2.关联后，使用命令git push -u origin master第一次推送master分支的所有内容；  
>
>3.此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；  