# CentOS7 最小安装后配置

```shell
yum -y install wget
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
sed -i -e '/mirrors.cloud.aliyuncs.com/d' -e '/mirrors.aliyuncs.com/d' /etc/yum.repos.d/CentOS-Base.repo

wget -O /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-7.repo

wget -O /etc/yum.repos.d/docker-ce.repo  https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
# cd /etc/yum/repos.d/
# wget https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
yum clean all
yum makecache fast
yum -y install ntpdate git vim net-tools lrzsz libnl iw NetworkManager-wifi
systemctl disable firewalld
systemctl stop firewalld
sed -i "s/SELINUX=enforcing/SELINUX=disabled/g" /etc/sysconfig/selinux  
mv /etc/sysconfig/network-scripts/ifcfg-enp7s0 /etc/sysconfig/network-scripts/ifcfg-eth0
sed -i "s/DEVICE=enp7s0/DEVICE=eth0/g" /etc/sysconfig/network-scripts/ifcfg-eth0
sed -i "s/NAME=enp7s0/NAME=eth0/g" /etc/sysconfig/network-scripts/ifcfg-eth0

vim /etc/sysconfig/grub
GRUB_CMDLINE_LINUX="crashkernel=auto rd.lvm.lv=centos_g460/root net.ifnames=0 biosdevname=0 rd.lvm.lv=centos_g460/swap rhgb quiet"

grub2-mkconfig -o /boot/grub2/grub.cfg


vim /etc/systemd/logind.conf
#文件中添加一行配置
HandleLidSwitch=ignore
#保存退出后重庆操作系统即可
```

