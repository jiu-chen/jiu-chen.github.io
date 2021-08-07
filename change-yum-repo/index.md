# 修改centos7 yum源

system: Centos 7  
装好centos之后，为了方便下载一些软件，常常需要更换yum源  
默认的yum源配置在 `/etc/yum.repos.d/CentOS-Base.repo`中
```
[base]
name=CentOS-$releasever - Base
mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
#baseurl=http://mirror.centos.org/centos/$releasever/os/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
```
更换阿里源  
## 备份默认的yum源
``` bash
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
```

## 下载阿里源
``` bash
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
```
阿里源配置:  
```
[base]
name=CentOS-$releasever - Base - mirrors.aliyun.com
failovermethod=priority
baseurl=http://mirrors.aliyun.com/centos/$releasever/os/$basearch/
        http://mirrors.aliyuncs.com/centos/$releasever/os/$basearch/
        http://mirrors.cloud.aliyuncs.com/centos/$releasever/os/$basearch/
gpgcheck=1
gpgkey=http://mirrors.aliyun.com/centos/RPM-GPG-KEY-CentOS-**7**
```
## 生成本地缓存
``` bash
yum makecache 
```
yum makecache 是 将服务器上的软件包信息 现在本地缓存,以提高 搜索 安装软件的速度
更换源成功  

## 查看当前源列表
```bash
sudo yum repo list
```

## about wget
wget是一个下载文件的工具, 比如下载安装包:
``` bash
wget https://golang.org/dl/go1.16.4.linux-amd64.tar.gz
```
参数 -O –output-document=FILE下载文件保存为别的文件名
