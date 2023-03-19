vagrant常用命令:
vagrant box add 添加box
vagrant init    初始化box
vagrant up   启动本地环境
vagrant ssh  通过ssh登录本地环境所在虚拟机(xshell显示不出来，？?)
vagrant halt    关闭本地环境
vagrant suspend 暂停本地环境,虚拟机内存等信息将以状态文件的方式保存在本地，可以执行恢复操作后继续使用
vagrant resume  恢复本地环境,与前面的暂停相对应
vagrant reload  修改了Vagrantfile后，使之生效，重新加载
vagrant destroy 彻底移除本地环境,删除后在当前虚拟机所做进行的除开Vagrantfile中的配置都不会保留
vagrant box list    显示当前已经添加的box列表
vagrant box remove  删除相应的box
vagrant package 打包命令，可以把当前的运行的虚拟机环境进行打包
vagrant plugin  用于安装卸载插件
vagrant status  获取当前虚拟机的状态
vagrant global-status   显示当前用户Vagrant的所有环境状态

1.下载box
vagrant box add centos7 https://mirrors.ustc.edu.cn/centos-cloud/centos/7/vagrant/x86_64/images/CentOS-7.box

2.初始化,初始化会得到vagrantfile
vagrant init

3.设置vagrantfile，实现多个vm

4.多个虚拟机之间无法PING通
  使用Vagrant生成虚拟机后，xu你寄可以PING通主机，但是主机通过ETH0显示的IP无法PING通虚拟机，这是因为VAGRANT使用的是ETH0做SSH，默认IP地址是10.0.2.15，所以一直无法PING通，后续安装K8S也需要注意
该问题，K8S的默认网卡也是ETH0，所以要调整至使用ETH1网络，步骤如下：
  4.1连接至虚拟机    ：   vagrant ssh
  4.2查看网卡状态    ：   ifconfig -a
  4.3发现要用的ETH1网卡并没有启动，所以启动ETH1      :     sudo  ifconfig eth1 up
  4.4重启网络服务       ：     sudo /etc/init.d/networking restart
  4.5更新IP地址         :      sudo dhclient eth1
  4.6关闭防火墙以备后用  :       sudo ufw disable
