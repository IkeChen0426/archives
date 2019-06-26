# git 教程 #

[git教程](https://learngitbranching.js.org/)

## git init ##

初始化一个Git仓库。

## git add ${file} ##

把文件添加到暂存区。

## git status ##

哪些文件被修改过。

## git diff ${file} ##

可以查看修改内容。

## git Commit ##

提交暂存区的修改。

### git commit -m ${message} ###

提交仓库时添加的备注信息。

## git log ##

从最近到最远的提交日志。

git log --graph  命令可以看到分支合并图

## git reset ##

git reset HEAD~1 ===>（等价于） git reset --hard HEAD^   取消上一次提交

git revert 撤销远程库提交，恢复上次提交记录

## git branch ##

git branch  命令会列出所有分支，当前分支前面会标一个*号

git branch ${分支名}  创建分支

git branch -d ${分支名}  删除分支

git branch -D ${分支名}  强行删除分支（未合并的分支）

git branch --set-upstream-to=origin/dev dev  指定本地dev分支与远程origin/dev分支的链接

git branch -f master HEAD~3  会将 master 分支强制指向 HEAD 的第 3 级父提交

git branch -u origin/master foo   这样 foo 就会跟踪 origin/master 了。如果当前就在 foo 分支上, 还可以省略 foo： git branch -u origin/master

## git checkout ##

git checkout -- ${file}  让这个文件回到最近一次git commit或git add时的状态。

git checkout ${分支名}  切换分支

git checkout ${哈希值}  将HEAD指向提交记录哈希值（在git中移动）

git checkout -b ${your-branch-name}  创建并切换分支

git checkout -b dev origin/dev  创建远程origin的dev分支到本地

git checkout master^  相对引用，切换到master的父节点

git checkout -b totallyNotMaster origin/master  就可以创建一个名为 totallyNotMaster 的分支，它跟踪远程分支 origin/master。

## git remote ##

查看远程库的信息

git remote -v  查看远程库更加详细的信息

### git remote add origin ###

添加远程库。

## git push ##

git push  负责将你的变更上传到指定的远程仓库，并在远程仓库上合并你的新提交记录。

git push origin master   切到本地仓库中的master分支，获取所有的提交，再到远程仓库origin中找到master分支，将远程仓库中没有的提交记录都添加上去。

git push origin dev  将dev分支推送到远程库对应的远程分支上

### git push -u origin master ###

第一次推送master分支的所有内容。之后提交就可以用 git push origin master

## git merge ##

git merge ${分支名}  需要先通过 git checkout master 切换到主分支，再通过git merge ${分支名} 将该分支合并到主分支

git merge --no-ff -m "merge with no-ff" dev   --no-ff参数，表示禁用Fast forward（合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息，如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit）。

## git rebase ##

git rebase ${目标分支} ${将某个分支}  合并分支

git rebase -i HEAD~4  ui界面调整最近4次的提交记录

## git cherry-pick ##

git cherry-pick <提交号>...   如果你想将一些提交复制到当前所在的位置（HEAD）下面的话， Cherry-pick 是最直接的方式了。

## git tag ##

永久地将某个特定的提交命名为里程碑，然后就可以像分支一样引用了，git tag 查看所有标签

git tag v1  在当前分支上面加上标签v1

git tag v1 ${commit id}  我们将这个标签命名为 v1，并且明确地让它指向提交记录 ${commit id}，如果你不指定提交记录，Git 会用 HEAD 所指向的位置。

git tag -a v0.1 -m "version 0.1 released" 1094adb   创建带有说明的标签，用-a指定标签名，-m指定说明文字

git show v1  查看标签信息

git tag -d v0.1  删除标签

git push origin v1  将tag推送到远程库

git push origin --tags  一次性推送全部尚未推送到远程的本地标签

git push origin :refs/tags/${tagname}  可以删除一个远程标签。

## git describe ##

git describe   由于标签在代码库中起着“锚点”的作用，Git 还为此专门设计了一个命令用来描述离你最近的锚点（也就是标签），它就是 git describe！

git describe ${ref}   ${ref} 可以是任何能被 Git 识别成提交记录的引用，如果你没有指定的话，Git 会以你目前所检出的位置（HEAD）。

## git bisect ##

git bisect  一个查找产生 Bug 的提交记录的指令

## git fetch ##

git fetch 完成了仅有的但是很重要的两步:

1. 从远程仓库下载本地仓库中缺失的提交记录
2. 更新远程分支指针(如 origin/master)

git fetch 实际上将本地仓库中的远程分支更新成了远程仓库相应分支最新的状态。

## git pull ##

git pull ===>（等价于） git fetch; git merge origin/master

git pull --rebase  ===>（等价于） git fetch; git rebase origin/master

## git stash ##

把当前工作现场储藏起来，等以后恢复现场后继续工作。

git stash list  所有储藏起来的工作现场。

恢复stash，有两个办法：

一是用git stash apply恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除；

另一种方式是用git stash pop，恢复的同时把stash内容也删了

多人协作的工作模式通常是这样：

1. 首先，可以试图用git push origin ${branch-name} 推送自己的修改；
2. 如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
3. 如果合并有冲突，则解决冲突，并在本地提交；
4. 没有冲突或者解决掉冲突后，再用git push origin ${branch-name}推送就能成功！

**.gitignore** 文件，把要忽略的文件名填进去，Git就会自动忽略这些文件。


##分支共有5种类型

 1. master，最终发布版本，整个项目中有且只有一个

 2. develop，项目的开发分支，原则上项目中有且只有一个 　　

 3. feature，功能分支，用于开发一个新的功能

 4. release，预发布版本，介于develop和master之间的一个版本，主要用于测试

 5. hotfix，修复补丁，用于修复master上的bug，直接作用于master

## Git工作流程
## Git工作流程演示
### 克隆项目到本地
起初本地文件夹 ../test1 为空，如下：

克隆远程代码到此文件夹：

    git clone https://gitee.com/shadage/product-service.git

### 切换到dev分支开发
1）git branch -a 查看所有分支：

    D:\test1\product-service>git branch -a
    * master
      remotes/origin/HEAD -> origin/master
      remotes/origin/master

2）git fetch 同步远程分支到本地：

    D:\test1\product-service>git fetch
    From https://gitee.com/shadage/product-service
     * [new branch]      develop    -> origin/develop

3）git checkout 切换分支：

    D:\test1\product-service>git checkout develop
    Switched to a new branch 'develop'
    Branch 'develop' set up to track remote branch 'develop' from 'origin'.

4）git checkout -b feature develop 基于 develop 创建 feature 分支：

    D:\test1\product-service>git checkout -b feature develop
    Switched to a new branch 'feature'

5）git status 查看当前分支状态

    D:\test1\product-service>git status
    On branch feature
    nothing to commit, working tree clean


### 本地开发
### 提交本地开发的代码
1）git status 查看本地代码状态：

    D:\test1\product-service>git status
    On branch feature
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
    
            test.txt
    
    nothing added to commit but untracked files present (use "git add" to track)

2）git add 添加本地修改到 Stage：

    git add .

3）git status 查看当前状态：

    D:\test1\product-service>git status
    On branch feature
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)
    
            new file:   test.txt

