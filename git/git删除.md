### git 删除

在实际操作中，有些文件（日志，或者其他无用的文件）需要删除
或者 有些文件本地需要，但是版本库不需要（不希望被版本库追踪，ru .gitignore 里的文件）


#### git rm

git rm  =rm file +git add 
即 删除本地文件，同时提交删除的步骤同步到git仓库

#### git rm --cached

将某个文件移除版本库追踪
比如有个傻蛋，把.idea 文件加提交了，每次pull 都会冲突
那么 我设置.gitignore /.idea
但是，每次提交了，仍然是冲突，
于是 git rm --cached .idea
移除版本库




