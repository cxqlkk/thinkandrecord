重要技能学得篇-dlv 调试 web 程序

> dlv 用了很久，虽然用的很浅，但确实不知道怎么调试web

`step`

1. go build main.go 
2. ./main
3. （新控制台） ps -ef|grep main 找到 ./main 进程 pid
4. dlv attach pid
5. b /路径/main.go(此处是源文件名）：333（行数）
6. 浏览器或者其他请求服务就可进入断点

> ps: 需要  go build  （go run ，打断点容易找不到）