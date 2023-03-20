###常用系统日志
- dmesg
主要记录系统在开机时内核检测过程所产生的信息，通过执行 dmesg 命令查看
- /var/log/wtmp or /var/log/faillog
这两个文件可以记录正确登陆系统者的账户信息，与错误登陆时所使用的账户信息，last 命令就是读取 wtmp 文件来获取的
- /var/log/btmp
记录错误登陆日志，这个文件是二进制的 不能使用 cat 命令查看 而要使用 lastb 命令查看
- /var/run/utmp
记录当前一登陆用户的信息，同样不能使用 cat 命令查看 而要使用 w,who,users 命令来查询
- /var/log/lastlog
记录了系统上面所有账户最近一次登陆系统时的相关信息，lastlog 命令就是读取这个文件里的记录来显示的
- /var/log/secure
只要涉及到需要用户名和密码的操作，那么当登陆系统是 不论正确错误 都会记录到这里
- /var/log/messages
这个文件非常重要，几乎系统发生的错误信息 或者重要信息都会被记录在这里
- /var/log/cron
主要记录关于crontab 计划任务的相关信息，比如 系统计划任务的错误配置 计划任务的修改等
- /var/log/malilog or /var/log/
记录着邮件的往来信息，默认是 postfix 邮件服务器的一些信息
