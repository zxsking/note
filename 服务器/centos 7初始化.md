## 1.关闭防火墙

### 停止firewall

```shell
systemctl stop firewalld.service
```

### 禁止firewall开机启动

```shell
systemctl disable firewalld.service 
```



## 2.修改网络配置文件

```shell
vim /etc/sysconfig/network-scripts/ifcfg-ens32
```

```
TYPE="Ethernet"
BOOTPROTO="static"
NAME="ens32"
UUID="dba727df-eb7f-47e5-a48f-ce5d7fdeae24"
DEVICE="ens32"
ONBOOT="yes"
GATEWAY=192.168.29.0	   	#要与虚拟机nat设置中的网关相一致 不然就会出先 ping 不通的情况
IPADDR=192.168.29.100
NETMASK=255.255.255.0
DNS1=114.114.114.114
DNS2=8.8.8.8    
```

## 3.解决冲突并重启网络服务

`linux`里两个网络配置工具`network`和`NetworkManager`冲突  所以我们禁用一下`NetworkManager `重启网络服务时则不会再报错

```shell
systemctl stop NetworkManager
```

```shell
systemctl disable NetworkManager
```

```shell
systemctl restart network.service
```

