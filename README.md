<<<<<<< HEAD
=======
# GitStudy
## git的学习记录
mkdir test
cd test
touch a.md

git init 初始化仓库

git status 查看状态

git add file

git rm --cache file  移除缓存

git commit -m "info" 提交  -m 提交信息

git log  查看所有产生的commit记录

git branch 查看当前分支情况

git branch a 新建一个名字叫 a 的分支,分支 a 跟分支 master 内容一样

git checkout a 切换分支

git checkout -b a 新建一个a分支，并且自动切换到a分支

git merge a  将a分支的代码合并过来（需要先checkout master切换到主分支）

git branch -d b 删除分支b，前提是a分支中的代码已经merge到了master分支，否则会删除失败

git branch -D b 强制删除b分支

git tag v1.0 新建代码版本标签

git tag 查看版本标签

git checkout v1.0 切换到某个标签

git remote -v 查看当前项目有哪些远程仓库

## github  

1. 配置ssh  ssh-keygen -t rsa 生成密钥 id_rsa id_rsa.pub 将id_rsa.pub配置到github

2. 配置用户名 git config --global user.name ""
   配置邮箱   git config --global user.email ""
3. git remote add origin git@github.com:renxuelong/GitStudy.git
   将本地的代码添加一个远程仓库，origin是这个远程仓库的名字，可以随便起
   一个项目可以由多个远程仓库，提交到不同的仓库就需要不用的仓库名

3. git push origin master 推到远程仓库origin的master分支

4. git pull origin master 将origin远程仓库master分支上的代码同步到本地

