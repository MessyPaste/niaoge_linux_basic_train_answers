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
3. 切换shell，一开始在官方镜像上切换，发现无法切换csh，我用chsh -l看了下(通过chsh -l可以查看当前系统已有的shell是哪些)，即没有显示csh这个shell
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/780618E9-97C2-4E29-A049-11BB7F5D668F.png)
然后我用腾讯云试了下，发现有csh
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/779308A7-8C9D-4620-AF76-9520AC4193D8.png)
下面使用腾讯云演示,这里使用chsh命令切换shell，输入chsh然后再次输入你要切换的shell所在的可执行程序就可以了
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
3. 命令是：usermod -s /bin/bash student，然后就可以继续登录了
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
1. 作者书中空格符也要加转义（即书中p110，黑色正方形第五点），而经过我实测，空格符是不需要的，如下所示：
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/BAD86A39-50AA-497E-97EE-886F2343AFA8.png)
2. 
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/C2D73161-A8EB-40A3-B5A6-5F8ED0C6A2AB.png)
3. 不能，因为变量不能以数字开头
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/229AD905-E614-4BD1-ABF0-30AF156EC0E1.png)
4. 注意$前面有转义字符
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/5BCC02E2-399D-47C0-9B0C-0E0A05AA47D7.png)
5. 注意$前面没有转义字符，$myname会被替换成myname指向的变量
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/CB56E50E-645F-42E9-B805-8BFF5CB690C8.png)
6. 这个命令用于显示操作系统的发行版号
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

## p113
1. PS1的内容为：[\u@\h \W]\$
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/BC9F9C29-9E80-4C05-9F6D-63D3002CBE33.png)
2. \W ：利用basename取得工作目录名称，只显示最后一个目录名
\$ ：提示字符，如果是root用户，提示符为 # ，普通用户则为 $
3. PS1="[\u@\h \# \W]\$"
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/9306C699-4114-4DD4-B2A7-717859032AEE.png)
[Linux系统下的终端命令提示符设置（PS1）_Linux教程_Linux公社-Linux系统门户网站](https://www.linuxidc.com/Linux/2016-10/136597.htm)
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/75B898FD-99D3-40A0-BE3A-99304D250357.png)

## p113-下
### 背景知识：
#### set、env和export命令的区别（做本章题目前，建议先了解）
set命令显示当前shell的变量，包括当前用户的变量;
env命令显示当前用户的变量;
export命令显示当前导出成用户变量的shell变量。

1. 如果直接输入set、env或export，那么会打印出所有相关的变量，可以通过在指令后加入 | grep “mypp”方式输出指定变量名的变量![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/E2414BBC-9D6D-4393-B687-BF02BBE6E79D.png)
2. 见3
3. 只有set中有
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/84F45F63-C2D2-4C93-B0F4-8867E0E2F0D3.png)
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/8860A91D-6E0B-41AC-A89F-A301AC923361.png)
4. 
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/6ED1DE77-D9B3-47B8-A51B-67E6CB884032.png)
5. 输出为空，均不存在,因为shell变了
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/E2414BBC-9D6D-4393-B687-BF02BBE6E79D%202.png)
6. 略
7. 输入exit即可
8. 不存在，因为shell变了
9. 存在，使用export即可将当前变量导出成用户变量，这样env或者export命令就可以看到了
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/DDADA675-D378-4A0D-832A-7D4258BCA16C.png)
10. 11. 12.  可见通过export导出的变量，在同一个用户的另外一个shell也可以看到
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/E5F8B7DB-2FD1-460E-8E3E-BF0488AA1487.png)
## p114
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/8A354736-4EE7-45B6-B205-2553A9B0789A.png)
## p115
1. 主要设置了PATH的本地路径，将本地目录下的bin加入可执行目录中
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/C2191A89-3EDA-4200-9F8E-4AE55B83BB90.png)
2. 这里记录了个人配置文件，我这里没有做多少配置，一些软件的环境变量可以设置在这里，比如讲一些可执行文件目录加入到PATH中
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/B14C51E7-3B58-447B-AC2D-961F4998F8CA.png)
## p115-下
1. 依次输入以下内容：
```
HISTSIZE="10000"
PATH=$PATH:/home/student/cmd
kver=`uname -r`
LANG="zh_CN.UTF-8"
PS1="[\u@\h \t \# \W]\$"
h_start=`wc -l ~/.bash_history | cut -d " " -f 1` 
```
即如下：
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/3A3DD340-52D7-444A-8FFB-3938D4387B1E.png)
2. 输入source ~/.bashrc立刻生效
```
source ~/.bashrc
```
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/F83FF5F0-A38C-42BA-B372-5C217710918B.png)

## p116
1. 加入以下内容到~/.bash_logout
```
date +%Y/%m/%d\ %H:%M >> history.log
```
输出结果如下
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/6A0830E2-D90D-43EC-ADDD-65FF6659DA35.png)
关于输出最新的命令，我没用采用书上方法，因为总是无法输出预期结果，我换了一种方案：
在.bash_logout加入以下代码：
```
history | tail -1 >> history.log
```
然后输出记录
![](Chapter7%20bash%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8%E4%B8%8E%E7%B3%BB%E7%BB%9F%E6%95%91%E6%8F%B4/6B9C03E2-0487-444C-9948-EE69BA19B22A.png)
但是你会发现因为你最后一个命令是logout，所以一直会显示logout，我感觉并不是作者的初衷，所以应该是显示倒数第二条指令，所以我把刚才加入到.bash_logout内容换成:
```
history | tail -n 2 | head -n 1 >> history.log
```
以上代码有点拗口，但是我觉得是对于新手来说比较容易理解，即先输出histroy最后两行然后取第一行，这样就达到了取倒数第二行的效果，如果你有更好的方案，欢迎告诉我。
2. 没有记录