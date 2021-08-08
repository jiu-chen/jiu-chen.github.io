# mac go grpc环境准备



1. 安装protobuf

源码安装: https://zhuanlan.zhihu.com/p/60471892
```shell
# 下载 https://github.com/protocolbuffers/protobuf/releases 
# 选择 protobuf-all-3.17.3.tar.gz
# 解压
# 设置编译目录
$ ./configure --prefix=/usr/local/protobuf
# 安装
$ make
$ make install
# 配置环境变量 .zshrc, 添加:
# export PROTOBUF=/usr/local/protobuf 
# export PATH=$PROTOBUF/bin:$PATH
$ source ~/.zshrc
$ protoc --version
libprotoc 3.17.3
```

2. 安装protoc的Go插件

```shell
go get -u github.com/golang/protobuf/protoc-gen-go
# 配置环境变量
# .zshrc
$ export PATH="$PATH:$(go env GOPATH)/bin"
```

3. 安装go-grpc包

```shell
$ go get -u google.golang.org/grpc
```






