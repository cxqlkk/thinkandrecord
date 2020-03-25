#   下载jenkins
wget -O ROOT.war http://mirrors.jenkins.io/war-stable/latest/jenkins.war

# 启动war
java -jar jenkins.war --httpPort=9090
