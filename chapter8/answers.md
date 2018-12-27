# 第八章 bash命令连续执行与数据流重定向
## p123-上
1. var=${变量}
单个花括号内是变量，其效果同 $变量，也就是说花括号这里有没有，都是一样的。
2. var=$(命令)
单个括号内是命令，其命令是运行在一个子shell的环境里面，子shell允许你在不影响当前shell的环境下去执行操作，如果只有一个命令，效果同var=`变量`
如：
![](%E7%AC%AC%E5%85%AB%E7%AB%A0%20bash%E5%91%BD%E4%BB%A4%E8%BF%9E%E7%BB%AD%E6%89%A7%E8%A1%8C%E4%B8%8E%E6%95%B0%E6%8D%AE%E6%B5%81%E9%87%8D%E5%AE%9A%E5%90%91/B620FB4D-B9A2-4B59-9BCB-09B53A14CF78.png)
3. var=$((数学计算式))
双括号内放的是数学计算式，用于算术计算，效果同var=$[数学计算式]。
4. var=“纯文本”
双引号里面的字符串如果有$或者``,那么会替换成变量或者命令
5. var=‘纯文本’
区别于上一条，单引号里面为纯文本，不会替换成变量或者命令。
6. var=`命令`
两个斜点内就是需要执行的命令，这个命令执行完成的结果会赋值给var
参考：[Bash中各种括号的使用 - xibeichengf的专栏 - CSDN博客](https://blog.csdn.net/xibeichengf/article/details/51226052) ,https://blog.csdn.net/weixin_42183399/article/details/80825986

## p123-中
1. 通过which可以找出命令全名
![](%E7%AC%AC%E5%85%AB%E7%AB%A0%20bash%E5%91%BD%E4%BB%A4%E8%BF%9E%E7%BB%AD%E6%89%A7%E8%A1%8C%E4%B8%8E%E6%95%B0%E6%8D%AE%E6%B5%81%E9%87%8D%E5%AE%9A%E5%90%91/EB578F6F-CA24-411C-A083-AB11259C2258.png)
![](%E7%AC%AC%E5%85%AB%E7%AB%A0%20bash%E5%91%BD%E4%BB%A4%E8%BF%9E%E7%BB%AD%E6%89%A7%E8%A1%8C%E4%B8%8E%E6%95%B0%E6%8D%AE%E6%B5%81%E9%87%8D%E5%AE%9A%E5%90%91/099ED33E-E855-415E-AED4-04CB59EEB1CA.png)
2. ls -l `which ifconfig` `which chfn`
![](%E7%AC%AC%E5%85%AB%E7%AB%A0%20bash%E5%91%BD%E4%BB%A4%E8%BF%9E%E7%BB%AD%E6%89%A7%E8%A1%8C%E4%B8%8E%E6%95%B0%E6%8D%AE%E6%B5%81%E9%87%8D%E5%AE%9A%E5%90%91/82A88C4D-C327-425B-A7FF-7F8B7E885153.png)

## p123-下
1. 显示数目为126
![](%E7%AC%AC%E5%85%AB%E7%AB%A0%20bash%E5%91%BD%E4%BB%A4%E8%BF%9E%E7%BB%AD%E6%89%A7%E8%A1%8C%E4%B8%8E%E6%95%B0%E6%8D%AE%E6%B5%81%E9%87%8D%E5%AE%9A%E5%90%91/EC8EF978-2D24-4686-BFCC-7AD826951D15.png)
2. 显示数目为127
![](%E7%AC%AC%E5%85%AB%E7%AB%A0%20bash%E5%91%BD%E4%BB%A4%E8%BF%9E%E7%BB%AD%E6%89%A7%E8%A1%8C%E4%B8%8E%E6%95%B0%E6%8D%AE%E6%B5%81%E9%87%8D%E5%AE%9A%E5%90%91/79113047-A68B-4536-9FE1-1887FF2D494D.png)
3. 找到这么一段话，意思是命令未找到返回127，文件不可执行返回126
![](%E7%AC%AC%E5%85%AB%E7%AB%A0%20bash%E5%91%BD%E4%BB%A4%E8%BF%9E%E7%BB%AD%E6%89%A7%E8%A1%8C%E4%B8%8E%E6%95%B0%E6%8D%AE%E6%B5%81%E9%87%8D%E5%AE%9A%E5%90%91/1FE1FF38-1EB9-4D3C-912A-1E2104180FD5.png)
4. 共有256个
![](%E7%AC%AC%E5%85%AB%E7%AB%A0%20bash%E5%91%BD%E4%BB%A4%E8%BF%9E%E7%BB%AD%E6%89%A7%E8%A1%8C%E4%B8%8E%E6%95%B0%E6%8D%AE%E6%B5%81%E9%87%8D%E5%AE%9A%E5%90%91/792CFC06-A0D1-462A-9D88-4DD6191F5F23.png)
5. 执行完ls /vbird后，输出$?，其结果为2，代表不正确的用法
![](%E7%AC%AC%E5%85%AB%E7%AB%A0%20bash%E5%91%BD%E4%BB%A4%E8%BF%9E%E7%BB%AD%E6%89%A7%E8%A1%8C%E4%B8%8E%E6%95%B0%E6%8D%AE%E6%B5%81%E9%87%8D%E5%AE%9A%E5%90%91/6658399A-D2BE-4AA3-9CA9-E5896674D208.png)
应该还是使用man bash查询返回的数字，因为这个数字是bash返回的。

## p126
ls -d _vbird &> /dev_null || echo non-exist && echo exist
不能，输入结果如下：
![](%E7%AC%AC%E5%85%AB%E7%AB%A0%20bash%E5%91%BD%E4%BB%A4%E8%BF%9E%E7%BB%AD%E6%89%A7%E8%A1%8C%E4%B8%8E%E6%95%B0%E6%8D%AE%E6%B5%81%E9%87%8D%E5%AE%9A%E5%90%91/971E33D6-5680-46B1-B45E-7F86A75E550A.png)
因为non-exist和exist会同时输出

## p128
1. 
![](%E7%AC%AC%E5%85%AB%E7%AB%A0%20bash%E5%91%BD%E4%BB%A4%E8%BF%9E%E7%BB%AD%E6%89%A7%E8%A1%8C%E4%B8%8E%E6%95%B0%E6%8D%AE%E6%B5%81%E9%87%8D%E5%AE%9A%E5%90%91/98F56EB0-1F2B-49DA-B146-68C435DDC320.png)
2. 
![](%E7%AC%AC%E5%85%AB%E7%AB%A0%20bash%E5%91%BD%E4%BB%A4%E8%BF%9E%E7%BB%AD%E6%89%A7%E8%A1%8C%E4%B8%8E%E6%95%B0%E6%8D%AE%E6%B5%81%E9%87%8D%E5%AE%9A%E5%90%91/1D2FABFA-DA4B-4C44-9B4C-766066939FFC.png)
3. 
![](%E7%AC%AC%E5%85%AB%E7%AB%A0%20bash%E5%91%BD%E4%BB%A4%E8%BF%9E%E7%BB%AD%E6%89%A7%E8%A1%8C%E4%B8%8E%E6%95%B0%E6%8D%AE%E6%B5%81%E9%87%8D%E5%AE%9A%E5%90%91/4A312061-1BC8-43E7-8602-696469625A1E.png)
4. 改为：test -e /vbird && echo exist || echo non-exist
![](%E7%AC%AC%E5%85%AB%E7%AB%A0%20bash%E5%91%BD%E4%BB%A4%E8%BF%9E%E7%BB%AD%E6%89%A7%E8%A1%8C%E4%B8%8E%E6%95%B0%E6%8D%AE%E6%B5%81%E9%87%8D%E5%AE%9A%E5%90%91/5151F9E8-97F9-4897-8D4D-D0C52CF147F6.png)
## p129
1. [ -e "/etc" ] && echo exist || echo non-exist
![](%E7%AC%AC%E5%85%AB%E7%AB%A0%20bash%E5%91%BD%E4%BB%A4%E8%BF%9E%E7%BB%AD%E6%89%A7%E8%A1%8C%E4%B8%8E%E6%95%B0%E6%8D%AE%E6%B5%81%E9%87%8D%E5%AE%9A%E5%90%91/7BE7A7DA-0B35-4B34-A001-2006466EF01F.png)
2. 
![](%E7%AC%AC%E5%85%AB%E7%AB%A0%20bash%E5%91%BD%E4%BB%A4%E8%BF%9E%E7%BB%AD%E6%89%A7%E8%A1%8C%E4%B8%8E%E6%95%B0%E6%8D%AE%E6%B5%81%E9%87%8D%E5%AE%9A%E5%90%91/1DD0291A-5AA6-4617-AFBD-EC1FCC1473FF.png)
3. 
![](%E7%AC%AC%E5%85%AB%E7%AB%A0%20bash%E5%91%BD%E4%BB%A4%E8%BF%9E%E7%BB%AD%E6%89%A7%E8%A1%8C%E4%B8%8E%E6%95%B0%E6%8D%AE%E6%B5%81%E9%87%8D%E5%AE%9A%E5%90%91/54FCCF5B-415C-4749-BFEC-796AE7C4979B.png)

# p131-上
3. 会提示是否覆盖 
![](%E7%AC%AC%E5%85%AB%E7%AB%A0%20bash%E5%91%BD%E4%BB%A4%E8%BF%9E%E7%BB%AD%E6%89%A7%E8%A1%8C%E4%B8%8E%E6%95%B0%E6%8D%AE%E6%B5%81%E9%87%8D%E5%AE%9A%E5%90%91/BC7D4E9A-3366-4861-95E2-43A342B9A85C.png)
4. 既然系统的cp别名会提示：是否覆盖，那么直接调用系统原来的命令即可，即：_bin_cp -r _etc_* ./ 

# p131-中间
1. alias cp="cp -i"
2. alias mv=“mv -i"
3. alias rm=“rm -i"

# p131-下方
1. alias geterr="echo \"I am error\" 1>&2"
2. 
![](%E7%AC%AC%E5%85%AB%E7%AB%A0%20bash%E5%91%BD%E4%BB%A4%E8%BF%9E%E7%BB%AD%E6%89%A7%E8%A1%8C%E4%B8%8E%E6%95%B0%E6%8D%AE%E6%B5%81%E9%87%8D%E5%AE%9A%E5%90%91/0C25154B-0449-4D78-84BE-D9D8A67195CA.png)
3. 4.
![](%E7%AC%AC%E5%85%AB%E7%AB%A0%20bash%E5%91%BD%E4%BB%A4%E8%BF%9E%E7%BB%AD%E6%89%A7%E8%A1%8C%E4%B8%8E%E6%95%B0%E6%8D%AE%E6%B5%81%E9%87%8D%E5%AE%9A%E5%90%91/605C3A60-3BFB-408F-BEF3-AE08038A3AFC.png)
无输出
5. 1>&2 代表命令将正确的输出流转到了错误输出流中，那么3和4意思是将错误错误流输入到一个空设备（_dev_null）中，因此是没有任何输出的，那么为什么第三条命令有输出而第四条命令没有呢？括号代表信息汇总，将这个命令内所有信息统一进行输出了。
# p133
1. 查找/etc文件夹下包含passwd的配置文件，然后进行输出，其中*是通配符
![](%E7%AC%AC%E5%85%AB%E7%AB%A0%20bash%E5%91%BD%E4%BB%A4%E8%BF%9E%E7%BB%AD%E6%89%A7%E8%A1%8C%E4%B8%8E%E6%95%B0%E6%8D%AE%E6%B5%81%E9%87%8D%E5%AE%9A%E5%90%91/C468D1BB-782A-4A40-9D54-0B2BF8614E67.png)
2. 将错误输出命令（即这里的permission denied命令）转向到_dev_null空设备中
![](%E7%AC%AC%E5%85%AB%E7%AB%A0%20bash%E5%91%BD%E4%BB%A4%E8%BF%9E%E7%BB%AD%E6%89%A7%E8%A1%8C%E4%B8%8E%E6%95%B0%E6%8D%AE%E6%B5%81%E9%87%8D%E5%AE%9A%E5%90%91/BA4F3DC1-0518-4C84-8E6F-440F51C9C5D1.png)
3. find _etc -name '_**_passwd_**_' 2>_dev/null 1>find_passwd.txt
4. find _etc -name '_**_shadow_**_' 2>_dev/null 1>>find_passwd.txt 
5. 打开后发现
![](%E7%AC%AC%E5%85%AB%E7%AB%A0%20bash%E5%91%BD%E4%BB%A4%E8%BF%9E%E7%BB%AD%E6%89%A7%E8%A1%8C%E4%B8%8E%E6%95%B0%E6%8D%AE%E6%B5%81%E9%87%8D%E5%AE%9A%E5%90%91/49EE72CB-3E32-4C20-958F-BF1D512B26CF.png)
# p134
3. 
![](%E7%AC%AC%E5%85%AB%E7%AB%A0%20bash%E5%91%BD%E4%BB%A4%E8%BF%9E%E7%BB%AD%E6%89%A7%E8%A1%8C%E4%B8%8E%E6%95%B0%E6%8D%AE%E6%B5%81%E9%87%8D%E5%AE%9A%E5%90%91/834B392E-723A-44B0-8483-6FC4BB10E3CD.png)
4. cat mycat.txt
5. cat _etc_hosts >> mycat.txt 
# p135-上
1. find _etc_ -name "*.conf"
2. find _etc_ | grep ".conf"
3. find _etc_ | grep ".conf" | wc -l
# p135-下
1. cat _etc_passwd |awk  -F ':'  '{print $1,$7}'  
2. cat _etc_passwd |awk  -F ':'  '{print $7}'| uniq -c
![](%E7%AC%AC%E5%85%AB%E7%AB%A0%20bash%E5%91%BD%E4%BB%A4%E8%BF%9E%E7%BB%AD%E6%89%A7%E8%A1%8C%E4%B8%8E%E6%95%B0%E6%8D%AE%E6%B5%81%E9%87%8D%E5%AE%9A%E5%90%91/9609322E-AFBD-4F93-86B2-90FE9D696E14.png)
3. last |awk  -F ' '  '{print $1}'| uniq -c
![](%E7%AC%AC%E5%85%AB%E7%AB%A0%20bash%E5%91%BD%E4%BB%A4%E8%BF%9E%E7%BB%AD%E6%89%A7%E8%A1%8C%E4%B8%8E%E6%95%B0%E6%8D%AE%E6%B5%81%E9%87%8D%E5%AE%9A%E5%90%91/17A33159-E8C4-40C8-8CA8-74FC2BA90765.png)
4. ip addr show | grep -E "([0-9]{1,3}[\.]){3}[0-9]{1,3}"
![](%E7%AC%AC%E5%85%AB%E7%AB%A0%20bash%E5%91%BD%E4%BB%A4%E8%BF%9E%E7%BB%AD%E6%89%A7%E8%A1%8C%E4%B8%8E%E6%95%B0%E6%8D%AE%E6%B5%81%E9%87%8D%E5%AE%9A%E5%90%91/B9424441-1762-441A-8725-4607E3A65D1A.png)
5. ip addr show | awk  -F ' '  '{print $2}'
6. ip addr show | awk  -F ' '  '{print $2}' > _dev_shm/myip.txt




