#搭建SVN服务器
***

###安装依赖包
>apr、apr-util、apr-iconv

###检查是否安装旧版本svn以及卸载旧版svn
>检查是否安装了低版本的SVN
>
	rpm -qa subversion
>卸载/删除原有安装
>
	yum remove subversion
	rm -rf /usr/local/svn

###安装svn
>1.yum安装：`yum -y install subversion`
>
>2.源码安装
>			
	i. #进入安装目录
	cd /usr/local
	ii. #解压压缩包
	tar -zxv -f subversion-1.8.4.tar.gz
	iii. #修改用户权限
	chown -R root:root /usr/local/subversion-1.8.4
	iv. #进入安装目录
	cd subversion-1.8.4
	v. #将sqlite-amalgamation-201311181848.zip上传到/usr/local/subversion-1.8.4中，然后解压安装sqlite支持
	mkdir -p sqlite-amalgamation
	unzip -o -d sqlite-amalgamation sqlite-amalgamation-201311181848.zip
	vi. #配置
	./configure \
	--prefix=/usr/local/svn \
	--with-apr=/usr/local/apr \
	--with-apr-util=/usr/local/apr-util \
	--with-zlib=/usr/local/zlib
	vii. #编译安装
	make && make install

###验证svn是否安装成功
>
	/usr/local/svn/bin/svnserve --version

###删除安装源文件
>
	cd /usr/local
	rm -rf subversion-1.8.4

###配置环境变量
>
	export SVN_HOME=/usr/local/svn
	export PATH=SVN_HOME/bin:PATH
	source /etc/profile
	svnserve --version

###单个仓库配置
>建立版本库(可建立多个，新建库后以下各项都需重新配置。注意区别安装目录与版本库目录,以下讲的都是版本库目录)
>
	mkdir -p /var/www/html/test
	chmod -R 775 /var/www/html/test

>建立svn版本库(与上面目录对应),执行命令后自动生成配置文件,文件夹发现包含了conf, db,format,hooks, locks, README.txt等文件，说明一个SVN库已经建立
>
	svnadmin create /var/www/html/test/svn

###生成账户密码
> 生成密码文件，配置用户信息(可以添加多个，用户名密码对的方式)
>
>【注意】：配置文件的行前的#和空格都要去掉，必须去掉
img

###配置authz
>对/var/www/html/test下所有文件具有可读可写权限，test只有只读权限，除此之外，其它用户均无任何权限，最后一行*=很重要不能少。
>
img

###配置svnserve.conf
>打开下面的5个配置注释
>
	anon-access = read #匿名用户可读
	auth-access = write #授权用户可写
	password-db = passwd #使用哪个文件作为账号文件
	authz-db = authz #使用哪个文件作为权限文件
	realm = /home/svn # 认证空间名，版本库所在目录
>
	【注意】：
	i. 最后一行的realm记得改成你的svn目录
	ii. 打开注释时切记前面不要留有空格，否则可能有问

IMG

###启动与停止SVN
>
	[root@localhost conf]# svnserve -d -r /var/www/html/test/svn（启动）
	[root@localhost conf]#  killall svnserve（停止）
	上述启动命令中，-d表示守护进程， -r 表示在后台执行。停止还可以采用杀死进程的方式：
>
	[root@localhost conf]# ps -ef|grep svnserve
	root      4908     1  0 21:32 ?        00:00:00 svnserve -d -r /home/svn
	root      4949  4822  0 22:05 pts/0    00:00:00 grep svnserve

###客户端连接
>这里使用TortoiseSVN，输入地址svn://你的IP 即可，不出意外输入用户名和密码就能连接成功了。
>
>默认端口3690，如果你修改了端口，那么要记得加上端口号。
IMG

###客户端初次上传代码到服务器
>现在客户端commit相关文件。
>
>服务器端使用svn up，不要带*号！

###SVN服务器更新代码
>【svn checkout】：svn服务器不是ftp服务器，通常你提交到服务器上的svn仓库中，会按照svn它内部的方式／格式来存储（包括代码、图片、文档等任何你提交的），以及相应的日志。需要在svn服务器上使用文件的话同样也像客户端一样用svn checkout检出来。
>
IMG

>如果需要自动更新服务器代码可以看下面两个链接：
>		
	http://mengkang.net/193.html
	http://mengkang.net/67.html

>客户端再次更新文件，使用svn up *进行文件的更新
>
img