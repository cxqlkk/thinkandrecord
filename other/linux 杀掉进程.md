### Linux 简便删除 进程

ps aux|grep reids |grep -v grep|awk '{print $2}'|xargs kill -9


kill命令没有接收到应有的参数。还有很多命令（比如最常见的mkdir、rm、cp等等等）都不会从标准输入读取内容，这时如果在管道符后加上xargs，再加上要执行的命令，那么前一个程序的标准输出就会作为后一个程序的参数，而不是标准输入了。