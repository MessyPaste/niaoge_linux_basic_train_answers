# Chapter7 bash的基本使用与系统救援
# p108-上
1. cat /etc/passwd |cut -d ":" -f 1,7
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/000E4F3D-A4C9-473A-ADC1-6EBE55835799.png)
首先cat /etc/passwd输出文件内的所有信息，然后后面一个竖线|代表一种管道，将前面的信息输出信息当成输入给后面一条命令处理，cut -d ":" -f 1,7 是核心命令，这里有两个重要的参数 -d （delimiter，分隔符）和 -f（fileld，字段），前者是设定分隔符，-d参数用于将字符串以冒号隔开，-f参数是选定需要哪个字段，可以理解成需要第几个字段。
2. Daemon是长时间运行的进程，通常在系统启动后就运行，在系统关闭时才结束。一般说Daemon程序在后台运行，是因为它没有控制终端，无法和前台的用户交互。Daemon程序一般都作为服务程序使用，等待客户端程序与它通信。我们也把运行的Daemon程序称作守护进程。
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/C61C47FF-7723-43E7-B3E4-30642B04C701.png)
参考：[linux 守护进程 daemon - Boblim - 博客园](https://www.cnblogs.com/fnlingnzb-learner/p/6485506.html)

# p108-下
1. 如下，输出了当前bash所在的位置
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/B19DF91F-7637-4164-8F21-C263FB61C70F.png)
2. 无内容
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/98BB5699-7058-4FC3-BE94-E5BFA0C9FAF3.png)
这里我对原书命令有疑问，应该是大写的shell，即SHELL，如下：
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/ADD84859-A9C2-4BA3-8952-0B4F9D56D91F.png)
也就是说当前系统的shell就是bash
3. 切换shell，一开始在官方镜像上切换，发现无法切换csh，我用chsh -l看了下
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/780618E9-97C2-4E29-A049-11BB7F5D668F.png)
然后我用腾讯云试了下，发现有csh
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/779308A7-8C9D-4620-AF76-9520AC4193D8.png)
下面使用腾讯云演示,这里使用chsh命令切换e
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/D6D6F784-E716-466E-94C9-5014F63D3DD4.png)
4. BASH无数据，SHELL已经改成csh
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/9F6ABB29-046F-4065-B161-887F62BBE169.png)
注意：这里更改完bash环境后要注销登录，不然无法查看到效果。
5. $0代表列出当前的执行文件
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/AB5FDF76-8ADB-4F7A-9375-B5E59A19E543.png)
6. 笔者是通过chsh命令更改的环境，输入exit后直接注销登录了，作者这里的意思应该是返回到原来的shell，所以返回到原来的shell可以通过chsh命令，输入/bin/bash即可回到默认bash
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/A9E7B6AE-7E3F-42EA-94D7-501267B887D1.png)
7. 会显示：无法登入（如下图），即：这个使用者无法使用 bash 或其他 shell 来登入系统进行交互。举例来说，各个系统账号，打印作业由 lp 这个账号在管理，WWW服务由apache这个账号在管理，他们都可以进行系统程序的工作，但是就是无法登入主机。（p109作者也对此进行了解释）
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/E4233F0E-8333-49E2-8EEF-3B921BA55CB2.png)
参考：[特殊的shell——/sbin/nologin - >>向着CTO前进>> - CSDN博客](https://blog.csdn.net/qhairen/article/details/45563433)

# p109-上
1. 命令为：usermod -s /usr/sbin/nologin student
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/75CCDE67-E683-4B2A-9FB5-714551CE7744.png)
2. 尝试使用shell登录student，无法登陆
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/994BB816-37F7-412A-8807-9A9D93BF3BF6.png)
3. 命令是：usermod -s /bin/bash student
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/F5538ED7-6C34-4AD0-97CB-C25D984A9EA8.png)

# p109-下
1. Linux id命令用于显示用户的ID，以及所属群组的ID。
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/FB90E14C-D96A-4940-BD7C-1490751AB8F8.png)
参考[Linux id命令 | 菜鸟教程](http://www.runoob.com/linux/linux-comm-id.html)
笔者在网上可以看到出现了bin这个用户，而在笔者安装的系统内，没有出现，如：
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/95863BD7-3787-446F-BC95-270FA17BC09E.png)
2. 可以，直接通过su - student 命令
3. 无法直接切换
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/79FAC423-FEAE-4947-9A09-0999B95303EC.png)
4. 创建过程如下：
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/B3486C52-87BE-4527-B50F-85C750CDEA3E.png)
5. 无法登陆，显示如下：
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/C1198B85-E367-4F81-AD2B-018C096E8629.png)

# p110
1. 作者书中空格符也要加转义（书中p110，黑色正方形第五点），而经过我实测，空格符是不需要的，如下所示：
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/BAD86A39-50AA-497E-97EE-886F2343AFA8.png)
2. 
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/C2D73161-A8EB-40A3-B5A6-5F8ED0C6A2AB.png)
3. 不能，因为变量不能以数字开头
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/229AD905-E614-4BD1-ABF0-30AF156EC0E1.png)
4. 注意$前面有转义字符
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/5BCC02E2-399D-47C0-9B0C-0E0A05AA47D7.png)
5. 注意$前面没有转义字符
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/CB56E50E-645F-42E9-B805-8BFF5CB690C8.png)
6. 
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/B6097791-CBA8-41B6-9580-143185834E3F.png)
7. 
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/F08B688A-2683-4CA6-BB05-8E69C74A1C6E.png)

# p111 -上
1. find -perm 是查找指定权限文件的命令
2. 特殊权限文件如下
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/33882976-FEE3-41AC-BB30-010586D8D32A.png)
3. 列出权限
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/E0C4948A-9A8D-4399-A542-6AB6F3A8B8A5.png)

# p111 -下
1. 先列出文件
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/4EE25C91-9DD9-46AC-B29D-1C56742BFACD.png)
可以列出详细列表
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/86B770ED-CE64-4506-A85A-31E54272682B.png)
2. 见3
3. 对比普通复制和连同权限复制
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/830AA64A-BB7B-4193-A5D7-57568E7274D8.png)

## p112
1. 分隔符是冒号
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/3B4D8051-08A9-4141-96FE-7D00235FF4E5.png)
2. oldpath=$PATH
3. PATH=$oldpath:/bin
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/3B15F149-E9EC-4556-AF63-DC90C2D68A7A.png)
4. 4-6略 笔者此处环境可能与书上不同，略

未完待续…