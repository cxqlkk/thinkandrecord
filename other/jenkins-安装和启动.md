#   下载jenkins
wget -O ROOT.war http://mirrors.jenkins.io/war-stable/latest/jenkins.war

# 启动war
nohup java -jar jenkins.war --httpPort=9090


# 初始密码
/root/.jenkins/secrets/initialAdminPassword


