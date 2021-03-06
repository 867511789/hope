# linux常用命令

一、目录切换命令

	cd usr 切换到usr目录下
	
	cd ../ 切换到上一层目录
	
	cd /   切换到系统根目录
	
	cd ~   切换到root目录(用户主目录)
	
	cd -   切换到上一个所在的目录
	
二、目录操作命令

	1.添加目录操作
	
		命令：mkdir 目录名称
		
	2.查看目录
	
		命令： 
		ls 	普通查看，当前目录下的所有文件和目录
		
		ls -a 高级查看，当前目录下的所有文件和目录（包括隐藏的）
		
		ls -l 详细查看，当前目录下的所有文件和目录的详细信息
		
		注意：ls -l 可以缩写成 ll
		
	3.寻找目录
	
		命令：  
		find 目录 参数 如：find / -name '*test*' 

	4.修改目录的名称
	
		命令：  mv 旧目录名称 新目录名称 

	5.移动目录的位置

		命令：  mv 目录名称 目录的新位置

	6.拷贝目录

		命令：  
		cp 目录名称 目录拷贝的目标位置(会提示不能直接拷贝目录，这种形式一般用于拷贝文件)

		cp -r 目录名称 目录拷贝的目标位置(-r代表递归)

	7.删除目录

		命令：  
		rm 目录(会提示不能直接删除目录，这种形式一般用于删除文件)

		rm -r 目录(会一步一步提示进行删除，如果目录中包含很多层目录一般不推荐使用)

		rm -rf 目录(强制直接删除，不提示)
		
三、文件的操作命令

	1.文件的创建
	
	    命令：  touch 文件名称（空文件） 

	2.文件的查看

		命令：	
		cat 文件名称(只会显示文件在屏幕显示的最后一屏内容，一般只用于小文件的查看)

		more 文件名称(可以显示百分比，回车可以向下一行，空格可以向下一页，q可以退出查看)

		less 文件名称(可以喝more有相同操作，但是可以使用键盘上的PageUp和PageDown向上和向下翻页，q可以退出查看)

		tail 参数 文件名称（查看参数值的文件的最后行数的内容，如果参数值的行数大于屏幕显示的最大行数，那么只会显示最后一屏的内容）

			如：tail -10 sudo.conf

				tail -f sudo.conf（动态监控，比如tomcat的监控，按Ctrl+C退出）

		注意：在linux系统中Ctrl+C代表强制退出，不建议经常使用

	3.修改文件的内容（重点）

		命令：	
		vim 文件

			命令模式（该文件现目前只处于打开状态，不能编辑，如果要进行编辑，输入i/a/o）

			编辑模式（该文件现目前只能进行编辑操作，如果是按下esc进入命令模式，重新进入编辑模式后以前的内容清空，重新编辑）

			底行模式（按下:进入底行模式，如果需要保存再退出输入wq，如果想直接不保存强制退出输入q!）

		关于vim的使用过程：

			在实际开发中，使用vim编辑器主要作用就是修改配置文件

			vim 文件---->进入文件---->命令模式---->按i进入编辑模式---->编辑文件---->按esc进入命令模式---->输入:进入底行模式---->输入wq/q!退出

	4.删除文件
	    命令：
        rm [-rf] 文件名
	
四、压缩文件的操作命令

	1.打包并压缩文件

		命令：	
		tar -zcvf 打包压缩后的文件名 要打包压缩的文件	

			如：tar -zcvf xxx.tar.gz a.txt b.txt

			    tar -zcvf xxx.tar.gz /test/*
			    
	2.解压压缩包(重点)

		命令：	
		tar -xvf 压缩文件	

			如：tar -xvf xxx.tar.gz（解压到当前目录）

			    tar -xvf xxx.tar.gz -C 目录(解压到指定目录)

五、其他命令


	1.显示当前所在位置

		命令：	
		pwd

	2.搜索命令

		命令：	
		grep 要搜索的字符串 要搜索的文件（从文件中查找字符串）

		grep 要搜索的字符串 要搜索的文件 --color(从文件中查找字符串并标记字符串的颜色为红色)

	3.管道命令

		命令：	|

	4.查看进程

		命令：	ps -ef（查看当前系统中运行的进程）

	5.杀死进程

		命令：	kill -9 进程的pid

	6.网络通信命令

		命令：	
		ifconfig	查看通信信息

		ping		查看连接状态

		netstat -an	查看当前系统的端口使用情况

六、linux的权限命令

	通过ll命令查看文件的详细信息

		第一个字符显示"-"代表是文件，显示"d"代表是目录，显示"l"代表是快捷方式

		后面的9个字符划分为三段（每三个字符为一段）

			第一段代表：属主权限

			第二段代表：属组权限

			第三段代表：其他用户权限

			四种字符：

				-	代表没权限		数字代表是0

				r	代表读的权限		数字代表是4

				w	代表写的权限		数字代表是2

				x	代表可执行的权限	数字代表是1

	修改权限的命令：chmod u=rwx,g=rwx,o=rwx 文件 

		需求：针对yp.conf文件修改权限：u=rwx,g=rw,o=r    764