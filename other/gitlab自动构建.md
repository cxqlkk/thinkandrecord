## 1. 安装gitlab-runner

1. 下载
 >  wget -O /usr/local/bin/gitlab-runner https://gitlab-ci-multi-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-ci-multi-runner-linux-amd64

2. 权限
> chmod +x /usr/local/bin/gitlab-runner 

3. 注册runner
> gitlab-runner register

(选择shell ,docker 暂时有问题)

4. 安装并启动服务
> gitlab-runner install --user=gitlab-runner --working-directory=/home/gitlab-runner
sudo gitlab-runner start


项目目录下
1. 放入 .gitlab-ci.yml


### 注意：
>1.  安装git   yum install git
> 2. 安装golang 
>> 1. 下载 安装包 https://dl.google.com/go/go1.10.3.linux-amd64.tar.gz
2. 配置path
 >> vi /etc/profile
   path=$PATH:/..
 export path
  >>  source /etc/profile
 >> go version
