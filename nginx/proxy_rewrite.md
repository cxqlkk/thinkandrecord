https://www.cnblogs.com/luxianghao/p/6807081.html


rewrite
syntax: rewrite regex replacement [flag]
Default: —
Context: server, location, if
如果正则表达式（regex）匹配到了请求的URI（request URI），这个URI会被后面的replacement替换
rewrite的定向会根据他们在配置文件中出现的顺序依次执行
通过使用flag可以终止定向后进一步的处理
如果replacement以“http://”, “https://”, or “$scheme”开头，处理将会终止，请求结果会以重定向的形式返回给客户端（client）
如果replacement字符串里有新的request参数，那么之前的参数会附加到其后面，如果要避免这种情况，那就在replacement字符串后面加上“？”，eg：
 rewrite ^/users/(.*)$ /show?user=$1? last;=
如果正则表达式（regex）里包含“}” or “;”字符，需要用单引号或者双引号把正则表达式引起来
可选的flag参数如下：
last
结束当前的请求处理，用替换后的URI重新匹配location；
可理解为重写（rewrite）后，发起了一个新请求，进入server模块，匹配location；
如果重新匹配循环的次数超过10次，nginx会返回500错误；
返回302 http状态码 ；
浏览器地址栏显示重地向后的url
break
结束当前的请求处理，使用当前资源，不在执行location里余下的语句；
返回302 http状态码 ；
浏览器地址栏显示重地向后的url
 redirect
临时跳转，返回302 http状态码；
浏览器地址栏显示重地向后的url
permanent
永久跳转，返回301 http状态码；
浏览器地址栏显示重定向后的url
 

proxy_pass
Syntax:    proxy_pass URL;
Default:    —
Context:    location, if in location, limit_except
不影响浏览器地址栏的url
设置被代理server的协议和地址，URI可选（可以有，也可以没有）
协议可以为http或https
地址可以为域名或者IP，端口可选；eg：
 proxy_pass http://localhost:8000/uri/;
 如果一个域名可以解析到多个地址，那么这些地址会被轮流使用，此外，还可以把一个地址指定为 server group（如：nginx的upstream）, eg:
复制代码
upstream backend {
    server backend1.example.com       weight=5;
    server backend2.example.com:8080;
    server unix:/tmp/backend3;
 
    server backup1.example.com:8080   backup;
    server backup2.example.com:8080   backup;
}
 
server {
    location / {
        proxy_pass http://backend;
    }
}
复制代码
server name， port， URI支持变量的形式，eg：
proxy_pass http://$host$uri;
这种情况下，nginx会在server groups（upstream后端server）里搜索server name，如果没有找到，会用dns解析，
请求的URI会按照下面的规则传给后端服务，下面结合具体的例子来说明URI的传递规则，假设nginx中server部分的配置如下：

复制代码
   server {
        listen       80;
        server_name example.com;
        proxy_read_timeout 120;
        proxy_send_timeout 120;
        include /etc/nginx/fastcgi_params;

        access_log  /var/log/nginx/access.log  main;
        error_log   /var/log/nginx/error.log;

        location / {
           ...
        }

}
复制代码
 

如果proxy_pass的URL定向里包括URI，那么请求中匹配到location中URI的部分会被proxy_pass后面URL中的URI替换，eg：
location /name/ {
    proxy_pass http://127.0.0.1/remote/;
}
请求http://example.com/name/test.html 会被代理到http://127.0.0.1/remote/test.html
如果proxy_pass的URL定向里不包括URI，那么请求中的URI会保持原样传送给后端server，eg：
location /name/ {
    proxy_pass http://127.0.0.1;
}

请求http://example/name/test.html 会被代理到http://127.0.0.1/name/test.html
 一些情况下，不能确定替换的URI

location里是正则表达式，这种情况下，proxy_pass里最好不要有URI
在proxy_pass前面用了rewrite，如下，这种情况下，proxy_pass是无效的，eg：
location /name/ {
    rewrite    /name/([^/]+) /users?name=$1 break;
    proxy_pass http://127.0.0.1;
}
xx