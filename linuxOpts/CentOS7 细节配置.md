# CentOS7 细节配置

### 1.笔记本安装CentOS7关盖子,系统不休眠设置

```shell
vim /etc/systemd/logind.conf
#文件中添加一行配置
HandleLidSwitch=ignore
#保存退出后重庆操作系统即可
```

### 2.无线网卡配置

```
ip link set wlp3s0 up
wpa_supplicant -B -i wlp3s0 -c <(wpa_passphrase "WiFi 名称" "密码")	
dhclient wlp3s0
```

### 3.修改mysql镜像源为清华大学源

```bash
#失败!总之把清华源的mysql该掉mysql原有的源

sed -i "s@http://repo.mysql.com/yum/mysql-5.7-community/el/7/$basearch/@https://mirrors.tuna.tsinghua.edu.cn/mysql/yum/mysql57-community-el7@g" /etc/yum.repos.d/mysql-community.repo
```

