# Chapter6文件系统的基本管理
## p91 
1. 超过2TB以上的磁盘会默认使用GPT的分区表
2. 由于主分区和扩展分区最多可以是四个，扩展分区最多只能有一个，又因为题目说了有两个主分区，那么可以这样排版：主分区、主分区、扩展分区（扩展分区再分3个逻辑分区）
> 文件可以分为这样：/dev/sdb1 /dev/sdb2 /dev/sdb5 /dev/sdb6 /dev/sdb7  
> 其中/dev/sdb5 /dev/sdb6 /dev/sdb7 是由/dev/sdb3扩展的，另外/dev/sdb4是保留给主分区和扩展分区的，不能使用  
3. 由于只剩余两个分区了，可以是一个扩展+一个主分区或者2个主分区，因为需要4个分区，所以肯定不能使用第二种方案，所以使用一个扩展分区，分出四块大小约100G的空间。

## p93 
1. EXT2除了metadata区块外，还有superblock、inode和block三个重要的区块，其作用分别是：superblock：整个文件系统的综合概要信息所在；inode：记录文件的属性以及文件是存放在哪个block内；block：实际数据的存放区，分为1KB、2KB和4KB
2. inode 区块内
3. block区块内
4. 每个文件只会占用一个inode，至少占用一个block（小于一个block大小的数据会造成block内部的空间浪费）
5. inode为128B，block可以为1KB或2KB或4KB

# p93
1. 本例我用的是阿里云的云主机，其文件系统是EXT4，以下运行后可以看到inode的编号
![](Chapter6%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E7%9A%84%E5%9F%BA%E6%9C%AC%E7%AE%A1%E7%90%86/3ADF56F8-CB69-4E79-A3F2-96234528E265.png)
2. 两个文件的inode是一样的，注意这里的一点.代表指向本文件夹，也算一个文件夹哦，具体分析见下面的第3题
![](Chapter6%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E7%9A%84%E5%9F%BA%E6%9C%AC%E7%AE%A1%E7%90%86/D91DDD30-7F7B-4235-A47C-71272F98B878.png)
3. 这题显示2，这里的2代表这个文件夹内默认链接数（可以简单理解成该文件夹内的文件夹数量），就是题目所说的连接字段的数量（其实下一页p94页就讲到这个知识点了）
![](Chapter6%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E7%9A%84%E5%9F%BA%E6%9C%AC%E7%AE%A1%E7%90%86/06DCAA40-980B-498E-B4AE-E5B41E29A022.png)为什么这个空文件是2呢？按道理来说空文件内没有文件夹，不是0吗？我们进入该文件夹看下详细信息
![](Chapter6%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E7%9A%84%E5%9F%BA%E6%9C%AC%E7%AE%A1%E7%90%86/CCB4BE0F-0598-458B-902D-AA466388D2F8.png)
可以看到文件属性前面的d代表文件夹，确实有两个（指向本目录和指向上层目录的文件夹，这个文件夹有点特殊，属于链接文件，这也是有点难理解的地方），注意这里查看文件夹所有文件的时候一定要加上参数-a，代表查看所有的，包括隐藏文件。
4. 运行的命令是： ll -id /tmp/inodecheck/ /tmp/inodecheck/. /tmp/inodecheck/check2/..
![](Chapter6%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E7%9A%84%E5%9F%BA%E6%9C%AC%E7%AE%A1%E7%90%86/ACBD0A1E-3C5B-4D52-BE6C-7614FABFA737.png)
先分析inode，这几个inode编号都是一样的，因为这三个文件夹指向的都是/tmp/inodecheck/目录，其中一点代表本文件夹，两点代表上一层文件夹
![](Chapter6%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E7%9A%84%E5%9F%BA%E6%9C%AC%E7%AE%A1%E7%90%86/B74F1C20-E6DD-49B8-AFC3-971C0D384DE8.png)
但是第二个字段从2变成了3，因为刚刚新建了一个文件夹check2，所以目录树就增加一个了
## p94
1. 略
2. 复制后查看，可发现文件夹链接数是1，可以理解，因为是直接复制过来的
![](Chapter6%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E7%9A%84%E5%9F%BA%E6%9C%AC%E7%AE%A1%E7%90%86/8ED24615-6BCF-45F3-BC26-C50008B742A5.png)
3. 完全相同，实体链接
![](Chapter6%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E7%9A%84%E5%9F%BA%E6%9C%AC%E7%AE%A1%E7%90%86/1A764167-7568-434C-A0A6-675111EC0C7A.png)
4. 符号链接，权限 和 链接数都不同，而且文件名有一个箭头->
![](Chapter6%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E7%9A%84%E5%9F%BA%E6%9C%AC%E7%AE%A1%E7%90%86/22322C6E-717C-4935-AAD3-DC8A413C5CB8.png)
5. 内容全部相同
![](Chapter6%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E7%9A%84%E5%9F%BA%E6%9C%AC%E7%AE%A1%E7%90%86/A99FE35C-3C3B-49F6-9E0D-E3C28FC7F970.png)
6. 删除后首先符号链接名称变成了红色，实体链接的链接数从2变成了1
![](Chapter6%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E7%9A%84%E5%9F%BA%E6%9C%AC%E7%AE%A1%E7%90%86/6F687513-7C6E-40DA-ADE0-304CC85E6538.png)
7. 实体链接依然能显示，而符号链接直接出错，显示不存在此文件或者文件夹
![](Chapter6%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E7%9A%84%E5%9F%BA%E6%9C%AC%E7%AE%A1%E7%90%86/827D5A09-EBB6-4148-9BCB-485B545342C4.png)
8. 作者让写ln /etc/hosts.（有一个点号）我觉得应该没有点号，应该是作者的笔误
![](Chapter6%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E7%9A%84%E5%9F%BA%E6%9C%AC%E7%AE%A1%E7%90%86/68A424F5-95EF-4CA2-9EEA-C9F76A6B1788.png)
使用命令后显示不能创建文件链接，因为文件不能跨设备（当前目录在/dev/shm内存上，而etc配置文件在硬盘里面）
## p94 
1. 将文件系统与目录树结合的方式成为挂载，挂载点一定是目录，该目录为进入该文件系统的入口。
2. 我用df -T查询了下我在阿里云的centos 7.4，如下
![](Chapter6%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E7%9A%84%E5%9F%BA%E6%9C%AC%E7%AE%A1%E7%90%86/D363ACA5-F406-4467-9A7E-0843B95ECC16.png)
并没有看到xfs系统，我查了下，xfs是日志文件系统，而centos现在普遍使用ext4日志文件系统，因此这里可能和作者想考察的不太一样。
3. 我这里只有挂载点/ inode是2，如果安装时候为/boot 和/home选择了独立的分区，那么你这里inode也应该是2，我用的是阿里云的云主机，一共就40GB空间，没有为我单独分区。
![](Chapter6%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E7%9A%84%E5%9F%BA%E6%9C%AC%E7%AE%A1%E7%90%86/E9D291FA-9F2A-49FE-9EC3-5607C39FB2D6.png)
4. 如果你是用的鸟哥镜像或者安装centos的时候为/、/boot和/home选择了独立的分区，那么这三个的inode应该一样，都是2，我这里显示是不一样的，是因为这三个属于同一个文件系统内，阿里云在为我安装的时候并没有做独立分区操作。

