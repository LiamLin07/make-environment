### hive 单机版环境搭建

#### 前置条件

1. 准备 java 环境

- hive1.2 版本需要 jdk1.7 的环境以上,强烈推荐 1.8

2. 准备 hadoop 环境

- Hadoop 2.X,Hive 2.0.0 及以上版本不再支持 Hadoop1.X

### 开始搭建

1. 下载 hadoop 安装包
   可以到附近的镜像进行下载，镜像站点可以在下面的网址查到
   https://mirrors.tuna.tsinghua.edu.cn/apache/hive/

2. 解压安装包

```shell
  tar -xzvf hive-x.y.z.tar.gz
```

3. 添加 Hive 环境变量

```shell
  cd hive-x.y.z
  export HIVE_HOME={{pwd}}
```

添加环境变量

```shell
export PATH=$HIVE_HOME/bin:$PATH
```

4. 修改 hive-env.sh 及 hive-site.xml 配置文件
   进入 conf 文件夹

   ```shell
   cd conf
   ```

   配置 HADOOP_HOME
   ![](https://tva1.sinaimg.cn/large/007S8ZIlgy1ggq2oma624j30cv01bjrg.jpg)

   修改 hive-site.xml，如果 hive-site.xml 不存在可以拷贝 hive-default.xml。
   执行命令

   ```shell
   cp hive-default.xml hive-site.xml
   ```

   配置 mysql 作为数据源，需要修改四个配置`javax.jdo.option.ConnectionURL`,`javax.jdo.option.ConnectionDriverName`,`javax.jdo.option.ConnectionUserName`以及`javax.jdo.option.ConnectionPassword`
   修改的配置如下
   ![](https://tva1.sinaimg.cn/large/007S8ZIlgy1ggq2zv59vtj30vg0e7jtv.jpg)

5. 拷贝 MySQL 驱动包到\$HIVE_HOME/lib
   ![](https://tva1.sinaimg.cn/large/007S8ZIlgy1ggq33wbdw4j30z701mmxh.jpg)
