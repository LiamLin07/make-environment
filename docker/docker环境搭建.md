### Docker 环境构建

1. 使用`yum`安装 Docker

```shell
yum -y install docker
```

2.配置阿里云镜像
执行如下命令：

```shell
systemctl status docker
```

添加如下配置并保存
![](https://github.com/LiamLin07/make-environment/img/linux/docker_aliyun.png)

3. 启动 docker

```shell
systemctl start docker
```

4. 查看 docker 状态
   如果现实截图中的`active (running)`，则说明 docker 启动成功

```shell
systemctl status docker
```

![](https://github.com/LiamLin07/make-environment/img/linux/docker_info.png)

5.查看 docker 镜像配置状态
输入`docker info`，确认阿里云加速镜像是否配置成功
![](https://github.com/LiamLin07/make-environment/img/linux/docker_status.png)
