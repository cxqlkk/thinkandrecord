Git 全局设置

git config --global user.name "陈向前"
git config --global user.email "chenxiangqian@codenai.com"

创建一个新仓库

git clone ssh://git@team.dmanywhere.cn:7022/chenxiangqian/yjgl.git
cd yjgl
touch README.md
git add README.md
git commit -m "add README"
git push -u origin master

推送现有文件夹

cd existing_folder
git init
git remote add origin ssh://git@team.dmanywhere.cn:7022/chenxiangqian/yjgl.git
git add .
git commit -m "Initial commit"
git push -u origin master

推送现有的 Git 仓库

cd existing_repo
git remote rename origin old-origin
git remote add origin ssh://git@team.dmanywhere.cn:7022/chenxiangqian/yjgl.git
git push -u origin --all
git push -u origin --tags