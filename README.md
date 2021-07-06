# Git 命令的常见使用场景

## 一、不同工作区的撤销更改

### git add 添加代码到暂存区(index)以后的撤销

-   命令：git checkout -- 路径下的文件名

### git commit 已经将代码添加到本地仓库（local Repository）后的撤销

-   命令：git reset -- 路径下的文件

## 二、GitHub 跨团队合作流程跨团队合作场景与合作流程

#### 当一个程序员 B 在浏览 github 上某个陌生作者 A 仓库中代码时，若有一些新的或者有益的想法，可以通过申请的方式对该陌生作者的代码进行修改或者增补。

### 2.1 跨团队合作流程

-   程序员 B 在陌生作者 A 的仓库界面，点击右上角的“Fork”,在程序 B 的仓库中就会生成一个陌生作者 A 项目代码的拷贝
-   程序员 B 发起一个 pull requests 请求
-   陌生作者 A 通过请求
-   程序员 B 克隆、修改、提交、推送代码带自己新生成的仓库，程序 B 所有的提交、对话都会在双方的 github 账号上记录下来
-   陌生者作者 A 待程序员 B 完成后，就可以将程序员 B 的修改代码合并到自己的代码中

### 2.2 团队合作同一个项目场景

#### 当一个项目很大时，就需要多人组成的团队完成。其中一个创建项目仓库后，可以通过邀请的方式，让团队中的其他成员加入，共同完成项目的开发

### 团队合作项目的流程

-   程序员 A 创建远程该项目 B 的远程仓库，然后他将点开 settings，在跳转的页面中，选择“manage access”,此时会经过一次密码填写验证。然后，点击界面中的"invite a collaborator"，将所有会参入开发的其他人员的 github 账号添加进来
-   收到邀请的每个程序员，创建 github 账号的主邮箱都会收到一封邮件。点击“view in inviting”，登录各自的 github 账号，每一位被邀请者都将会在自己的仓库中自动生成一个项目 B 的拷贝仓库
-   程序 A 将仓库连接分享给各位被邀请者，然后这个团队就可以共同开发这个项目了
-   团队中所有成员的提交，都会显示在项目 B 的提交记录中

## 三、GitHub 交互模式,git 交互模式的作用

-   在开发中，常常会遇到在一个分支中，出现许多次无效提交，这种情况下可以使用 rebase 交互模式，把多次无效提交压缩成一次提交，使得提交记录更加整洁
-   命令格式：git rebase -i <base-commit,通常是提交的序列号的前 7 位的字符>。使用命令：git log --oneline 可以直接获得前 7 位的字符。该命令是：git log --pretty=oneline --abbrev-commit 的简写
-   团队中所有成员的提交，都会显示在项目 B 的提交记录中

## 四、起别名（alias）的方式简化命令，提高工作效率

-   全局配置指令的简写方式，可以提高工作效率
-   如：git config --global alias.ci commit
-   如：git config --global alias.ck checkout 等等

## 五、使用 git stash 来暂存文件

### 使用场景

-   当某个程序员在 temp 分支上做开发时，出现一个突发情况。master 分支上的 bug 需要优先完成修复，而程序员手上的 temp 分支代码还没有编写完成，他又不想提交，可以使用 git stash 命令来实现，对 temp 分支文件的暂存(git stash/git stash save "说明文字")。待 master 上分支修复完成后，再切换到 temp 分支上，释放暂存的文件，继续之前的开发

### 暂存文件和释放文件

-   git stash
-   git stash save "说明文字"
-   应用某个存储-git stash apply stash@{n} ,n 从 0 开始取值，可以使用 git stash list 查看列表，然后确定 n 的值。应用这个文件，但是不会主动把该文件从暂存列表中清除，执行 git stash list 命令后可以验证。git stash apply 不跟任何内容，默认将使用 stash@{0}
-   应用某个存储-git stash pop,同时会把该文件从暂存列表中清除
-   删除某个缓存，使用 git stash drop 命令，git stash drop stash@{n}
-   git stash clear 删除所有的缓存

