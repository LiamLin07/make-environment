### docker 快速安装 mysql

#### 前置条件

1.安装好 docker,具体安装步骤见[my link](./docker安装mysql.md)

#### 安装步骤

1.拉镜像

```shell
docker pull mysql:5.7
```

2. 添加 mysql 配置

```shell
vim ~/mysql/conf/mysql.cnf
```

输入如下配置:

```
[mysqld]
port = 3306
socket = /tmp/mysql.sock
skip-external-locking
#避免 MySQL 的外部锁定，减少出错几率增强稳定性。

key_buffer_size = 16M
#指定用于索引的缓冲区大小，增加它可得到更好的索引处理性能。16M适用于 512MB内存，对于内存在4GB左右的服务器该参数可设置为256M，依此类推即可。注意：该参数值设置的过大反而会是服务器整体效率降低！

max_allowed_packet = 1M
#MySQL 根据此配置会限制 server 接受的数据包大小。

table_open_cache = 64
#指定表高速缓存的大小。每当MySQL访问一个表时，如果在表缓冲区中还有空间，该表就被打开并放入其中，这样可以更快地访问表内容。注意，不能盲目地把#table_open_cache设置成很大的值。如果设置得太高，可能会造成文件描述符不足，从而造成性能不稳定或者连接失败。
#64 适用于 512MB 内存，1GB 内存则可以设置成 128，依此类推即可。

sort_buffer_size = 512K
#查询排序时所能使用的缓冲区大小。注意：该参数对应的分配内存是每连接独占，如果有100个连接，那么实际分配的总共排序缓冲区大小为100 × 512K ＝ 50MB。
#512K 适用于 512MB 内存，1GB 内存则可以设置成 1M，依此类推即可。

net_buffer_length = 8K
#初始化server 接受的数据包大小，当需要的时候再由 max_allowed_packet 控制增长的大小。注意：该参数值设置的范围只能为1 – 1024K。

read_buffer_size = 256K
#读查询操作所能使用的缓冲区大小。和 sort_buffer_size 一样，该参数对应的分配内存也是每连接独享。
#256K 适用于 512MB 内存，1GB 内存则可以设置成 512K，依此类推即可。

read_rnd_buffer_size = 512K
#查询操作多表所能使用的缓冲区大小。设置较大的值可以有效提升 ORDER BY 的性能。和 sort_buffer_size 一样，该参数对应的分配内存也是每连接独享。
#512K适用于 512MB 内存，1GB 内存则可以设置成 1M，依此类推即可。

myisam_sort_buffer_size = 8M
#MyISAM 排序所能使用的缓冲区大小。
#8M 适用于 512MB 内存，1GB 内存则可以设置成 16M，依此类推即可。

max_connections = 256
#指定MySQL允许的最大连接进程数。如果在访问时经常出现 Too Many Connections 的错误提示，则需要增大该参数值。
#注意：该参数默认值为 151，最大可以设置为 100000
#这里建议设置成内存的一半，比如 512MB 内存就设置成 256，依此类推。
```

3. 启动 mysql

```shell
docker run --name mysql57 \
-e MYSQL_ROOT_PASSWORD=123456 \
-p 3306:3306 \
-v ~/app/mysql/conf/mysql.cnf:/etc/mysql/mysql.conf.d/mysql.cnf \
-d mysql:5.7
```

4. 进入 mysql
   在命令行执行`mysql -u root -p`命令，输入密码后进入 mysql

5. 修改用户权限

- 修改 root 用户密码
  update user set authentication_string=password('123') where user='userName' and host='1.0.0.0';
- 授权 root 用户所有所有 ip 都能登录
  `grant all on *.* to 'root'@'%';`

- Mysql 8.0 中的用户授权
  Mysql8.0 中不允许用户使用 grant 命令创建用户，只能先创建再授权
  `CREATE USER 'user1'@'%' IDENTIFIED BY '123456';`
  `grant all on *.* to 'root'@'%';`

6. 修改密码校验规则(可选)

- 查看密码校验规则

```
  SHOW VARIABLES LIKE 'validate_password%'
```

![](https://tva1.sinaimg.cn/large/007S8ZIlgy1ggne2j48o6j309k05cgm9.jpg)

- 修改需要改的规则

```
SET GLOBAL validate_password.length=3;
```
