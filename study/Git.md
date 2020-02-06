[一、Git结构](https://github.com/xingyuexingyue/sangyu/blob/master/study/Git.md#%E4%B8%80git%E7%BB%93%E6%9E%84)

[二、Git和代码托管中心](https://github.com/xingyuexingyue/sangyu/blob/master/study/Git.md#%E4%BA%8Cgit%E5%92%8C%E4%BB%A3%E7%A0%81%E6%89%98%E7%AE%A1%E4%B8%AD%E5%BF%83)

[三、本地库和远程库的交互方式](https://github.com/xingyuexingyue/sangyu/blob/master/study/Git.md#%E4%B8%89%E6%9C%AC%E5%9C%B0%E5%BA%93%E5%92%8C%E8%BF%9C%E7%A8%8B%E5%BA%93%E7%9A%84%E4%BA%A4%E4%BA%92%E6%96%B9%E5%BC%8F)

[四、设置签名](https://github.com/xingyuexingyue/sangyu/blob/master/study/Git.md#%E5%9B%9B%E8%AE%BE%E7%BD%AE%E7%AD%BE%E5%90%8D)

[五、添加提交以及查看状态操作](https://github.com/xingyuexingyue/sangyu/blob/master/study/Git.md#%E4%BA%94%E6%B7%BB%E5%8A%A0%E6%8F%90%E4%BA%A4%E4%BB%A5%E5%8F%8A%E6%9F%A5%E7%9C%8B%E7%8A%B6%E6%80%81%E6%93%8D%E4%BD%9C)

[六、版本穿梭](https://github.com/xingyuexingyue/sangyu/blob/master/study/Git.md#%E5%85%AD%E7%89%88%E6%9C%AC%E7%A9%BF%E6%A2%AD)

[七、基于索引值前进后退版本-推荐](https://github.com/xingyuexingyue/sangyu/blob/master/study/Git.md#%E4%B8%83%E5%9F%BA%E4%BA%8E%E7%B4%A2%E5%BC%95%E5%80%BC%E5%89%8D%E8%BF%9B%E5%90%8E%E9%80%80%E7%89%88%E6%9C%AC-%E6%8E%A8%E8%8D%90)

[八、使用^ 后退版本](https://github.com/xingyuexingyue/sangyu/blob/master/study/Git.md#%E5%85%AB%E4%BD%BF%E7%94%A8-%E5%90%8E%E9%80%80%E7%89%88%E6%9C%AC)

[九、使用～ 后退版本](https://github.com/xingyuexingyue/sangyu/blob/master/study/Git.md#%E4%B9%9D%E4%BD%BF%E7%94%A8-%E5%90%8E%E9%80%80%E7%89%88%E6%9C%AC)

[十、reset命令的三个参数对比](https://github.com/xingyuexingyue/sangyu/blob/master/study/Git.md#%E5%8D%81reset%E5%91%BD%E4%BB%A4%E7%9A%84%E4%B8%89%E4%B8%AA%E5%8F%82%E6%95%B0%E5%AF%B9%E6%AF%94)

[十一、永久删除文件后找回](https://github.com/xingyuexingyue/sangyu/blob/master/study/Git.md#%E5%8D%81%E4%B8%80%E6%B0%B8%E4%B9%85%E5%88%A0%E9%99%A4%E6%96%87%E4%BB%B6%E5%90%8E%E6%89%BE%E5%9B%9E)

[十二、添加到暂存区的删除文件找回](https://github.com/xingyuexingyue/sangyu/blob/master/study/Git.md#%E5%8D%81%E4%BA%8C%E6%B7%BB%E5%8A%A0%E5%88%B0%E6%9A%82%E5%AD%98%E5%8C%BA%E7%9A%84%E5%88%A0%E9%99%A4%E6%96%87%E4%BB%B6%E6%89%BE%E5%9B%9E)

[十三、比较文件](https://github.com/xingyuexingyue/sangyu/blob/master/study/Git.md#%E5%8D%81%E4%B8%89%E6%AF%94%E8%BE%83%E6%96%87%E4%BB%B6)

[十四、分支概述](https://github.com/xingyuexingyue/sangyu/blob/master/study/Git.md#%E5%8D%81%E5%9B%9B%E5%88%86%E6%94%AF%E6%A6%82%E8%BF%B0)

[十五、分支操作](https://github.com/xingyuexingyue/sangyu/blob/master/study/Git.md#%E5%8D%81%E4%BA%94%E5%88%86%E6%94%AF%E6%93%8D%E4%BD%9C)

[十六、解决合并分支后产生的冲突](https://github.com/xingyuexingyue/sangyu/blob/master/study/Git.md#%E5%8D%81%E5%85%AD%E8%A7%A3%E5%86%B3%E5%90%88%E5%B9%B6%E5%88%86%E6%94%AF%E5%90%8E%E4%BA%A7%E7%94%9F%E7%9A%84%E5%86%B2%E7%AA%81)

[十七、本地创建远程仓库别名](https://github.com/xingyuexingyue/sangyu/blob/master/study/Git.md#%E5%8D%81%E4%B8%83%E6%9C%AC%E5%9C%B0%E5%88%9B%E5%BB%BA%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93%E5%88%AB%E5%90%8D)

[十八、远程仓库推送操作](https://github.com/xingyuexingyue/sangyu/blob/master/study/Git.md#%E5%8D%81%E5%85%AB%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93%E6%8E%A8%E9%80%81%E6%93%8D%E4%BD%9C)

[十九、克隆操作](https://github.com/xingyuexingyue/sangyu/blob/master/study/Git.md#%E5%8D%81%E4%B9%9D%E5%85%8B%E9%9A%86%E6%93%8D%E4%BD%9C)

[二十、远程库修改的拉取](https://github.com/xingyuexingyue/sangyu/blob/master/study/Git.md#%E4%BA%8C%E5%8D%81%E8%BF%9C%E7%A8%8B%E5%BA%93%E4%BF%AE%E6%94%B9%E7%9A%84%E6%8B%89%E5%8F%96)

[二十一、协同开发冲突的解决](https://github.com/xingyuexingyue/sangyu/blob/master/study/Git.md#%E4%BA%8C%E5%8D%81%E4%B8%80%E5%8D%8F%E5%90%8C%E5%BC%80%E5%8F%91%E5%86%B2%E7%AA%81%E7%9A%84%E8%A7%A3%E5%86%B3)




## 一、Git结构

![](https://upload-images.jianshu.io/upload_images/2765653-8a3a4e85e4fb0d3a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 二、Git和代码托管中心

代码托管中心的任务：维护远程库
局域网环境下：GitLab服务器
外网环境下：码云


## 三、本地库和远程库的交互方式

团队内部协作

![](https://upload-images.jianshu.io/upload_images/2765653-e9de0da140a76a0d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
$ git init // 初始化本地库
Initialized empty Git repository in /Users/xxx/sangyu/sangyuStudy/.git/ // .git目录中存放的是本地库相关的子目录和文件，不要删除和随意修改
```
## 四、设置签名

作用：区分不同开发人员的身份
设置的签名和登录远程库(代码托管中心)的账号、密码没有任何关系
级别优先级：就近原则，项目优先级优先于系统用户级别，二者都没有不允许

```
// 项目级别/仓库级别：仅在当前本地库范围内有效，信息保存位置：./git/config 文件
$ git config user.name sangyu // 设置user
$ git config user.email xx@xx.com // 设置email
$ cat .git/config // 查看设置的user和email
[core]
        repositoryformatversion = 0
        filemode = true
        bare = false
        logallrefupdates = true
        ignorecase = true
        precomposeunicode = true
[user]
        name = sangyu
        email = xx@xx.com
```

```
// 系统用户级别：登录当前操作系统的用户范围，信息保存位置：~/.gitconfig 文件
git config --global user.name xxx
git config --global user.email xxx@xx.com
```

## 五、添加提交以及查看状态操作

```
$ git status
On branch master // 在master分支，默认的，也可以称为主干

No commits yet // 本地库没有提交过任何东西

Untracked files: // 可以提交到暂存区的内容
  (use "git add <file>..." to include in what will be committed) // 可以使用git add提交

        sangyuStudy.iml
        study/
nothing added to commit but untracked files present (use "git add" to track)
```

```
$ git add * // 添加到暂存区所有可添加的
$ git status
On branch master

No commits yet

Changes to be committed: // 更改要提交的
  (use "git rm --cached <file>..." to unstage)

        new file:   sangyuStudy.iml
        new file:   study/Git.md
```

```
$ git rm --cached study/Git.md // 从暂存区移除study/Git.md
rm 'study/Git.md'
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   sangyuStudy.iml

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        study/

$ git add study/Git.md // 重新添加study/Git.md到暂存区
$ git status // 查看状态
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   sangyuStudy.iml
        new file:   study/Git.md
```

```
$ git commit // 提交到工作区
# Please enter the commit message for your changes. Lines starting // 加入本次提交的注释
# with '#' will be ignored, and an empty message aborts the commit. 
# 
# On branch master 
#
# Initial commit
#
# Changes to be committed:
#       new file:   sangyuStudy.iml
#       new file:   study/Git.md
-- 可视 --             
# vim编辑模式，底部命令i进入输入模式
# 输入后，esc退出输入模式
# 进入底部命令模式，:wq退出并保存      
[master (root-commit) 4b5caec] My second commits //  (root-commit) 4b5caec 根提交只能有一个
 2 files changed, 12 insertions(+)
 create mode 100644 sangyuStudy.iml
 create mode 100644 study/Git.md      
```

```
// 修改文件后查看状态
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed) // 添加到暂存区
  (use "git checkout -- <file>..." to discard changes in working directory) // 用这个命令撤销修改

        modified:   study/Git.md

no changes added to commit (use "git add" and/or "git commit -a") // and/or 可以add后commit，或者直接commit
```

```
$ git commit -m "my second commit" . // 不进入vim，直接在命令中增加当次提交的注释 使用-m
[master c9f56c0] my second commit // [master c9f56c0] ，在根提交的基础上
 1 file changed, 3 insertions(+), 1 deletion(-)
```

## 六、版本穿梭

```
$ git log  // 查看版本历史记录
commit c9f56c0dac410a229da58dbe14824d6ba5650733 (HEAD -> master) // commit c9f56c0dac410a229da58dbe14824d6ba5650733 本次提交的索引;HEAD -> master :head是指针指向当前的版本
Author: sangyu <xx@xx.com>
Date:   Wed Feb 5 11:14:23 2020 +0800

    my second commit

commit 62149d060c283232d01a2c059e033cf67705e82b
Author: sangyu <935789914@qq.com>
Date:   Wed Feb 5 11:12:30 2020 +0800

    my third commits
：// 表示的日志太多，enter继续查看后面的日志
// b 向上翻页
// q 退出
```

```
$ git log --pretty=oneline // 日志按行展示
c9f56c0dac410a229da58dbe14824d6ba5650733 (HEAD -> master) my second commit
62149d060c283232d01a2c059e033cf67705e82b my third commits
4b5caec431700bda84f5c42c69547054e85de96a My second commits
```

```
$ git log --oneline // 日志展示的第二种方式
c9f56c0 (HEAD -> master) my second commit // c9f56c0 索引值的一部分
62149d0 my third commits
4b5caec My second commits
```

```
$ git reflog // 日志展示的第三种方式
c9f56c0 (HEAD -> master) HEAD@{0}: commit: my second commit //{x} 到某个版本需要移动的步数 
62149d0 HEAD@{1}: commit: my third commits
4b5caec HEAD@{2}: commit (initial): My second commits
```
##  七、基于索引值前进后退版本-推荐
```
$ git reset --hard 62149d0
HEAD is now at 62149d0 my third commits // head指向了62149d0所在版本
$ git reflog
62149d0 (HEAD -> master) HEAD@{0}: reset: moving to 62149d0
c9f56c0 HEAD@{1}: commit: my second commit
62149d0 (HEAD -> master) HEAD@{2}: commit: my third commits
4b5caec HEAD@{3}: commit (initial): My second commits
```

##  八、使用^ 后退版本
```
$ git reset --hard HEAD^ // ^表示以当前版本往后退一步
HEAD is now at 9994181 4
```
##  九、使用～ 后退版本

```
$ git reset --hard HEAD~2 // 数字是几表示后退几个版本
HEAD is now at 7e610f6 3
```

## 十、reset命令的三个参数对比

```--soft``` 仅仅在本地库移动HEAD指针

```--mixed``` 在本地库移动HEAD指针、重置暂存区

```--hard``` 在本地库移动HEAD指针、重置暂存、重置工作区

##  十一、永久删除文件后找回

```
$ rm  study/aa.txt // 删除文件
$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        deleted:    study/aa.txt

$ git commit -m 'delete' . // 提交到本地库，记录这个文件的删除,git只会增加版本，不会删除
[master a281a9a] delete
 2 files changed, 1 insertion(+), 1 deletion(-)
 delete mode 100644 study/aa.txt

$ git reset --hard fc81d02 // 执行后删除的文件会恢复
HEAD is now at fc81d02 1
```

##  十二、添加到暂存区的删除文件找回

```
$ rm study/apple.txt // 删除文件后没有添加到本地库
$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        deleted:    study/apple.txt

no changes added to commit (use "git add" and/or "git commit -a")
$ git reset --hard HEAD // 找回文件
HEAD is now at 3b9743c apple
```

##  十三、比较文件

```
$ git diff study/apple.txt // 修改文件，diff工作区和暂存区的比较
diff --git a/study/apple.txt b/study/apple.txt
index 04a9f41..297bd50 100644
--- a/study/apple.txt
+++ b/study/apple.txt
@@ -1,3 +1,3 @@
 1111
-2222 // - 表示删除
+2222 aaa // + 表示新增加
 3333
\ No newline at end of file
```

```
n$ git diff HEAD study/apple.txt // 和暂存区的某个版本进行比较
diff --git a/study/apple.txt b/study/apple.txt
index 04a9f41..297bd50 100644
--- a/study/apple.txt
+++ b/study/apple.txt
@@ -1,3 +1,3 @@
 1111
-2222
+2222 aaa
 3333
\ No newline at end of file
```

```
$ git diff HEAD^ study/ee.txt // 和某个历史版本比较
diff --git a/study/ee.txt b/study/ee.txt
new file mode 100644
index 0000000..d5644ad
--- /dev/null
+++ b/study/ee.txt
@@ -0,0 +1,11 @@
+1
+
+2
+
+3 111
```

```
$ git diff // 不带文件名，比较多个文件
diff --git a/study/Git.md b/study/Git.md
index c0da29a..3f0d704 100644
--- a/study/Git.md
+++ b/study/Git.md
@@ -4,4 +4,8 @@
 
 2. 修改
 
-3. 
\ No newline at end of file
+3. 
```

## 十四、分支概述

![](https://upload-images.jianshu.io/upload_images/2765653-7cf2fb490c249352.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

分支的好处：
同时并行推进多个功能开发，提高开发效率
各个分支在开发过程中，如果某一个分支开发失败，不会对其他分支有任何影响。失败的分支删除重新开始即可

## 十五、分支操作

```
$ git branch -v // 查看当前所有的分支
* master 801553e apple. // 只有1个分支master，并且当前所在分支也是master
```

```
$ git branch hot-fix // 创建新的分支 hot-fix
$ git branch -v 
  hot-fix 801553e apple.
* master  801553e apple.
```

```
$ git checkout hot-fix // 切换分支
Switched to branch 'hot-fix'
$ git branch -v
* hot-fix 801553e apple. // 当前所在分支hot-fix
  master  801553e apple.
```

```
// 在hot-fix 分支上修改
$ git add .
$ git commit -m 'hot-fix' .
[hot-fix e50785a] hot-fix
 4 files changed, 27 insertions(+), 2 deletions(-)
 create mode 100644 study/cc.txt
 create mode 100644 study/ee.txt
$ git branch -v
* hot-fix e50785a hot-fix
  master  801553e apple.
// 合并分支
$ git checkout master // 第一步：合并到接受修改的分支上（被合并，增加新内容）
$ git branch -v
  hot-fix e50785a hot-fix
* master  801553e apple.

$ git merge hot-fix //第二步：执行merge命令
Updating 801553e..e50785a
Fast-forward
 study/Git.md    |  6 +++++-
 study/apple.txt |  2 +-
 study/cc.txt    | 10 ++++++++++
 study/ee.txt    | 11 +++++++++++
 4 files changed, 27 insertions(+), 2 deletions(-)
 create mode 100644 study/cc.txt
 create mode 100644 study/ee.txt
```

## 十六、解决合并分支后产生的冲突

```
// 两个分支上分别对同一个文件同一个地方做不同的修改
// 合并分支
$ git merge master  
Auto-merging study/good.txt // 产生分支冲突，必须手动修改
CONFLICT (content): Merge conflict in study/good.txt
Automatic merge failed; fix conflicts and then commit the result.
```

![分支冲突的表现](https://upload-images.jianshu.io/upload_images/2765653-17da5101817a676e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
// 冲突的解决
$ git status // 修改文件后查看status
On branch hot-fix
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)

        both modified:   study/good.txt

no changes added to commit (use "git add" and/or "git commit -a")

$ git add . // 使用add 标记冲突已解决
$ git status // 此时在查看status，冲突已修复
On branch hot-fix
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

Changes to be committed:

        modified:   study/good.txt
$ git commit -m 'conclude merge' // 使用git commit结束合并 不可带文件名称，可带 注释
```

## 十七、本地创建远程仓库别名

```
$ git remote add origin https://github.com/xingyuexingyue/sangyu.git // origin: 别名；url是远程仓库地址

$ git remote -v // 查看远程仓库地址
origin  https://github.com/xingyuexingyue/sangyu.git (fetch) // 取回
origin  https://github.com/xingyuexingyue/sangyu.git (push) // 推送
```

## 十八、远程仓库推送操作

```
$ git push origin master // 推送到远程仓库必须指定分支
```

## 十九、克隆操作

```
$ git clone https://github.com/xingyuexingyue/sangyu.git
Cloning into 'sangyu'...
remote: Enumerating objects: 50, done.
remote: Counting objects: 100% (50/50), done.
remote: Compressing objects: 100% (30/30), done.
remote: Total 50 (delta 5), reused 50 (delta 5), pack-reused 0
Unpacking objects: 100% (50/50), done.
```

## 二十、远程库修改的拉取

```
// pull 相当于fetch 和merge
$ git fetch origin master
From https://github.com/xingyuexingyue/sangyu
 * branch            master     -> FETCH_HEAD
$ git merge origin/master
```

## 二十一、协同开发冲突的解决

如果不是基于GitHub远程库的最新版所做的修改，不能推送，必须先拉取

拉取下来后如果进入冲突状态，则按照“分支冲突解决”操作解决即可

```
// 两个账号分别对远程仓库相同位置做不同的修改
// 先pull下来，再提交到远程仓库
```

![协同开发冲突表现](https://upload-images.jianshu.io/upload_images/2765653-5b781e7d64f584af.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![协同开发冲突解决](https://upload-images.jianshu.io/upload_images/2765653-ecbee91ecb87bd90.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)