### 1.安装jenkins(安装插件)
### 2.（服务器安装git)
### 3. 配置
>  1. Manage Jenkins
>  2. Configure System
>  3. 


1.gitlab webhook 403问题，一般描述为Error 403 anonymous is missing the Job/Build Permission

解决方法：

安装插件：gitlab/gitlab hook/Build Authorization Token Root Plugin
系统管理-->configure global security -->去掉勾选  防止跨站点请求伪造（可能）
系统管理-->系统设置-->去掉 Enable authentication for '/project' end-point