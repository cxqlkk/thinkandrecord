# docker 批量删除 退出的容器
docker rm `docker ps -a|grep Exited|awk '{print $1}'`