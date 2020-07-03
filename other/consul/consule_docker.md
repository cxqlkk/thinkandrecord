https://blog.csdn.net/wzy_168/article/details/102498206

docker run  --net = "host"   --name 244server -e CONSUL_BIND_INTERFACE='em4' -d  -p 8300:8300 -p 8301:8301 -p 8302:8302 -p 8600:8600 204ef3cdcad6 agent -server -bootstrap-expect 2  -node=xx(唯一) -bind=2.94.216.244  -client=0.0.0.0


//配置详解
https://www.jianshu.com/p/d8f273dda86c


consul join
consul members
consul reload