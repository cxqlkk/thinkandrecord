确认你的电脑是否安装homebrew，打开电脑终端 输入：

/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

确认homebrew是否安装成功，在终端输入：

brew -v

image.png
安装nginx，在终端输入：

brew install nginx
检查nginx是否安装成功，在终端输入：

nginx -v

image.png
启动nginx，在终端输入：

brew services start nginx
检查nginx是否启动成功，在浏览器输入：

localhost:8080

image.png
nginx常用命令小结


//检查是否安装nginx及对应的目录
find /|grep nginx.conf
//启动Nginx
service nginx start
//重启nginx
service nginx restart

