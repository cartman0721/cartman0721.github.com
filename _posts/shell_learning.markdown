Title: shell 学习记录
Author: Dazuo Sun
Date: Thur May 17 2012 17:13:00 GMT+0800 (China Standard Time)
Lang: shell

  上两周学习shell效果明显，把公司里的ci脚本看了下（公司那个脚本写的太罗嗦了，优化空间很大），虽然没有非常深入，
但是对付平常工作已经绰绰有余了，想到公司里那个工作十几年的架构师连在日志里查找某个字符串都不太会（他用个工具把日志同步到装了windows的本地
，再用UE打开，再ctrl+find），把一些常用到mark下

####常用的命令：
1.找日志文件里是否包含字符串：

    cartman@ubuntu:~/test$ grep -i sundazuo test.txt
    sundazuo

2.ctrl+replace 将sundazuo 替换为cartman

    cartman@ubuntu:~/test$ sed -i 's/sundazuo/cartman/g' test.txt

3.查看端口占用情况

    netstat -aon|grep 80

4.查找历史命令

    Ctrl+r

5.远程同步
    
    rsync  "hz\dazuo.sundz"@10.250.4.110:/home/dazuo.sundz/* .
    Password: 
6.统计文件大小

    du -h --max-depth=1
7.删除找到到文件

    find . -name 'test.txt' -exec rm -rf {} +




   