4）git commit 提交到 develop 分支上：
    
    D:\test1\product-service>git commit -m '添加一个文件'
    [feature eb1c9b5] '添加一个文件'
     1 file changed, 1 insertion(+)
     create mode 100644 test.txt

5）git status 查看当前状态：

    D:\test1\product-service>git status
    On branch feature
    nothing to commit, working tree clean


### 提交本地代码到远程仓库
1）git checkout develop 切换到 develop 分支上

    D:\test1\product-service>git checkout develop
    Switched to branch 'develop'
    Your branch is up to date with 'origin/develop'.

2）git pull 拉取 develop 分支的最新代码（若有冲突则解决后 commit）

    D:\test1\product-service>git pull --rebase
    Already up to date.

3）git merge --no-ff 把 feature 代码合并到 develop 分支上（若有冲突则解决后 commit） 

    D:\test1\product-service>git merge --no-ff -m "feature合并到develop分支" feature
    Merge made by the 'recursive' strategy.
     test.txt | 1 +
     1 file changed, 1 insertion(+)
     create mode 100644 test.txt

4）git push 推送当前本地分支代码到远程分支

    D:\test1\product-service>git push
    Enumerating objects: 5, done.
    Counting objects: 100% (5/5), done.
    Delta compression using up to 6 threads.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (4/4), 377 bytes | 377.00 KiB/s, done.
    Total 4 (delta 2), reused 0 (delta 0)
    remote: Powered by Gitee.com
    To https://gitee.com/shadage/product-service.git
       afd57db..87caeb9  develop -> develop

## 分支管理规范
### 分支操作注意事项
1）同一分支 git pull 使用 [rebase]

    git pull --rebase

默认的 git pull 行为是 merge，可以进行如下设置修改默认的 git pull 行为：

    #为某个分支单独设置，这里是设置 develop 分支
    git config branch.develop.rebase true
    #全局设置，所有的分支 git pull 均使用 --rebase
    git config --global pull.rebase true
    git config --global branch.autoSetupRebase always

2) 分支合并使用 --no-ff

    # 例如当前在 develop 分支，需要合并 feature 分支
    git merge --no-ff feature

