## 安装
##### Linux安装
* 产看是否安装
``` 
$ git
The program 'git' is currently not installed. You can install it by typing:
sudo apt-get install git
```
* Detbian或Ubuntu安装
``` 
$ sudo apt-get install git
```
* 其它版本自行官网下载，解压安装
##### Mac OSX安装
* 在XCode里面安装，菜单preferences->downloads->command line tools->install.
##### Windows安装
* https://git-scm.com/downloads
* 安装后打开Git Bash
* 设置用户面和邮箱
```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```
## 创建版本库 (以下操作都是在创建版本库中命令操作)
* 创建空目录
```
$ mkdir directory's name (创建版本目录)
$ cd directory's name （跳转到创建的版本库目录中）
$ pwd （显示当前目录）
```
* 初始化（使得目录变成git可以管理的仓库）
```
$ git init
Initialized empty Git repository in directory
```
* 添加管理文件

1. 使用notepad++ 写一个readme.txt文件，版本库中
2. 命令添加readme.txt
```
$ git add readme.txt
```
3. 告诉git把文件提交到仓库中
```
$git commit -m "wrote a readme file" (后面是文件说明)
[master (root-commit) cb926e7] wrote a readme file
1 file changed, 2 insertions(+)
create mode 100644 readme.txt
```
4. 提交多个文件
```
$ git add file1.txt
$ git add file2.txt file3.txt
$ git commit -m "add 3 files"
```
## 版本退回
* 查看仓库状态(修改readme.txt之后)
```
$ git status
on branch master
Changes not staged for commit:
    (use "git and <file>..." to update what will be comitted)
    (use "git checkout --<file>..." to discard changes in working directory)
    modified: readme.txt
no changes added to commit (use "git add" and/or "git commit -a")
```
* 查看修改和修改之前的不同
 ```
 $ git diff
 diff --git a/readme.txt b/readme.txt
index d8036c1..013b5bc 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,2 +1,2 @@
-Git is a version control system.
+Git is a distributed version control system.
 Git is free software.
\ No newline at end of file
 ```
 * 再次提交修改后的readme.txt
 ```
 $ git add readme.txt
 ```
 * 查看添加后的状态
 ```
 $ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   readme.txt
 ```
 * 提交修改后的readme.txt
