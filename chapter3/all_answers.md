#Chapter 3
##3.1.1
###例题1
1. cd /dev/shm
2. mkdir class3
3. ls -a 可显示所有文件，包括隐藏文件
4. 略
5. 不能直接删除
	直接删除显示：
	
	> rmdir: failed to remove ‘class3/’: Directory not empty
	
	需要使用rm -r /dev/shm/class3，如果不需要任何提示则用：rm -rf /dev/shm/class3

###例题2
1. 略
2. 可以，因为此时class3下面没有文件，是个空文件夹，所以可以使用rmdir命令删除
	
##3.1.2
1. ll /etc/?????
2. ll /etc/\*[0-9]*

##3.1.3