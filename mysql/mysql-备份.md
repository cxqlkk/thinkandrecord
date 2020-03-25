### mysql 备份
数据库是web应用系统的心脏（我乱说的）, 作用是很大的,为了数据的安全，我们必须备份数据库
数据库的备份方式有两种 
1. 增量备份，即每次只将对主数据库的 新增修改删除操作，同步到备份数据库
2. 全量备份，将数据库文件定期全部导出

增量备份，更灵活，更多的是用在读写分离上，但是如果是对主数据的恶意操作，或误操作 将会同步到从库中
全量备份，需要锁库，占用磁盘空间，但是可以避免 恶意操作

####一、增量备份（主从同步）
增量备份，主要是修改主从库的配置文件
`特别说明`：GTID 方式 不需要知道偏移量（简单来说更好操作）
##### 一、 增量备份
1.1 修改配置文件
`主库配置文件 `
```
[mysqld]
#GTID:
server_id=1 #服务器id
gtid_mode=on #开启gtid模式
log_slave_updates ## 表示即可以当从也可以当主
enforce_gtid_consistency=on #强制gtid一致性，开启后对于特定create table不被支持

#binlog
#log_bin=master-binlog
log_bin=mysql-bin
#log-bin=/data/mysql/mysql-bin.log    //binlog日志文件,(文件名如果是绝对路径,必须指定索引文件)
#log_bin_index =    /var/lib/mysql/mysql-bin.index     //是binlog文件的索引文件，这个文件管理了所有的binlog文件的目录
log-slave-updates=1 
binlog_format=row #binlog日志格式，强烈建议，其他格式可能造成数据不一致
expire_logs_days=7            //binlog过期清理时间



#relay logskip_slave_start=1

```
`从库`
只需要server-id 不同


1.2 创建用户并授权
master 数据库   
```
create user repl_user IDENTIFIED BY 'repl_passwd';

grant replication slave on *.* to 'repl_user'@'2.82.74.199' identified by 'repl_passwd';

flush privileges;

show master status;

```

从数据库

```
change master to master_host='10.0.0.132', master_user='repl_user',master_password='repl_passwd',master_port=3306,master_auto_position=1;

start slave;
show slave status;
```

##### 二、全量备份

编写脚本
db_user="xxx"
db_passwd="xxx"
db_name="xxx"
backup_dir="/data/backmysql
" log_dir="/data/logs" 
time="$(date +"%Y%m%d%H%M%S")" 
start=`date +%Y-%m-%d_%H:%M:%S` 
echo -e "开始执行备份：$start" >> $log_dir/auto_backup.log mysqldump -u$db_user -p$db_passwd $db_name > "$backup_dir/$db_name"_"$time.sql" end=`date +%Y-%m-%d_%H:%M:%S` echo -e "结束执行备份：$end\n" >> $log_dir/auto_backup.log find $backup_dir -mtime +5 -name "*.*" -exec rm -f {} \;```

```
添加执行权限
`chmod +x backmysql.sh `//

编辑定时任务
crontab -e

0 3 * * * sh /data/backmysql.sh

重启 cron
service cron restart




