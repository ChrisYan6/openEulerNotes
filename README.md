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

#网络功能
###使用ifcfg文件配置静态网络
在/etc/sysconfig/network-scripts/ 目录中生成的ifcfg-enp4s0的文件中修改配置
```
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
DEVICE=enp4s0
BOOTPROTO=none
ONBOOT=yes
IPADDR=192.168.0.10
PREFIX=24
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=enp4s0static
UUID=08c3a30e-c5e2-4d7b-831f-26c3cdc29293
```
然后执行systemctl reload NetworkManager命令重新加载配置
###使用ifcfg配置网关
/etc/sysconfig/network文件
`GATEWAY=192.168.0.1`

###使用IP命令配置网络
`ip addr [add|del] address dev interface-name`
例如
`ip address add 192.168.0.10/24 dev enp3s0`
指令立即生效但重启后消失
###路由
`ip route [add|del|change|append|replace] destination-address`
显示路由表
'ip route'
例如
```
ip route add 192.168.2.1 via 10.0.0.1 [ dev interface name]
ip route add 192.168.2.0/24 via 10.0.0.1 [ dev interface name]
```

#systemctl
```
systemctl start network.service
systemctl stop network.service
systemctl restart network.service
systemctl reload netwrok.service
systemctl status network.service
systemctl enable network.service
systemctl disable network.service

systemctl list-units --type service  #列出当前运行的服务

systemctl rescue #进入救援模式
systemctl emergency #进入紧急模式
```

###Linux启动流程
电源
BIOS/UEFI
Bootloader
MBR/GPT
GRUB/GRUB2
加载内核
|说明|传统模式|新模式|
|----|----|----|
|第一个进程|init|systemd|
|运行级别|/etc/inittab(默认是3)|etc/systemd/system/default.target(默认multi-user.target)|
|初始化|etc/init.d/boot|usr/lib/systemd/system/sysinit.taiget|
|服务|串行启动|并行启动|
|登录|/sbin/mingetty|/sbin/agetty|
开启shell
