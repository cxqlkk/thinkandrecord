#### docker 容器部署mysql 和镜像挂载

> 参考[Docker安装MySql-挂载外部数据和配置](https://www.cnblogs.com/0oliumino0/p/10538207.html)

> 使用docker 镜像来构建mysql 数据库环境是很方便的，但是容器删除所有数据就和容器一起丢失，所以还需要将宿主机的文件夹来挂载在容器来存储数据（data 和配置文件）

###### 1 .下载镜像并启动容器找到配置文件

> docker pull  docker.io/javiersolis/mysql5.7
>
> docker run -it 镜像id /bin/bash
>
> * 找到 配置文件 (/etc/mysql/mysql.conf.d/mysqld.cnf)
> * 打开配置文件（并复制一份到宿主机） 找到 数据存储目录 （/var/lib/mysql)

###### 2. 在宿主机创建配置 目录 和文件用来挂载

> cd opt
>
> mkdir mysql
>
> cd mysql && makedir data && makedir config
>
> cd config touch mysqld.cnf(里面的内容指明了数据存储目录，方便挂载）
>
> ```mysql
> [mysqld]
> pid-file        = /var/run/mysqld/mysqld.pid
> socket          = /var/run/mysqld/mysqld.sock
> datadir         = /var/lib/mysql
> lower_case_table_names=1
> #log-error      = /var/log/mysql/error.log
> # By default we only accept connections from localhost
> #bind-address   = 127.0.0.1
> # Disabling symbolic-links is recommended to prevent assorted security risks
> symbolic-links=0
> ```

###### 3.重新创建容器并挂载文件

> ```docker
> ocker run --name mysql5.7 --restart always --privileged=true -p 3306:3306 -v /opt/mysql/config/mysqld.cnf:/etc/mysql/mysql.conf.d/mysqld.cnf -v /opt/mysql/data:/var/lib/mysql -e MYSQL_USER="fengwei" -e MYSQL_PASSWORD="pwd123" -e MYSQL_ROOT_PASSWORD="rootpwd123" -d 镜像id
> ```

###### 4. 权限问题和日期零值问题

`宿主机连接容器mysql,会报出权限问题`

```mysql
GRANT ALL PRIVILEGES ON *.* TO 'root'@'192.168.1.3' IDENTIFIED BY   'mypassword' WITH GRANT OPTION;   

  FLUSH   PRIVILEGES;  
```

`由于版本问题mysql 对日期零值会报错`

```mysql
set @@global.sql_mode='STRICT_TRANS_TABLES,NO_ENGINE_SUBSTITUTION';
set @@session.sql_mode='STRICT_TRANS_TABLES,NO_ENGINE_SUBSTITUTION';
```

`修改密码`

```mysql
alter user 'root'@'localhost' identified by '123';
flush privileges;
```

