# Linux相关的笔记

## linux简介

## 定时任务crontab命令

​	**crontab命令** 被用来提交和管理用户的需要周期性执行的任务，当安装完成操作系统后，默认会安装此服务工具，并且会自动启动crond进程，crond进程每分钟会定期检查是否有要执行的任务，如果有要执行的任务，则自动执行该任务。

常用参数 -e -l

```shell
crontab -e
# crontab -e会进入编辑界面，再后面写上内容即可
crontab -l
# crontab -l可以查看内容
# crontab -r会清除该用户所有定时任务，一般不用
crontab -l
# Edit this file to introduce tasks to be run by cron.
#
# Each task to run has to be defined through a single line
# indicating with different fields when the task will be run
# and what command to run for the task
#
# To define the time you can provide concrete values for
# minute (m), hour (h), day of month (dom), month (mon),
# and day of week (dow) or use '*' in these fields (for 'any').
#
# Notice that tasks will be started based on the cron's system
# daemon's notion of time and timezones.
#
# Output of the crontab jobs (including errors) is sent through
# email to the user the crontab file belongs to (unless redirected).
#
# For example, you can run a backup of all your user accounts
# at 5 a.m every week with:
# 0 5 * * 1 tar -zcf /var/backups/home.tgz /home/
#
# For more information see the manual pages of crontab(5) and cron(8)
#
# m h  dom mon dow   command
# * 0,12 * * * /bin/bash /home/zhilin/docs_build.sh >> docs_build.log 2>&1

```

可以看到分最前面分别有5个空格分开的参数，后面接上shell命令，5个参数分别是分，时，日，月，周，它们的参数可选范围分别是0-59，0-23，1-31，1-12，0-6之间的整数，其中最后一个0表示最期日。

特殊字符

`*`表示所有值，比如在分里就是0-59，在月里就是1-31

`,`表示取多个值，比如周一周二周三可以在表示周的地方写成1,2,3

`-`表示范围，比如周一到周五可以用1,2,3,4,5也可以用1-5

`/`表示频率，分里面`*/2`可以表示每两分钟

```
实例
每1分钟执行一次command
* * * * * command

每小时的第3和第15分钟执行
3,15 * * * * command

在上午8点到11点的第3和第15分钟执行
3,15 8-11 * * * command

每隔两天的上午8点到11点的第3和第15分钟执行
3,15 8-11 */2 * * command
每个星期一的上午8点到11点的第3和第15分钟执行
3,15 8-11 * * 1 command

每晚的21:30执行command 
30 21 * * * command

每月1、10、22日的4 : 45执行command 
45 4 1,10,22 * * command

每周六、周日的1:10执行command
10 1 * * 6,0 command

每天18 : 00至23 : 00之间每隔30分钟执行command
0,30 18-23 * * * command

每星期六的晚上11:00 执行
0 23 * * 6 command

每一小时执行
* */1 * * * command

晚上11点到早上7点之间，每隔一小时执行command
* 23-7/1 * * * command

每月的4号与每周一到周三的11点执行command
0 11 4 * mon-wed command

一月一号的4执行command
0 4 1 jan * command

每小时执行command
01 * * * * command
```

crontab定时任务执行时可能会遇到的问题，比如你装了一个vue的npm工具在自己用户目录的bin里面，shell脚本里用到了npm并且没有问题，用crontab执行shell脚本里会发现执行失败，原因是shell脚本PATH变量默认的话没有用户bin目录，可以在用到之前写上`PATH=/home/user_name/bin:$PATH`user_name为用户名，若要查看定时任务执行的脚本的日志，可以在执行命令后面加上重定向内容，比如`* * * * * /bin/bash test.sh >>test.log 2>&1`每分钟执行一次并追加写上日志。