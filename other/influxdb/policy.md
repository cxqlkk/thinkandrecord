

SHOW RETENTION POLICIES ON db_metric(数据库)

 CREATE RETENTION POLICY "20_days" ON "mydb11" DURATION 20d REPLICATION 1



 只更新是否为默认策略，将策略20_days作为库db_metric默认策略

alter retention policy "20_days" on "db_metric" DEFAULT
(2) 只更新保存时间

alter retention policy "20_days" on "db_metric" duration 30d


DROP RETENTION POLICY <retention_policy_name> ON <database>