# Git 命令的使用场景

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
-   删除某个缓存，使用git stash drop命令，git stash drop stash@{n}
-   git stash clear 删除所有的缓存

