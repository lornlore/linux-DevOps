1.安装ifconfig
    查找安装包：yum list | grep net-tool*
    安装：yum install -y net-tools.x86_64

2.防火墙
    1:查看防火状态
    systemctl status firewalld
    service iptables status
    2:暂时关闭防火墙
    systemctl stop firewalld
    service iptables stop
    3:永久关闭防火墙
    systemctl disable firewalld
    chkconfig iptables off
    
3.开放指定端口
    开放指定端口的方式一：
    在linux中执行： /sbin/iptables -I INPUT -p tcp --dport 6379 -j ACCEPT
    redis默认端口号6379是不允许进行远程连接的，所以在防火墙中设置6379开启远程服务；

    开放指定端口的方式二：
    先开启防火墙才能开放指定端口的：systemctl start firewalld
    firewall-cmd --zone=public --add-port=6379/tcp --permanent
