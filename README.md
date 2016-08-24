# GitStudy
## git的学习记录
mkdir test
cd test
touch a.md

git init 初始化仓库

git status 查看状态

git add file 添加文件

git rm file 移除文件

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

git remote rm origin 移除远程仓库

## github  

1. 配置ssh  ssh-keygen -t rsa 生成密钥 id_rsa id_rsa.pub 将id_rsa.pub配置到github

2. - 配置用户名 git config --global user.name ""
   - 配置邮箱   git config --global user.email ""
   - 可以再随便一个项目中执行以上代码擦除全局配置的个人信息
3. git remote add origin git@github.com:renxuelong/GitStudy.git
   将本地的代码添加一个远程仓库，origin是这个远程仓库的名字，可以随便起
   一个项目可以由多个远程仓库，提交到不同的仓库就需要不用的仓库名

3. git push origin master 推到远程仓库origin的master分支

4. git pull origin master 将origin远程仓库master分支上的代码同步到本地

## alias 设置别名
git config --global alias.co checkout

git config --global alias.psm 'push -u origin master'

git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative" 格式化log日志

git config --global core.editor "vim" 设置Editor使用vim

git config --global color.ui true 开启Git输出着色

git config --global core.quotepath false 设置显示中文文件名

git config -l 查看自己的配置


## diff
git diff 查看改动 红色代表删除的，绿色代表增加的，git diff 只能查看没有添加到缓存区的差异，就是没有git add的文件

git diff <$id1> <$id2> 比较两次提交之间的差异


## checkout
git checkout develop 切换分支

git checkout v1.0  切换tag，切换到某次commit

git checkout ffddllllll  commit_id,每次commit的SHA1值


git checkout a.md  撤销没有添加到缓存区的改动，没有git add的变动

## stash
git stash 将没有commit的代码暂存，add了也沒关系,git status会看不到任何改动

git stash list 查看暂存区的记录

git stash apply 将暂存的代码还原

git stash drop 将最近的一条stash记录删除

git stash pop 跟 apply 功能一样，区别是 pop 不但会将代码还原，还自动删除该条 stash 记录，省去 drop 一次的操作

git stash clear 清空所有暂存区记录，drop只删除一条，后面跟可以跟stash_id参数来删除指定的某条记录，不跟参数就是删除最近的，clear是清空