## 六、使用 git revert 回滚某次提交

### 回退版本使用场景

-   你的项目有两个版本要上线，两个版本都还伴随着之前遗留的 bug 修复。你将 bug 修复在了第一个版本的 relese 分支上。突然在发版前一天，测试告知，需要将 bug 修复放在第二个版本上。此时，第一个版本的集成分支上，应当包括了第一个版本的功能内容、bug 修复内容、同事的其他提交。如果粗暴的使用 git reset <commit 提交>回退到某个版本，肯定行不通。而且，这种做法会很危险，会破坏掉一些提交记录，此时就可以使用 git revert 了
-   git revert 操作后，不会修改之前的任何一次提交记录，而是自动新增了一个 Revert 开头的记录

### 回滚多次提交

-   命令：git revert <commit id1> <commit id2>,注意这是一个前开后闭的区间

### 使用场合

-   对于个人的 feature 提交，可以使用 git reset 回滚，然后 git push --force（最好不要使用这种方式，这种推送将会覆盖掉远程主机上更新的版本）提交。但是，对于团队协作，切记不要使用 git reset 的方式，而要使用更加安全的 git revert 的方式
-   git 远程操作详解见：[git 远程操作](http://www.ruanyifeng.com/blog/2014/06/git_remote.html)

## 七、使用 git cherry-pick 获取指定的提交

### cherry-pick 使用场景

-   git cherry-pick 可以理解为“挑拣分支”，与 merge 合并某条分支或者 rebase 变基应用某个分支不同。如果是只需要某次提交，并不想对整个分支进行合并，就可以使用 git cherry-pick 了

### cherry-pick 命令

-   语法：git cherry-pick <commit id1> ，该次提交就会被合并到当前分支上
-   可以进行多次转移提交的操作，比如：git cherry-pick <commit id1> git cherry-pick <commit id2>，执行过程中，如果出现冲突，手动解决后，git add,然后输入 git cherry-pick --continue,当然也可以是 git cherry-pick --abort 放弃合并，回到操作之前的样子，亦或 git cherry-pick --quit,发生冲突后退出 cherry-pick，但回不到之前的样子了
-   也支持一次转移多次提交，git cherry-pick A..B 含义是：转移从 A 的下一个提交开始，到 B 的所有提交。注意；这是前开后闭的区间。如果想包含 A,命令写作：git cherry-pick A^..B
-   参考文档：[git cherry-pick 的使用](https://www.ruanyifeng.com/blog/2020/04/git-cherry-pick.html)

## 八、git rebase 的变基操作

### 使用场景

-   有些时候，我们需要将某个分支保存在另一个分支上，又不想使用 git merge 合并。可以使用变基来实现这一操作

### git rebase 变基使用和案例分析

-   基本语法：假设有两个分支分别为 master、temp,如果需要把 temp 分支引用到 master 上。有两种处理方式：1.留在 master 分支，然后执行 git rebase master temp;2.切换到 temp 分支，输入命令：git rebase master 即可
-   案例 1：[变基的使用实例](https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E5%8F%98%E5%9F%BA)
-   案例 2：[你真的懂变基吗？](https://www.jianshu.com/p/6960811ac89c)
-   案例 3：[Git 由浅入深细说变基](http://www.uml.org.cn/pzgl/201704253.asp)

## 九、git pull 和 git fetch 的区别

# git branch -a 命令查看远程分支+本地分支

-   git fetch 和 git pull 的区别在于，git fetch 只会将远程代码请求过来，而不会自动进行合并。git pull 却是将代码请求过来,而且
    自动合并
-   使用 git fetch 请求分支，然后合并。远程代码请求过来，成为远程分支 origin/temp
-   合并方式：git merge origin/temp 或者 git rebase origin/temp
