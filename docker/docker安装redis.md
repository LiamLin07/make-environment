### docker 快速安装 mysql

#### 前置条件

1.安装好 docker,具体安装步骤见[my link](./docker安装mysql.md)

#### 安装步骤

1.拉镜像
这里安装的是 redis4.0 版本，如果要安装其他版本只需要修改`:`后的版本号

```shell
docker pull redis:4.0
```

2.启动 redis

```shell
docker run -d -p 6379:6379 --name myredis redis:4.0
```
