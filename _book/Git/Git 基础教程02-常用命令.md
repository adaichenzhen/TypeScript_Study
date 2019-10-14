## 命令说明
+ `<>`内的内容为必填项
+ `[]`内的内容为选填项
+ `file`代指具体的文件路径
+ `message`代指具体的说明内容
+ `remoteRepo`代指具体的远程仓库地址
+ `remoteName`代指具体的远程仓库名称
+ `localBranchName`代指具体的本地仓库分支名
+ `remoteBranchName`代指具体的远程仓库分支名
+ `stashName`代指具体的工作现场名
+ `commitId`代指具体的版本号
+ `tagName`代指具体的标签名
+ `...`指可以指定多个（如`file`）
+ `HEAD`表示当前版本，上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`

## 基本用法

| 序号 | 命令内容 | 命令含义 | 备注 |
| :-: | :-: | :-: | :-: |
| 1 | `git init` | 创建版本库 | 执行该命令的目录将变成`Git`可以管理的本地仓库，目录下多的一个`.git`的目录就是`Git`来跟踪并管理版本库的 |
| 2 | `git add <file>...` | 将工作区中的修改文件添加到本地仓库的暂存区中 | 修改文件不仅仅指被修改的文件，也可以指添加的新文件、被删除的文件等 |
| 3 | `git commit -m <message>` | 将暂存区的修改全部提交到本地仓库的当前分支上 | `message`为本次提交添加说明 |
| 4 | `git status` | 查看当前分支的状态 |  |
| 5 | `git diff [file]...` | 查看工作区和仓库暂存区文件内容的修改 | `file`不指定时，将查看所有修改文件 |
| 6 | `git diff HEAD [file]...` | 查看工作区和仓库当前分支文件内容的修改 | `file`不指定时，将查看所有修改文件 |
| 7 | `git log` | 显示最近的提交日志 | 添加参数`--pretty=oneline`可以简化显示内容；添加参数`--graph --pretty=oneline --abbrev-commit`可以查看分支的合并情况 |
| 8 | `git reset --hard <commitId>` | 回退到指定版本（也可以是未来的某个版本） | 版本号（`commitId`）可以用`HEAD`表示，也可以用具体的值表示（值没必要写全，一般写前`7`位即可） |
| 9 | `git reflog` | 查看命令历史 | 常用于确定版本号 |
| 10 | `git checkout -- <file>` | 撤销工作区的修改 | 回退到最后一次`git add`或`git commit`后的状态 |
| 11 | `git reset HEAD <file>` | 撤销暂存区的修改 | 将暂存区的修改撤销掉，重新放回工作区 |
| 12 | `git rm <file>` | 删除文件 | 用于将删除的文件添加到暂存区，使用`git add <file>`也可以达到同样的效果 |
| 13 | `git rebase` | 把本地未推送的分叉提交历史整理成直线 |  |

## 与远程仓库的此操作

| 序号 | 命令内容 | 命令含义 | 备注 |
| :-: | :-: | :-: | :-: |
| 1 | `git remote add origin <remoteRepo>` | 将一个已有的本地仓库与远程仓库关联 | 此时本地仓库的分支并未与远程仓库的分支关联 |
| 2 | `git remote [-v]` | 查看远程仓库信息 | 添加`-v`参数可以显示详细信息 |
| 3 | `git remote rename <old> <new>` | 修改远程仓库的名称 | 远程仓库的默认名称为`origin` |
| 4 | `git push [-u] [remoteName] [localBranchName]` | 将本地仓库的指定分支推送到指定远程仓库的关联分支上 | 执行推送操作的前提是，本地仓库的指定分支与远程仓库的某个分支已关联，如果没有关联，可以通过在 push 后添加 -u 参数进行首次关联和推送 |
| 5 | `git branch --set-upstream-to=<remoteName>/<remoteBranchName> <localBranchName>` | 将本地仓库的指定分支与远程库的指定分支进行关联 | 提示信息：`no tracking information` |
| 6 | `git clone <remoteRepo>` | 将远程仓库的默认分支克隆到本地 | 本地将创建相同名称的仓库和分支；默认分支一般是`master`分支 |
| 7 | `git clone -b <remoteBranchName> <remoteRepo>` | 直接将远程仓库的的指定分支克隆到本地 | 本地将只有一个与指定分支同名的分支 |
| 8 | `git checkout -b <localBranchName> <remoteName>/<remoteBranchName>` | 创建远程库的指定分支到本地 | 也可以说，本地创建一个分支，并将该分支与远程库的指定分支进行关联 |
| 9 | `git pull` | 抓取远程库的关联分支的最新提交并合并到本地的当前分支 |  |

## 分支管理

| 序号 | 命令内容 | 命令含义 | 备注 |
| :-: | :-: | :-: | :-: |
| 1 | `git branch <localBranchName>` | 创建分支 |  |
| 2 | `git checkout <localBranchName>` | 切换分支 |  |
| 3 | `git checkout -b <localBranchName>` | 创建并切换分支 |  |
| 4 | `git branch [-v]` | 显示本地所有分支 | 当前分支会标一个`*`号；添加`-v`参数表示显示分支的最新提交信息 |
| 5 | `git branch -a` | 显示本地和远程库的所有分支 |  |
| 6 | `git branch -vv` | 显示本地所有分支及对应远程库的关联分支 |  |
| 7 | `git merge <localBranchName>` | 将指定分支合并到当前分支 |  |
| 8 | `git branch -d <localBranchName>` | 删除分支 |  |
| 9 | `git branch -D <localBranchName>` | 强制删除分支 |  |
| 10 | `git stash` | 将当前工作现场“储藏”起来 |  |
| 11 | `git stash list` | 显示存储的工作现场（stash 内容） |  |
| 12 | `git stash apply [stashName]` | 恢复指定工作现场 | 恢复后，`stash`内容并不删除 |
| 13 | `git stash drop` | 删除`stash`内容 |  |
| 14 | `git stash pop [stashName]` | 恢复现场的同时将删除 stash 内容 |  |
| 15 | `git cherry-pick <commitId>` | 复制一个特定的提交到当前分支 | 使用场景：在`master`分支上修复的`bug`，想要合并到当前`dev`分支 |

## 标签管理

> 标签的作用主要就是方便提交的历史版本的提取；创建一个标签指向某一个版本号，后续需要取该版本，就可以直接通过标签去取；标签和分支一样都是指向某个版本号的指针，但分支可以移动，标签不能移动。

| 序号 | 命令内容 | 命令含义 | 备注 |
| :-: | :-: | :-: | :-: |
| 1 | `git tag <tagName> [commitId]` | 创建标签 | 版本号不指定时，标签将打在当前分支最新提交的版本号上的；创建的标签都只存储在本地，不会自动推送到远程 |
| 2 | `git tag -a <tagName> -m <"message"> <commit-id>` | 创建带有说明的标签 | `-a`指定标签名，`-m`指定说明内容 |
| 3 | `git tag` | 查看所有标签 | 标签不是按时间顺序列出，而是按字母排序的 |
| 4 | `git show <tagName>` | 查看标签信息 | 标签总是和某个版本号挂钩。如果这个版本号同时出现在多个分支上，那么在这几个分支上都可以看到这个标签 |
| 5 | `git tag -d <tagName>` | 删除标签 |  |
| 6 | `git push <remoteName> <tagName>` | 推送某个标签到远程 |  |
| 7 | `git push <remoteName> --tags` | 一次性推送所有尚未推送到远程的本地标签 |  |
| 8 | `git push origin :refs/tags/<tagName>` | 删除远程标签 | 前提：本地对应标签已删除 |


参考：[廖雪峰的 Git 教程](https://www.liaoxuefeng.com/wiki/896043488029600)