# Git 命令

mkdir test  
cd test  
touch a.md  


## alias 设置别名
git config --global alias.co checkout

git config --global alias.psm 'push -u origin master'

git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative" 格式化log日志

git config --global core.editor "vim" 设置Editor使用vim

git config --global color.ui true 开启Git输出着色

git config --global core.quotepath false 设置显示中文文件名，false为显示中文名

git config -l 查看自己的配置


### 初始化、查看状态

git init 初始化仓库

git status 查看状态


### 添加移除版本控制

git add file 添加文件进入git版本控制

git rm --cache file  移除版本控制，只是将已添加到版本控制的文件移出版本控制


### 删除文件

git rm file 工作目录中删除文件，直接删除文件，接 commit 提交删除

rm file 是 shell 的删除指令，在删除后需要 add 指令添加再  commit 提交


### 提交

git commit -m "info" 提交  -m 提交信息

git commit --amend -m "info"  紧跟上次 commit，修改上次 commit 时的提交信息


### 版本回退

git checkout file 未 add 的时候丢弃改动，抛弃当前本地所做所有改动，恢复到最后 add 的版本或最后 commit 的版本,不会移除 add 的版本

git reset file add 操作之后撤销 add，使用历史区的版本替换暂存区的版本，工作区的不变，可以重新 add  

git reset HEAD^/HEAD^^/HEAD~100 file 回退相应 file 已经 commit 的提交，reset 掉提交的记录中 file 发生的修改，但不修改本地工作区，可以从新提交。区别于库的回退，库回退会回退所有文件，这里的回退只是回退该文件内容

git reset --hard HEAD^/HEAD^^/HEAD~100 将整个代码库回退到相应的版本， HEAD 表示当前版本 HEAD^ 表示上一版本，会将当前工作区、暂存区中的所有代码恢复到指定的版本，并指定版本之后的 commit 记录全部清除，相当于恢复到指定版本时的状态


### 查看记录

git blame file 追溯一个指定文件修改历史记录

git log  查看所有产生的commit记录

git shortlog 根据提交者的名字分组显示提交 log

git reflog 查看所有产生的 commit 记录，包括 reset 时移除的，并且使用 reset --hard 指令也会将内容恢复到对应版本


## diff 查看改动
git diff 查看改动 红色代表删除的，绿色代表增加的，git diff 只能查看没有添加到缓存区的差异，就是没有git add的文件

git diff file 查看该文件有何改动

git diff v1.0 v1.1   比较两次提交之间的差异

git diff master develop 在两个分支之间比较 

git diff --staged   比较暂存区和版本库差异

git diff HEAD^/HEAD^^/HEAD~100   比较提交节点直接的差异


## checkout 切换分支或版本
git checkout develop 切换分支

git checkout v1.0  切换tag，切换到某次commit

git checkout ffddllllll  commit_id,每次commit的SHA1值

git checkout a.md  撤销没有添加到缓存区的改动，没有git add的变动


## stash 暂存
git stash 将没有commit的代码暂存，add了也沒关系,git status会看不到任何改动，将代码恢复到上次 commit 后时的状态，并将上次 commit 后发生的修改暂存

git stash list 查看暂存区的记录

git stash apply 将暂存的代码还原

git stash drop 将一条stash记录删除，后面跟可以跟 stash_id 参数来删除指定的某条记录，不跟参数就是删除最近的

git stash pop 跟 apply 功能一样，区别是 pop 不但会将代码还原，还自动删除该条 stash 记录，省去 drop 一次的操作

git stash clear 清空所有暂存区记录，drop只删除一条，后面跟可以跟stash_id参数来删除指定的某条记录，不跟参数就是删除最近的，clear是清空 


## github  

1. 配置ssh  ssh-keygen -t rsa 生成密钥 id_rsa id_rsa.pub 将id_rsa.pub配置到github

2. - 配置用户名 git config --global user.name ""
   - 配置邮箱   git config --global user.email ""
   - 可以再随便一个项目中执行以上代码擦除全局配置的个人信息
 
3. git remote add origin git@github.com:renxuelong/GitStudy.git
   将本地的代码添加一个远程仓库，origin 是这个远程仓库的名字，可以随便起
   一个项目可以由多个远程仓库，提交到不同的仓库就需要不用的仓库名

3. git push -u origin master 推送 本地 master 分支到远程仓库 origin 的 master 分支，加 -u 为将本地  master 分支和远程 master 分支关联起来，之后的 push 就不需要 -u 参数了

4. git pull origin master 将 origin 远程仓库 master 分支上的代码同步到本地

5. git pull --rebase 指令拉取最新修改，该指令作用为拉取本地代码后，将本地未提交的代码作用到最新版本中，避免多余的 mergy history 

6. git remote 查看当前项目有哪些远程仓库

7. git remote -v 查看当前项目所以远程仓库的详细信息

8. git remote rm origin 移除 origin 远程仓库

9. git push origin develop：develop2 将远程分支取名为develop2，不建议本地跟远程分支名不同，建议本地分支跟远程分支名要保持一致   

10. git push origin develop 将本地 develop 分支推送到远程 origin 仓库中

11. git push origin :develop 删除远程 origin 库中的 develop 分支  

12. git checkout develop origin 将远程分支迁到本地，测试无效  

13. git checkout -b develop origin 将远程分支迁到本地并切换到该分支 

14. git push origin v1.0 推送 Tag 到远程仓库 

