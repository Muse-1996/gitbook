# Git命令

```bash
kill -USR2 平滑重启

Git 常用命令

git prune 处理本地的松散碎片，提高git运行速度

常用的git命令:
------------------------------------------------
同步git所有分支状态
git fetch -p 

更新当前选中分支的代码（先执行git fetch -p 更新状态)
git checkout 分支名
git pull  拉代码

从远端下分支到本地
git branch 分支名  origin/分支名

切换分支
git checkout 分支名

删除本地分支
git branch -D 分支名

建立一个本地的分支
git checkout -b dev 建立一个新的本地分支dev

推到远端
git push origin
git log查看日志

在没有fetch的情况下，查看最后一个提交点
$ git merge-base personal/heige/master-1015 master
212ea466d23af9322131e0535b2dc02c008d065e    sha密钥

查看git操作别名
 vim ~/.gitconfig
 

------------------------------------------------

配置git的快捷键使用 git 接着下面的命名
vim ~/.gitconfig
添加如下内容：
[alias]
st=status
co=checkout
br=branch
ci=commit . -m
fe=fetch -p
pu=pull
lg=log --graph --pretty=format:'%h %ci [%Cgreen%an%Creset]%s'
lgst=log --pretty=format:'%H [%an] %ci%ncommit:%s' --stat

使用方法
git st 查看状态
git co my -b mylocal 建立本地分支
git br 查看分支
git fe 同步状态
git pu  拉代码
git lg  看看提交的日志
git lgst 查看提交的日志，状态，时间格式化处理


常用的命令：

git branch 查看本地所有分支
git status 查看当前状态 
git commit 提交 
git branch -a 查看所有的分支
git branch -r 查看本地所有分支
git commit -am "init" 提交并且加注释 
git remote add origin git@192.168.1.119:ndshow
git push origin master 将文件给推到服务器上 
git remote show origin 显示远程库origin里的资源 
git push origin master:develop
git push origin master:hb-dev 将本地库与服务器上的库进行关联 
git checkout --track origin/dev 切换到远程dev分支
git branch -D master develop 删除本地库develop
git checkout -b dev 建立一个新的本地分支dev
git merge origin/dev 将分支dev与当前分支进行合并
git checkout dev 切换到本地dev分支
git remote show 查看远程库
git add .
git rm 文件名(包括路径) 从git中删除指定文件
git clone git://github.com/schacon/grit.git 从服务器上将代码给拉下来
git config --list 看所有用户
git ls-files 看已经被提交的
git rm [file name] 删除一个文件
git commit -a 提交当前repos的所有的改变
git add [file name] 添加一个文件到git index
git commit -v 当你用－v参数的时候可以看commit的差异
git commit -m "This is the message describing the commit" 添加commit信息
git commit -a -a是代表add，把所有的change加到git index里然后再commit
git commit -a -v 一般提交命令
git log 看你commit的日志
git diff 查看尚未暂存的更新
git rm a.a 移除文件(从暂存区和工作区中删除)
git rm --cached a.a 移除文件(只从暂存区中删除)
git commit -m "remove" 移除文件(从Git中删除)
git rm -f a.a 强行移除修改后文件(从暂存区和工作区中删除)
git diff --cached 或 $ git diff --staged 查看尚未提交的更新
git stash push 将文件给push到一个临时空间中
git stash pop 将文件从临时空间pop下来
---------------------------------------------------------
git remote add origin git@github.com:username/Hello-World.git
git push origin master 将本地项目给提交到服务器中
-----------------------------------------------------------
git pull 本地与服务器端同步
-----------------------------------------------------------------
git push (远程仓库名) (分支名) 将本地分支推送到服务器上去。
git push origin serverfix:awesomebranch
------------------------------------------------------------------
git fetch 相当于是从远程获取最新版本到本地，不会自动merge
git commit -a -m "log_message" (-a是提交所有改动，-m是加入log信息) 本地修改同步至服务器端 ：
git branch branch_0.1 master 从主分支master创建branch_0.1分支
git branch -m branch_0.1 branch_1.0 将branch_0.1重命名为branch_1.0
git checkout branch_1.0/master 切换到branch_1.0/master分支
du -hs


【打补丁】
-----------------------------------------------------------------
git diff > /tmp/tmp0709_patch
git apply /tmp/tmp0709_pathc


从master checkout一个新分支修改然后与master对比生成patch。
git format-patch -M master //-M选项表示这个patch要和那个分支比对
git am 001-xxx.patch（不必重新commit）

【查分支第一个开始点】
-----------------------------------------------------------------
git merge-base master group/api/version3.2.3_beta1  组分支是从master那个点开始的

【ag】 alias
-----------------------------------------------------------------
内网，保存别人的服务器上更改，再丢弃，更新代码，再把更改应用回来
-----------------------------------------------------------------
【合并代码到一个点】
git log `git branch | grep "\*" |cut -d " " -f 2` --pretty="%H" --not master | tail -n 1 | xargs -i git reset --soft {}~1 && git commit -m `read -p "请输入注释： " com && echo $com` && git log -1 --stat

-----------------------------------------------------------------
【rebase命令】
git rebase `git fetch -p && git log origin/master --pretty="%H" -1`

-----------------------------------------------------------------
git log 格式化

查看提交历史，并单行显示：                        $ git log --pretty=oneline

查看提交历史，并格式化显示：                      $ git log --pretty=format:"%h - %an, %ar : %s"

git log --pretty=format:'%H %ad %s (%an)' --date=short group/api/temai31

git log --pretty=format:"%H [%an] %ci %s" group/api/temai31 【显示日志标准格式】


    %H: commit hash
    %h: 缩短的commit hash
    %T: tree hash
    %t: 缩短的 tree hash
    %P: parent hashes
    %p: 缩短的 parent hashes
    %an: 作者名字
    %aN: mailmap的作者名字 (.mailmap对应，详情参照git-shortlog(1)或者git-blame(1))
    %ae: 作者邮箱
    %aE: 作者邮箱 (.mailmap对应，详情参照git-shortlog(1)或者git-blame(1))
    %ad: 日期 (--date= 制定的格式)
    %aD: 日期, RFC2822格式
    %ar: 日期, 相对格式(1 day ago)
    %at: 日期, UNIX timestamp
    %ai: 日期, ISO 8601 格式
    %cn: 提交者名字
    %cN: 提交者名字 (.mailmap对应，详情参照git-shortlog(1)或者git-blame(1))
    %ce: 提交者 email
    %cE: 提交者 email (.mailmap对应，详情参照git-shortlog(1)或者git-blame(1))
    %cd: 提交日期 (--date= 制定的格式)
    %cD: 提交日期, RFC2822格式
    %cr: 提交日期, 相对格式(1 day ago)
    %ct: 提交日期, UNIX timestamp
    %ci: 提交日期, ISO 8601 格式
    %d: ref名称
    %e: encoding
    %s: commit信息标题
    %f: sanitized subject line, suitable for a filename
    %b: commit信息内容
    %N: commit notes
    %gD: reflog selector, e.g., refs/stash@{1}
    %gd: shortened reflog selector, e.g., stash@{1}
    %gs: reflog subject
    %Cred: 切换到红色
    %Cgreen: 切换到绿色
    %Cblue: 切换到蓝色
    %Creset: 重设颜色
    %C(...): 制定颜色, as described in color.branch.* config option
    %m: left, right or boundary mark
    %n: 换行
    %%: a raw %
    %x00: print a byte from a hex code
    %w([[,[,]]]): switch line wrapping, like the -w option of git-shortlog(1).

-----------------------------------------------------------
mkdir WebApp
cd WebApp
git init
touch README
git add README
git commit -m 'first commit'
git remote add origin git@github.com:daixu/WebApp.git
git push -u origin master

空间清理
$ git gc 
$ git prune  

~/.gitconfig
[user]
        name = heige
        email = heige@juanpi.com

[alias]
st=status
co=checkout
br=branch
ci=commit . -m
fe=fetch -p
pu=pull
lg=log --graph --pretty=format:'%h %ci [%Cgreen%an%Creset]%s'
lgst=log --pretty=format:'%H [%an] %ci%ncommit:%s' --stat
puor=push origin


回退至指定提交
git reset --hard HEAD_id
git push --force
```