3) git stash
我们有时会遇到这样的情况，正在 develop 分支开发新功能，做到一半时有人过来反馈一个 bug，让马上解决，但是新功能做到了一半你又不想提交，这时就可以使用 git stash 命令先把当前进度保存起来，然后切换到另一个分支去修改 bug，修改完提交后，再切回 develop 分支，使用 git stash pop 来恢复之前的进度继续开发新功能。

    # 保存当前工作进度，会把暂存区和工作区的改动保存起来。
    git stash save 'message...'
    # 显示保存进度的列表。也就意味着，git stash命令可以多次执行。
    git stash list
    # 恢复进度到指定的工作区
    git stash pop [index]
    # 删除所有存储的进度
    git stash clear
    

### 分支说明和操作
1) master 分支
master 永远处于稳定状态，这个分支代码可以随时用来部署。不允许在该分支直接提交代码。

2) develop 分支
开发分支，包含了项目最新的功能和代码，所有开发都依赖 develop 分支进行。
小的改动可以直接在 develop 分支进行，改动较多时切出新的 feature 分支进行。

3) feature 分支
功能分支，开发新功能的分支。
开发新的功能或者改动较大的调整，从 develop 分支切换出 feature 分支，分支名称为 feature/xxx ，如果该功能只是某个模块的，分支名称添加模块名，例如  feature/puma/product。
开发完成后合并回 develop 分支并且删除这个 feature 分支，相应的操作如下：

    # 切出新的 feature/xxx 分支
    git checkout -b feature/xxx develop
    # 写代码，提交，写代码，提交
    # feature 开发完成，合并回 develop
    git checkout develop
    # 务必加上 --no-ff，以保持分支的合并历史
    git merge --no-ff feature/xxx
    git branch -d feature/xxx

如果想要当前分支能保持与 develop 的更新，请用 rebase，操作如下：

    # 假设当前在 feature/xxx 分支
    git rebase develop
    # rebase 过程中出现冲突，请按照提示进行操作

rebase 会修改历史，如果你的 feature 分支是跟人合作开发的或者已经提交到远端，请互相做好协调。

4）hotfix 分支
紧急修复线上 bug 分支。
如果我们发现线上的代码（也就是 master）有 bug，但是这个时候我们的 develop 上的有些功能还没完成，还不能发布，这个时候我们可以从 master 分支上开出一个 hotfix 分支（记住：直接在 master 上提交代码是不允许的！），分支名约定为hotfix/xxx，在这个分支上修改完 bug 后需要把这个分支同时合并到 master 和 develop 分支。相应操作如下：

    git checkout -b hotfix/xxx master
    # 修完 bug 后
    git checkout master
    git merge --no-ff hotfix/xxx
    git checkout develop
    git merge --no-ff hotfix/xxx
    # hotfix 分支完成使命
    git branch -d hotfix/xxx

### 分支管理

### 项目分支操作流程示例
1）切到 develop 分支，更新 develop 最新代码

    git checkout develop
    git pull --rebase

新建 feature 分支，开发新功能

    git checkout -b feature/train/crn
    
    ... 
    git add .
    git commit -m "feat(rob): 抢票详情页改成 CRN 页面"
    # 其他提交
    ...

2）完成 feature 分支，合并到 develop 分支

    # 切到 develop 分支，更新下代码
    git check develop
    git pull --rebase 
    
    # 合并 feature 分支
    git merge --no-ff feature/train/crn
    
    # 删除 feature 分支
    git branch -d feature/train/crn
    
    # 推到远端
    git push origin develop

3）准备发布新版本

    # master 分支合并 develop 分支并添加 tag
    git checkout master
    git merge --no-ff develop
    # 添加版本标记，这里可以使用版本发布日期或者具体的版本号
    git tag 20180826

至此，一个新版本发布完成。

### 提交信息规范
git commit 格式：<type>(<scope>): <subject>
1) type 类型，提交的类别

* feat: 新功能
* fix: 修复 bug
* docs: 文档变动
* style: 格式调整，对代码实际运行没有改动，例如添加空行、格式化等
* refactor: bug 修复和添加新功能之外的代码改动
* perf: 提升性能的改动
* test: 添加或修正测试代码
* chore: 构建过程或辅助工具和库（如文档生成）的更改

2) scope 修改范围 主要是这次修改涉及到的部分，简单概括，例如 login、order

3) subject 修改的描述,具体的修改描述信息

4) 范例：

    feat(order-detail): 订单详情页添加 AB 测试
    fix(login): 登录页面错误处理
    test(crn): CRN 添加测试代码


**友情链接：**

[git图像化工具][1]
[学习git指令][2]
[廖雪峰官方网站-Git教程][3]
[Git官网教程][4]


  [1]: https://www.cnblogs.com/tian-xie/p/6264104.html
  [2]: https://learngitbranching.js.org/
  [3]: https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000
  [4]: https://git-scm.com/book/en/v2