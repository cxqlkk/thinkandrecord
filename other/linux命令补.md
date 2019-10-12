##### 1. vi 文件内容替换

> 切换到命令行模式
>
> %s+源内容+替换后内容+
>
> 例： %s+你好+你坏+

##### 2.远程登陆和文件传输

> * ssh root@ip
> * scp /home/1.txt  root@ip:/home/ ( 如果是文件夹 scp -r)

##### 3. 重定向

> 每个linux 命令运行时会打开三个文件
>
> 标准输入文件（stdin) :文件描述符为0，unix程序 默认从 stdin读取数据
>
> 标准输出文件（stdout):文件描述符为1，unix程序默认向stdout 输出数据
>
> 标准错误文件（stderr):文件描述父为2，unix 会向stderr 输出错误数据

```
ls >1.txt 将输出重定向到1.txt
lp 2>1.txt 将错误信息重定向到1.txt
ls <1.txt
./mian > log.txt 2>&1 &
将标准输出重定向到 log.txt 同时将标准错误重定向到标准输出  并且程序 后台运行（&）
```

