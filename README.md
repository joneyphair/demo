## Git大法


#### 基本命令

* 初始化git仓库

```
  git init
  
```

* 把工作区的修改提交到暂存区


``` 
 touch demo.html

```

``` 
 git add demo.html

```

* 把暂存区的所有内容提交到当前分支


``` 
 git commit -m "feat: 新增demo.html 文件"

```

```
[master (root-commit) cb01fc0] feat: 新增demo.html 文件
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 demo.html
```


* 把远程库和本地仓库关联


``` 
 git remote add origin git@github.com:joneyphair/demo.git
 
```


把本地master 分支推送到远程仓库
>-u参数在第一次推送相应分支的时候用

``` 
  git push -u origin master

```

```
Counting objects: 5, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (5/5), 488 bytes | 0 bytes/s, done.
Total 5 (delta 0), reused 0 (delta 0)
To git@github.com:joneyphair/demo.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.

```

* 从远程库克隆出一个本地库

``` 
git clone git@github.com:joneyphair/demo.git

```

```
Cloning into 'demo'...
remote: Counting objects: 5, done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 5 (delta 0), reused 5 (delta 0), pack-reused 0
Receiving objects: 100% (5/5), done.
Checking connectivity... done.
```

#### 分支

* 创建dev分支，然后切换到dev分支


``` 
git checkout -b dev

```


同

``` 
git branch dev
git checkout dev

```

```
Switched to a new branch 'dev'

```

* 查看分支

``` 
git branch

```


* 提交分支


>添加一些内容

```
vim dev.html
git add .
git commit -m 'feat: 新增dev.html 文件'

```
>提交

```
git push 
```

```
fatal: The current branch dev has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin dev
```

```
git push --set-upstream origin dev

```


```
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 353 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To git@github.com:joneyphair/demo.git
   d81cf08..5776804  dev -> dev
```



#### 历史记录


* 查看所有提交历史记录

``` 
git log

```

```
commit 5a4ca0ec6c45db28e2a1e1cbf155928087171f72
Author: 张屈 <joneyphair@qq.com>
Date:   Tue Aug 23 19:52:06 2016 +0800

    docs: 新增README.md 说明文件

commit cb01fc041d93afaf43473f71a23bb5542f234330
Author: 张屈 <joneyphair@qq.com>
Date:   Tue Aug 23 19:48:30 2016 +0800

    feat: 新增demo.html 文件
(END)

```

* 查看文件提交记录

``` 
 git log demo.html 
 
```

```
commit cb01fc041d93afaf43473f71a23bb5542f234330
Author: 张屈 <joneyphair@qq.com>
Date:   Tue Aug 23 19:48:30 2016 +0800

    feat: 新增demo.html 文件
(END)

```

* 查看commit修改信息

```
git show d81cf08fee5e16cabf4f8880f0760c1ecf2b355e

```
```
commit d81cf08fee5e16cabf4f8880f0760c1ecf2b355e
Author: 张屈 <joneyphair@qq.com>
Date:   Tue Aug 23 20:00:18 2016 +0800

    feat: 修改demo.html

diff --git a/demo.html b/demo.html
index e69de29..3f5ec39 100644
--- a/demo.html
+++ b/demo.html
@@ -0,0 +1,10 @@
+<!DOCTYPE html>
+<html lang="en">
+<head>
+       <meta charset="UTF-8">
+       <title></title>
+</head>
+<body>
+
+</body>
+</html>
(END)


```

* 查看命令操作记录（很强大）

``` 
git reflog

```

#### 吃后悔药，补救


* 回退到上一个版本


``` 

git reset --hard HEAD^

```

* 回退到任意commit 节点

``` 

git reset --hard commit_id

```


* 查看当前分支修改状态


``` 

vim demo.html (修改这个文件)

git status

```

```
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

       	modified:   demo.html

no changes added to commit (use "git add" and/or "git commit -a")
```

* 查看工作区和版本库里面最新版本的区别


``` 
git diff demo.html

```

```
diff --git a/demo.html b/demo.html
index 3f5ec39..82ebb30 100644
--- a/demo.html
+++ b/demo.html
@@ -5,6 +5,8 @@
        <title></title>
 </head>
 <body>
+
+       添些内容

 </body>
 </html>
(END)

```


* 丢弃工作区的修改


``` 
git checkout demo.html （丢弃demo.html 文件的修改）

git status  (查看当前状态)

```

```
On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working directory clean

```
* 查看本地分支

```

* dev
  master

```

* 查看所有分支（包含远端分支）
>前面带＊的代表当前所在的分支名


```
* dev 
  master
  remotes/origin/dev
  remotes/origin/master
```


* 合并dev到master分支


``` 
git checkout master
git merge dev

```

```
Updating d81cf08..5776804
Fast-forward
 dev.html | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 dev.html

```


* 删除本地分支

``` 
git branch -D dev

```

出现如下错误提示，需要切换到其他分支，然后才能成功执行 ``git branch -D dev`` 操作

```
error: Cannot delete the branch 'dev' which you are currently on.
```

```
Deleted branch dev (was 5776804).
```

* 拉取远端所有代码到本地仓库

```
git fetch

```

* 拉取最新代码并且进行合并操作

``` 
git pull

```


* 工作现场 (当手头工作没有完成时，先把工作现场暂存)

``` 
git stash

```


* 修复bug后再git stash pop，回到工作现场


``` 
git stash pop

```

* 查看工作现场列表

``` 
git stash list

```


### Commit Message格式(规范)


每次提交，Commit message 都包括两个部分：**Header**，**Body** 。header中的 **type** 和 **subject**有特殊的规定

```
<type>: <subject>
// 空一行
<body>
```
其中，**Header** 是必需的，**Body**  可以省略。
不管是哪一个部分，任何一行都不得超过72个字符（或100个字符）。这是为了避免自动换行影响美观。

#### Header

##### type

```
* feat：新功能（feature）
* fix：修补bug
* docs：文档（documentation）
* style： 格式（不影响代码运行的变动）
* refactor：重构（即不是新增功能，也不是修改bug的代码变动）
* test：增加测试
* chore：构建过程或辅助工具的变动
```

注：如果type为feat和fix，则该 commit 将肯定出现在 Change log 之中。其他情况（docs、chore、style、refactor、test）由你决定，要不要放入 Change log，建议是不要。

##### subject
**subject**是 commit 目的的简短描述，不超过50个字符。

```
* 以动词开头，使用第一人称现在时，比如change，而不是changed或changes
```
#### Body

**Body** 部分是对本次 commit 的详细描述，可以分成多行

```
* 使用第一人称现在时，比如使用change而不是changed或changes。
* 应该说明代码变动的动机，以及与以前行为的对比。
```