```
$ git commit -m "distributed"
[master 08b6528] distributed
1 file changed, 1 insertion(+), 1 deletion(-)
```
* 产看提交后的状态
```
$ git status
on branch master
nothing to commit, working tree clean
```
* 产看修改日志
```
$ git log (产看所有日志)
commit d709937518037765a9b0f3bf96ce96e78e6878da (HEAD -> master)
Author: ICEMARK <1541914268@qq.com>
Date:   Tue Mar 13 16:44:34 2018 +0800

    append GPL

commit 08b6528020aa1f4684f62ebc1d7e06756e06e06f
Author: ICEMARK <1541914268@qq.com>
Date:   Tue Mar 13 16:28:34 2018 +0800

    distributed

commit a9b4054ea061556a189fe38e008aed15be76b0f3
Author: ICEMARK <1541914268@qq.com>
Date:   Tue Mar 13 10:43:48 2018 +0800

    wrote a readme file
$ git log --pretty=oneline(查看少量重要日志)
d709937518037765a9b0f3bf96ce96e78e6878da （==版本号==）(HEAD -> master) （表示当前版本） append GPL
08b6528020aa1f4684f62ebc1d7e06756e06e06f distributed
a9b4054ea061556a189fe38e008aed15be76b0f3 wrote a readme file
```
* 退回指定版本
```
git reset --hard head^ (上一版本用 head^,上上一版本用head^^, 如果比较久的话用head~版本数)
```
* 查看文件内容
```
cat file's name
Git is a distributed version control system.
Git is free software.
```
* 通过ID找回指定版本，前提命令窗口没有关闭
```
$ git reset --hard id（这里的id没必要写全，只需要前一部分就可以）
```
* 找回上次窗口执行过的版本更新操作
```
$ git reflog(查询上次操作的版本更新的id和内容)
```
## 工作区和暂存区
* 存储控件流程
1. 注意版本库在.git里面，外面是工作区
2. git add 是把工作区内容添加到暂存区（stage）中
3. git commit 是把暂存区全部提交到分支中（master）
* ![image](https://note.youdao.com/yws/public/resource/d2bf30a46dec8ae9b0be192ffefd3446/xmlnote/726A551AB523448AA7EBD703951F7192/3234)

4. 例子
* ![image](https://note.youdao.com/yws/public/resource/d2bf30a46dec8ae9b0be192ffefd3446/xmlnote/B2D0E2BFCD774D6E92B17A3CDB92E33B/3259)
* ![image](https://note.youdao.com/yws/public/resource/d2bf30a46dec8ae9b0be192ffefd3446/xmlnote/044720D14F244E1FAABB50D549EF718B/3271)
* 查看工作区和版本区的不同
```
$ git diff head -- file's name
diff --git a/readme.txt b/readme.txt
index 0734544..2c59878 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,4 +1,4 @@
 Git is a distributed version control system.
 Git is free software distributed under the GPL.
 Git has mutable index called stage.
-Git tracks changes.
+Git tracks changes files.
```
## 撤销修改
* 撤销最近工作区修改。
```
$ git checkout -- file's name
```
* 撤销暂存区中的修改的文件
```
$ git reset head file's name
```
## 删除文件
* 删除工作区文件
```
$ rm file's name
```
* 版本库中的文件
```
$ git rm file's name
```
* 用版本库中文件恢复工作区文件
```
$ git checkout -- file's name
```
## 远程仓库
* 创建SSH Key
1. 看项目目录下有没有.ssh,如果有在看看有没有id_rsa（私钥）和id_rsa.pub（公钥）
2. 如果没有上述文件,创建
```
$ ssh-keygen -t rsa -C "youremail@example.com"
```
* 注册登录Github之后，操作步骤如下
* ![image](https://note.youdao.com/yws/public/resource/d2bf30a46dec8ae9b0be192ffefd3446/xmlnote/5E8C48178E8C477A8E3C1EDDA2B22A26/3336)
* ![image](https://note.youdao.com/yws/public/resource/d2bf30a46dec8ae9b0be192ffefd3446/xmlnote/5E8C48178E8C477A8E3C1EDDA2B22A26/3336)
* ![image](https://note.youdao.com/yws/public/resource/d2bf30a46dec8ae9b0be192ffefd3446/xmlnote/83290AF7672B4E5D96FB08C183A5C476/3338)
## 添加远程库
* ![image](https://note.youdao.com/yws/public/resource/d2bf30a46dec8ae9b0be192ffefd3446/xmlnote/FFF86ECC96184C56B1B993D2A5AAD291/3350)
* ![image](https://note.youdao.com/yws/public/resource/d2bf30a46dec8ae9b0be192ffefd3446/xmlnote/B11E2F54CC154223AD8DEDD9C3E810B0/3352)
1. 把本地项目远程关联起来
```
$ git remote add origin git@github.com:username/program's file
```
2. 把项目推送和关联到远程库上（第一次需要加-u，之后就需要了）
```
$ git push -u origin master
```
第一次clone或者push命令连接Github可能会警告
```
The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established.
RSA key fingerprint is xx.xx.xx.xx.xx.
Are you sure you want to continue connecting (yes/no)?
$ yes 
```
## 从远程库克隆
* 创建远程库
* ![image](https://note.youdao.com/yws/public/resource/d2bf30a46dec8ae9b0be192ffefd3446/xmlnote/5BA640016CDD4B4FA2B589078753E6F3/3385)
* 克隆远程库(把目录切换到你要克隆的文件位置)
```
$ git clone https://github.com/ICEMARK123/gitlearn.git
Cloning into 'gitlearn'...

remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
```
## 创建于合并分支
查看分支：git branch

创建分支：git branch <name>

切换分支：git checkout <name>

创建+切换分支：git checkout -b <name>

合并某分支到当前分支：git merge <name>

删除分支：git branch -d <name>
## 解决冲突
* 创建分支并切换到创建的分支
```
$ git checkout -b branch's name
```
* 修改项目内容
* 添加与提交
```
$ git add file's name
$ git commit -m "describe"
```
* 切换到主分支
```
$ git checkout master
```
* 更改和新建的分支同样的文件
* 添加并提交
```
$ git add file's name
$ git commit -m "describe"
```
* 合并分支 (这是会报出冲突提示)
```
$ git merge branch's name
```
* 然后把有冲突的文件内容更改成自己想要的内容再次提交
* 查看分支合并情况
```
$ git log --graph --pretty=oneline -abbrev-commit
```
* 最后删除分支
```
$ git branch -d branch's name
```
## 分支管理策略
* 禁用fast forward，这种方式，分支信息不丢失
```
git merge --no-ff -m 'merge with no-ff' branch's name
```
* 开发过程中，不在稳定的master上开发，而是在不稳定的分支上面开发，然后在进行合并到master上面。
## Bug分支
* 首先把当前分支的工作保存下来
```
$ git stash
```
* 创建临时分支，看看你想在那个分支上面修改bug就切换到那个分支上面
```
$ git checkout branch's name
$ git checkout -b but-branch's name
```
* 然后开始修复bug，修复完后提交
```
$ git add file's name
$ git commit -m 'describe'
```
* 最后合并，删除临时分支
```
$ git checkout branch's name
$ git merge --no-ff -m 'merge bug fix' bug-branch's name
$ git branch -d bug-branch's name
```
* 跳回原来的分支工作
```
$ git checkout work-branch
$ git status （工作区是干净的）
```
* 查看所有存储区
```
$ git stash list
```
* 恢复原来工作区的内容
```
$ git stash apply (恢复不删除stash内容，还需要$ git stash drop来删除)
$ git stash pop (恢复并删除)
```
* 如果你多次使用了stash，可以指定恢复stash
```
$ git stash list(查看编号)
$ git stash apply stash@{id}(恢复指定编号的内容)
```
## Feature分支
* 开发过程中，应需求开发新功能，用一个新的分支来开发，如果该需求最终不需要了，不用合并了，需要删除该分支。
```
$ git brranch -D branch's name(强制删除)
```
## 多人协作
* 产看远程库的信息
```
$ git remote
$ git remote -v(查看最详细的远程库的信息)
```
* 分支推送
```
$ git push origin master(推送到主分支)
$ git push origin branch's name(推送到工作分支)
```
master：分支是主分支，因此要时刻与远程同步。
dev: 分支是开发分支，团队所有成员都需要子啊上面工作所以也需要与远程同步；
bug：bug分支主要用于本地修复bug，就没必要推到远程了，除了费老板要看看你每周到底修复了几个bug。
feature:分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。


* 抓取分支
```
$ git checkout -b dev origin/dev(抓取远程分支)
```
* 解决同一个分支两个人跟新提交同一个文件冲突
1. 本地分支与远程origin/dev分支的连接
```
$ git branch --set-upstream-to orgin/dev
```
2. 把最新的抓下来,合并
```
$ git pull
```
3. 推送
```
git push origin dev
```
## 标签管理
* 创建标签
1. 确定在那个分支上面创建标签
```
$ git branch
$ git checkout branche's name
$ git tag version number(创建标签)
```
2. 如果忘记打标签了,通过查询修改日志中的修改id
```
$ git log --pretty=oneline --abbrev-commit
$ git tag version number id
$ git tag
```
3. 查看详细的标签信息
```
$ $ git show tag
```
4. 添加标签可以添加标签说明
```
$ git tag -a v1.0 -m "version 1.0 released" id
```
5. 用私钥签名一个标签
```
$ git tag -s v0.2 -m "signed version 0.2 released" id 
```
6. 删除标签
```
$ git tag -d v0.1
```
7. 推送标签
```
$ git push origin tagname（推送一个标签）
$ git push origin --tags（推送所有标签）
```
8. 删除远程标签
```
$ git push origin :refs/tags/tagname
```
## 使用码云
* ![image](https://note.youdao.com/yws/public/resource/d2bf30a46dec8ae9b0be192ffefd3446/xmlnote/7EA880F381C449D2ABCA608CCC4E7E3F/3671)
* ![image](https://note.youdao.com/yws/public/resource/d2bf30a46dec8ae9b0be192ffefd3446/xmlnote/BE87700DCEB04CCEBF9EE1C7F391375F/3677) 
* 删除、添加关联
```
$ git remote -d origin's namne（删除远程库）
$ git remote add origin's name git@gitee.com:lhl_1541914268/gitlearn.git（添加码云关联）
$ git remote add origin's name git@github.com:ICEMARK123/gitlearn.git（添加github关联）
```
* 查看关联的远程库信息
```
$ git remote -v
```
## 配置命令别名
```
$ git config --global alias.st status （一个命令单词）
$ git config --global alias.unstage 'reset HEAD'（多个命令单词）
```

## 提交步骤

$ git add -A(添加所有的文件)/文件名

$ git commit -m "describe"

$ git push -u origin master(主分支)
    