15. git push origin --tags 推送本地所以 tag 到远程仓库

## brach 分支

git branch 查看本地分支  

git branch -r 查看远程分支

git branch -a 列举所有本地和远程分支

git brach develop 在当前分支基础上新建分支，分支 develop 跟当前分支内容一样  

git checkout develop 切换分支  

git checkout -b a 新建一个a分支，并且自动切换到a分支

git branch -d develop 删除本地分支，前提是a分支中的代码已经merge到了master分支，否则会删除失败  

git branch -D develop (强制删除)  

git push origin :develop 删除远程 origin 库中的 develop 分支  

git checkout develop origin/develop 将远程分支迁到本地，测试无效  

git checkout -b develop origin/develop 将远程分支迁到本地并切换到该分支 

git merge a  将 a 分支的代码合并到当前分支，可能发生冲突，这时会把冲突代码显示到代码中，开发者自己删除废弃代码，完成合并操作

git 分支存储原理： 不同于 SVN 每个分支都是备份一下整个库文件，git 不论是创建分支还是记录版本都不会创建整个文件或者分支的备份，而是通过创建一个指针指向不同的文件或分支，切换分支或者版本记录都只是改变指针指向的位置，git 实际是使用了很少的存储空间来记录一切


### tag 标签

tag 可以认为是一个快照，一个记录点，用于记录某个 commit 点或分支的历史快照，tag 通常打在 master 分支上，以保证代码的准确性

git tag v1.0 新建代码版本标签，默认记录在最后一次 commit 

git tag v1.0 commit_id 在 commit_id 对应的 commit 处新建 tag

git tag 查看版本标签

git tag -a v1.0 -m "tag message" 通过 -a 参数指定添加 tag 信息，-m 参数为 tag 的信息

git show tagname 查看指定 tag 的详细信息

git tag -d v1.0 删除指定 tag

git push origin :ref/tags/v1.0 删除本地 tag 后再推送到远程仓库删除远程仓库的 tag

git checkout v1.0 切换到某个标签

git push origin v1.0 推送 Tag 到远程仓库

git push origin --tags 推送本地所以 tag 到远程仓库


## merge & rebase
**merge 合并**

git checkout master 切换到 master 分支

git merge featureA 将 featureA 分支上的代码合并到 master 分支上

**rebase 合并**

git checkout master 切换到 master 分支

git rebase featureA 将 featureA 分支上的代码合并到 master 分支上
 
merge 和 rebase 的区别在于，merge 直接将 featureA 的代码放到另一空间

rebase 则是将两个分支上的代码先进行比较，按时间重新排序，然后放置，优点是合并后代码很有逻辑，缺点是不知道哪些代码来自哪个分支


## 冲突解决
**conflicts** 冲突

冲突的地方有=======分出上下两部分，上部分一个有HEAD的字样代表是我当前所在的分支的代码，下半部分是要合并到的分支的代码，比较后，删除了老旧代码，同时删除 <<< HEAD ========这些标记符号，再进行一次commit就可以了


## Git Flow
**git flow"**是一种比较成熟的分支管理流程  

- **master**：永远处于即将发布（production-ready）状态
- **develop**：最新的开发状态，develop 分支属于测试环境
- **feature**：开发新功能的分支，基于 develop ，完成后merge回develop，开发新功能时基于 develop 新建一个分支feature/A，开发完成后merge回develop分支，规定所有的功能分支都已 feature 为前缀
- **release**:准备要发布的版本，用来修复bug，基于develop，完成后merge回develop和master， develop分支属于测试环境，跟后端对接并且测试差不多时，这时候新建一个 release 分支，这时候 API、数据等都是正式环境，这个分支上做最后的测试，bug修改，测试ok后 merge 到 develop 和 master ，然后发布
- **hotfix**：修复master上的问题，等不及release版本就必须马上上线，基于master，完成后merge回master和develop。线上的紧急bug需要修改，这时候需要切换到master分支，在此基础上新建hotfix/B分支，修复完成后直接合并到 develop 和 master ，然后发布。

**master** --> **develop** --> **master**

**develop** --> **feature** --> **develop**

**master** --> **hotfix** --> **develop&master**

**master** --> **release** --> **develop&master**


## Git Flow 管理开发流程
**git flow init** 初始化 git-flow 功能，默认设置，完成后当前分支就变成了develop，然和开发都必须从develop开始  
**git flow feature start some_awesome_feature** 创建名为 some_awesome_feature 的分支  
**git flow feature publish some_awesome_feature** Publish一个feature（也就是push到远程） 
**git flow feature pull origin some_awesome_Feature** 获取Publish的feature  
**git flow feature finish some_awesome_feature** 该命令会把 feature/some_awesome_feature 合并到 develop 分支，然后删除feature分支，必须将改变commit后才可以使用该命令，该命令也会将publish到远程的feature删除  

 
**git flow release start v0.1.0** 需要发布新版本时，基于develop创建一个发布分支，然后升级版本号，修改bug。  
**git flow release publish v0.1.0** Publish一个release，但是并没有pull的方法  
**git flow release finish v0.1.0** 在完成（finish）一个发布版本时，它会把所做的修改合并到 master 分支，同时合并会 develop 分支。  
**git push --tags** finish一个发布版本后，应该git push版本号，不用git tag，git push --tags 会将当前release的版本号作为tag提交


**git flow hotfix start 0.0.1** 开始一个 Hotfix  **git flow hotfix finish 0.1.1** 发布一个 Hotfix  
