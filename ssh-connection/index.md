# ssh连接远程虚拟机

system: centos7  
通过ssh连接远程虚拟机首先当前client安装了ssh, 使用
``` bash
ssh -V
```
命令可以查看ssh版本
```
$ ssh -V
OpenSSH_7.9p1, LibreSSL 2.7.3
```

## ping
通过ping命令目标虚拟机可以check网络是否联通
```
$ ping 10.211.55.3
PING 10.211.55.3 (10.211.55.3): 56 data bytes
64 bytes from 10.211.55.3: icmp_seq=0 ttl=64 time=0.217 ms
64 bytes from 10.211.55.3: icmp_seq=1 ttl=64 time=0.318 ms
^C
```

## telnet
通过telnet命令check目标虚拟机对应端口是否开放, ssh默认端口是22
```
$ telnet 10.211.55.3 22
Trying 10.211.55.3...
Connected to juzis-mbp.client.tw.trendnet.org.
Escape character is '^]'.
SSH-2.0-OpenSSH_7.9
```
## ssh 
通过ssh连接
```
$ ssh jc@10.211.55.3 
jc@10.211.55.3's password:
```
输入密码即可，如果目标虚拟机的ssh端口不是22, 需要带上参数 `-p port_number`  

如果连接失败，出现connection reused, 需要在目标机器上排查:  
### 1. sshd service是否active  
``` bash
service sshd status
```
如果出现: `Unit sshd.service could not be found`  
安装openssh-server
``` bash
sudo yum install openssh-server
```
然后启动sshd service:  
``` bash
service sshd start
```
不启动的话 service status 是 `inactive (dead)`  
启动之后:  
```
[jc@CentOS7 ~]$ service sshd status
Redirecting to /bin/systemctl status sshd.service
● sshd.service - OpenSSH server daemon
   Loaded: loaded (/usr/lib/systemd/system/sshd.service; enabled; vendor preset: enabled)
   Active: active (running) since Sat 2021-05-29 09:48:53 CST; 24min ago
     Docs: man:sshd(8)
           man:sshd_config(5)
 Main PID: 1012 (sshd)
   CGroup: /system.slice/sshd.service
           └─1012 /usr/sbin/sshd -D
```
这是最常见的原因之一;

### 2. ssh端口号不是22
在目标机上查看 `/etc/ssh/sshd_config`中的`Port`值

如果连接失败提示permission不对，则可能需要修改`/etc/ssh/sshd_config`中的`PubkeyAuthentication`等参数；


