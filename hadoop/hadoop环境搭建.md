### hadoop 单机环境搭建

1. 下载 hadoop 安装包
   可以到附近的镜像进行下载，镜像站点可以在下面的网址查到
   https://www.apache.org/dyn/closer.cgi/hadoop/common

2. 使用 wget 命令下载安装包,这里以 2.7.7 版本为例

```
wget https://mirrors.tuna.tsinghua.edu.cn/apache/hadoop/common/hadoop-2.7.7/hadoop-2.7.7.tar.gz
```

3. 使用 tar 命令解压安装包

```
tar -zxvf hadoop-2.7.7.tar.gz
```

4. 修改配置中`JAVA_HOME`

```
vim etc/hadoop/hadoop-env.sh
```

找到`JAVA_HOME`配置并修改

![](https://tva1.sinaimg.cn/large/007S8ZIlgy1ggpolwf9enj309g01ewef.jpg)

5. 修改 core-site.xml 配置及 hdfs-site.xml 配置
   etc/hadoop/core-site.xml:

```xml
<property>
  <name>fs.defaultFS</name>
  <value>hdfs://localhost:9000</value>
</property>
```

etc/hadoop/hdfs-site.xml:

```xml
<property>
  <name>dfs.replication</name>
  <value>1</value>
</property>
<property>
  <name>hadoop.tmp.dir</name>
  <value>/root/app/tmp</value>
</property>
```

6.启动 HDFS
第一次执行的时候一定要格式化文件系统，不要重复执行.执行命令

```
hdfs namenode -format
```

启动集群

```
sbin/start-dfs.sh
```

启动完毕后使用 jps 查看进程，如果看到下面的截图，说明启动成功了
![](https://tva1.sinaimg.cn/large/007S8ZIlgy1ggpr4b4x1fj306p01y74a.jpg)

7. 配置`HADOOP_HOME`
   配置完 HADOOP_HOME 后续就可以在任意文件夹下执行 hadoop 命令

```
vim /etc/profile
```

增加如下两行

```
HADOOP_HOME=hadoop解压路径
PATH=$PATH:$HADOOP_HOME/bin
```

最后再`source`一下配置文件

```
source /etc/profile
```
