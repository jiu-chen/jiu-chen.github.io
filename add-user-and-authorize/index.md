# linux下添加用户并授权


添加Linux用户并为添加的用户授予root权限  
System: Centos7

## 添加用户rock
``` bash
adduser rock  
```
## 修改用户密码
``` bash
passwd rock
```

## 授权
因为个人用户只拥有当前home目录下的所有权限, 无法查看或修改其他用户目录。使用sudo可以获取到root权限。然而，新建的用户无法使用sudo命令，需要先对用户进行授权。  
编辑 /etc/sudoers 文件
``` bash
chmod -v u+w /etc/sudoers
vim /etc/sudoers
```
在  
`root ALL=(ALL)  ALL`  
下面加入一行  
`rock ALL=(ALL)  ALL`  
后 wq 保存文件  
如果你想要使用sudo的时候不需要密码，则加入  
`rock ALL=(ALL) NOPASSWD:ALL`  
收回sudoers的写权限
``` bash
chmod -v u-w /etc/sudoers
```
退出并用新用户重新登陆， 此时新用户将可以使用 sudo 来获取root权限  

## 删除user
``` bash
userdel rock
```


## 关于chmod命令
全称: change mode, 用于控制用户对文件的权限  
{{< figure src="/images/chmod.jpeg" title="文件权限" >}}
```
-v: 显示权限变更的详细资料
-u 表示该文件的拥有者，g 表示与该文件的拥有者属于同一个群体(group)者，o 表示其他以外的人，a 表示这三者皆是。
+ 表示增加权限、- 表示取消权限、= 表示唯一设定权限。
```
所以 `u+w`表示给文件拥有者加入写权限

