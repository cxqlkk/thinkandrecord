https://dba.stackexchange.com/questions/41050/is-it-safe-to-delete-mysql-bin-files?spm=a2c6h.13066369.0.0.43813048W7v9ib



binlog日志随着时间的增长会占用很大的磁盘资源。

有时候我们需要手动清理。

查看指定删除日志

mysql >show binary logs; 查看多少binlog日志，占用多少空间。

mysql> PURGE MASTER LOGS TO 'mysql-bin.000007'; 删除mysql-bin.000007以前所有binlog，这样删除可以保证*.index信息与binlog文件同步。

手动清理

mysql>PURGE MASTER LOGS BEFORE DATE_SUB(CURRENT_DATE, INTERVAL 5 DAY); 手动删除5天前的binlog日志

自动设置清理

mysql> set global expire_logs_days = 5; 把binlog的过期时间设置为5天; 

mysql> flush logs; 刷一下log使上面的设置生效，否则不生效。

为保证在MYSQL重启后仍然有效，在my.cnf中也加入此参数设置

expire_logs_days = 5
————————————————
版权声明：本文为CSDN博主「一眼隔世」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/fuzhongfaya/java/article/details/80989191