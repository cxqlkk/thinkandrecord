## elk 日志收集查看系统


### 1. 安装elastic
 1. wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.4.3.tar.gz
 2. 解压 运行 config jvm  和 ym 可以配置相关信息


https://blog.csdn.net/tanqian351/article/details/83827583

### 2. 安装kibana


 wget https://artifacts.elastic.co/downloads/kibana/kibana-6.4.2-linux-x86_64.tar.gz


步骤2：解压

tar -zxvf kibana-6.4.2-linux-x86_64.tar.gz

mv kibana-6.4.2-linux-x86_64 kibana-6.4.2

步骤3：修改配置文件中的url

vim kibana-6.4.2/config/kibana.yml
————————————————
版权声明：本文为CSDN博主「TByoung」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_19524879/java/article/details/83540840

### 3. logstash

wget https://artifacts.elastic.co/downloads/logstash/logstash-6.4.3.tar.gz