## p95
1. 阿里云显示如下：
![](Chapter6%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E7%9A%84%E5%9F%BA%E6%9C%AC%E7%AE%A1%E7%90%86/D235642B-71DC-4107-B080-4D57CF543421.png)
腾讯云显示如下：
![](Chapter6%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E7%9A%84%E5%9F%BA%E6%9C%AC%E7%AE%A1%E7%90%86/9AD22002-D5E1-45A3-BF3C-54061ECBE496.png)
2. 我试了下lsblk -all，显示如下：
![](Chapter6%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E7%9A%84%E5%9F%BA%E6%9C%AC%E7%AE%A1%E7%90%86/FAF08079-1A1B-4225-A9B0-A3D249DDAF4A.png)
并没有完整显示设备名（/dev/vda1），我没有找到lsblk能列出完整命令的选型，于是我试了这个命令：fdisk -l
![](Chapter6%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E7%9A%84%E5%9F%BA%E6%9C%AC%E7%AE%A1%E7%90%86/8722ECA9-73BA-42C7-A4B9-3D33CBA98BCF.png)
可以看到vda1完整的设备名是/dev/vda1，接下来就可以用parted 打印出来啦
3. 可见分区表是MBR分区（显示的是msdos）
![](Chapter6%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E7%9A%84%E5%9F%BA%E6%9C%AC%E7%AE%A1%E7%90%86/8AC42C64-5A99-4C8A-B7BE-982C429BBD03.png)
## p97
1. 由于我的系统不是GPT分区，书上提到的gdisk均采用fdisk命令进行
![](Chapter6%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E7%9A%84%E5%9F%BA%E6%9C%AC%E7%AE%A1%E7%90%86/B9F8AA1C-509E-4C94-B3FF-D1AC5CF30455.png)
2. 输入p显示如下：
![](Chapter6%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E7%9A%84%E5%9F%BA%E6%9C%AC%E7%AE%A1%E7%90%86/99842034-8406-4D3B-BFDE-5D34A3C6E245.png)
3. 3-7 此处跟着作者敲一遍即可，过程略

[未完待续]