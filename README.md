# GitStudy
## git的学习记录
mkdir test
cd test
touch a.md

git init 初始化仓库

git status 查看状态

git add file 添加文件进入git版本控制

git rm --cache file  移除版本控制

git rm file 工作目录中删除文件

git checkout file 未add的时候丢弃改动

git reset file add之后撤销add  
git reset HEAD file add之后撤销add

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

git config --global core.quotepath false 设置显示中文文件名，false为显示中文名

git config -l 查看自己的配置


## diff
git diff 查看改动 红色代表删除的，绿色代表增加的，git diff 只能查看没有添加到缓存区的差异，就是没有git add的文件

git diff v1.0 v1.1   比较两次提交之间的差异

git diff master develop 在两个分支之间比较 

git diff --staged   比较暂存区和版本库差异

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

## merge & rebase
**merge 合并**

git checkout master

git merge featureA 将 featureA 分支上的代码合并到master分支上

**rebase 合并**

git checkout master
git rebase featureA 将featureA分支上的代码合并到master分支上
 
merge 和 rebase 的区别在于，merge直接将featureA的代码放到另一空间

rebase则是将两个分支上的代码先进行比较，按时间重新排序，然后放置，优点是合并后代码很有逻辑，缺点是不知道哪些代码来自哪个分支

## 冲突解决
**conflicts** 冲突

冲突的地方有=======分出上下两部分，上部分一个有HEAD的字样代表是我当前所在的分支的代码，下半部分是要合并到的分支的代码，比较后，删除了老旧代码，同时删除 <<< HEAD ========这些标记符号，再进行一次commit就可以了

## brach 分支

git brach develop 在当前分支基础上新建分支，内容同当前分支一样  
git checkout develop 切换分支  
git push origin develop：develop2 将远程分支取名为develop2，不建议本地跟远程分支名不同，建议本地分支跟远程分支名要保持一致  
git branch 查看本地分支  
git branch ir 查看远程分支
git branch -d develop 删除本地分支  
git branch -D develop (强制删除)  
git push origin :develop 删除远程分支  
git checkout develop origin/develop 将远程分支迁到本地，测试无效  
git checkout -b develop origin/develop 将远程分支迁到本地并切换到该分支  

## Git Flow
**git flow"**是一种比较成熟的分支管理流程  

- **master**：永远处于即将发布（production-ready）状态
- **develop**：最新的开发状态，develop 分支属于测试环境
- **feature**：开发新功能的分支，基于 develop ，完成后merge回develop，开发新功能时基于 develop 新建一个分支feature/A，开发完成后merge回develop分支，规定所有的功能分支都已 feature 为前缀
- **release**:准备要发布的版本，用来修复bug，基于develop，完成后merge回develop和master， develop分支属于测试环境，跟后端对接并且测试差不多时，这时候新建一个 release 分支，这时候 API、数据等都是正式环境，这个分支上做最后的测试，bug修改，测试ok后 merge 到 develop 和 master ，然后发布
- **hotfix**：修复master上的问题，等不及release版本就必须马上上线，基于master，完成后merge回master和develop。线上的紧急bug需要修改，这时候需要切换到master分支，在此基础上新建hotfix/B分支，修复完成后直接合并到 develop 和 master ，然后发布。

**master** --> **develop** --> **master**

**develop** --> **feature** --> **develop**

**master** --> **hotfix** --> **develop&master**

**master** --> **release** --> **develop&master**


## Git Flow 管理开发流程
**git flow init** 初始化 git-flow 功能，默认设置，完成后当前分支就变成了develop，然和开发都必须从develop开始  
**git flow feature start some_awesome_feature** 创建名为 some_awesome_feature 的分支  
**git flow feature publish some_awesome_feature** Publish一个feature（也就是push到远程） 
**git flow feature pull origin some_awesome_Feature** 获取Publish的feature  
**git flow feature finish some_awesome_feature** 该命令会把 feature/some_awesome_feature 合并到 develop 分支，然后删除feature分支，必须将改变commit后才可以使用该命令，该命令也会将publish到远程的feature删除  

 
**git flow release start v0.1.0** 需要发布新版本时，基于develop创建一个发布分支，然后升级版本号，修改bug。  
**git flow release publish v0.1.0** Publish一个release，但是并没有pull的方法  
**git flow release finish v0.1.0** 在完成（finish）一个发布版本时，它会把所做的修改合并到 master 分支，同时合并会 develop 分支。  
**git push --tags** finish一个发布版本后，应该git push版本号，不用git tag，git push --tags 会将当前release的版本号作为tag提交