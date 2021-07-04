# GitHub的两个合作使用场景
## GitHub跨团队合作流程
### 跨团队合作场景
#### 当一个程序员B在浏览github上某个陌生作者A仓库中代码时，若有一些新的或者有益的想法，可以通过申请的方式对该陌生作者的代码进行修改或者增补。
### 跨团队合作流程
- 程序员B 在陌生作者A的仓库界面，点击右上角的“Fork”,在程序B的仓库中就会生成一个陌生作者A项目代码的拷贝
- 程序员B发起一个 pull requests 请求
- 陌生作者A通过请求
- 程序员B克隆、修改、提交、推送代码带自己新生成的仓库，程序B所有的提交、对话都会在双方的github账号上记录下来
- 陌生者作者A待程序员B完成后，就可以将程序员B的修改代码合并到自己的代码中
## 团队合作开发一个项目
### 团队合作同一个项目场景
#### 当一个项目很大时，就需要多人组成的团队完成。其中一个创建项目仓库后，可以通过邀请的方式，让团队中的其他成员加入，共同完成项目的开发
### 团队合作项目的流程
- 程序员A创建远程该项目B的远程仓库，然后他将点开settings，在跳转的页面中，选择“manage access”,此时会经过一次密码填写验证。然后，点击界面中的"invite a collaborator"，将所有会参入开发的其他人员的github账号添加进来
- 收到邀请的每个程序员，创建github账号的主邮箱都会收到一封邮件。点击“view in inviting”，登录各自的github账号，每一位被邀请者都将会在自己的仓库中自动生成一个项目B的拷贝仓库
- 程序A将仓库连接分享给各位被邀请者，然后这个团队就可以共同开发这个项目了
- 团队中所有成员的提交，都会显示在项目B的提交记录中
# GitHub交互模式
## git交互模式的作用
- 在开发中，常常会遇到在一个分支中，出现许多次无效提交，这种情况下可以使用rebase交互模式，把多次提交压缩成一次提交，使得提交记录更加整洁
- 命令格式：git  rebase -i <base-commit,通常是提交的序列号的前7位的字符>。使用命令：git  log --oneline可以直接获得前7位的字符。该命令是：git log --pretty=oneline --abbrev-commit 的简写

