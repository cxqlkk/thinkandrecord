1. 版本为elasticsearch-6.4.3
2. 修改 config/jvm.options
   > -Xms556m
    > -Xmx556m
3. 修改 elasticsearch.yml
   增加 >
   ```
   network.host: 0.0.0.0
    http.port: 9200
    http.cors.enabled: true
    http.cors.allow-origin: "*"
    http.publish_host: 0.0.0.0
    ```

4. 创建新用户 

 > user add elsearch

5. 赋予权限
   > chmod -R 777 elasticsearch-6.4.3 

6. 切换 用户
    > su elsearch

7. 错误
    > [1]: max file descriptors [65535] for elasticsearch process is too low, increase to at least [65536]

    ```
        su root
        vi  /etc/security/limits.conf
          soft    nofile      65536
          hard    nofile     65536
    ```

    > [2]: max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]
    ```
        vi /etc/sysctl.conf 
        vm.max_map_count = 262144


        sysctl -p

    ```
    https://www.cnblogs.com/zhi-leaf/p/8484337.html