# docker容器和宿主机之间相互拷贝文件


开发过程中常常需要将宿主机的文件拷贝到docker容器中，或将docker容器中的文件拷贝出来到宿主机。
## 拷贝到docker容器
``` bash
docker cp file_name container_name:/tmp
```
比如将文件a.txt拷贝到mysql容器下的tmp目录
```
docker cp a.txt mysql:/tmp
```
进入docker容器查看是否拷贝成功
```
docker exec -it mysql /bin/bash
cd /tmp
ls
```

## 拷贝到宿主机
只需要反过来写即可
``` bash
docker cp container_name:/xxx/filename .
```
比如将mysql容器中/tmp/b.txt拷贝到宿主机当前文件
```
docker cp mysql:/tmp/b.txt .
```
`ls`命令查看是否拷贝成功


拷贝文件夹不需要 `-r` 参数, 依然使用 `docker cp`
