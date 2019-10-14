## 为什么需要分支

问题情景：开发人员在开发一个新功能，需要两天完成，第一天完成 50%，如果当天提交，由于代码还没写完，不完整的代码库会导致别人不能干活了。如果等代码全部写完再一次提交，又存在丢失第一天进度的巨大风险。

解决方案：创建了一个属于你自己的分支，别人看不到，别人可以继续在原来的分支上正常工作，而你在自己的分支上干活，想提交就提交，直到开发完毕后，再一次性合并到原来的分支上。

## Git 分支的生命周期

>我们知道，每次提交，`Git`都把它们（提交）串成一条时间线，这条时间线就是一个分支。最开始只有一条时间线，在`Git`里，这个分支叫主分支，即`master`分支。`HEAD`严格来说不是指向提交，而是指向`master`，`master`才是指向提交的，所以，`HEAD`指向的就是当前分支。

#### 初始化后
一开始的时候，`master`分支是一条线，`Git`用`master`指向最新的提交，再用`HEAD`指向`master`，从而`Git`通过`HEAD`就能确定当前分支，以及当前分支的提交点。每次提交，`master`分支都会向前移动一步，这样，随着你不断提交，`master`分支的线也越来越长。

![alt](./images/after_init.png)

#### 创建并切换到新分支

当我们创建新的分支，例如`dev`时，`Git`新建了一个指针叫`dev`，指向`master`相同的提交，再把`HEAD`指向`dev`，就表示当前分支在`dev`上（切换分支）。在`Git`中创建一个分支很快，因为除了增加一个`dev`指针（创建新分支），改改`HEAD`的指向（切换到新分支），工作区的文件都没有任何变化！

![alt](./images/new_branch.png)

#### 新分支上提交
不过，从现在开始，对工作区的修改和提交就是针对dev分支了，比如新提交一次后， `dev`指针往前移动一步，而`master`指针不变。

![alt](./images/new_branch_commit.png)

#### 合并分支

假如我们在`dev`上的工作完成了，就可以把`dev`合并到`master`上。Git 怎么合并呢？最简单的方法，就是直接把`master`指向`dev`的当前提交，就完成了合并。所以`Git`合并分支也很快！就改改指针，工作区内容也不变！

![alt](./images/merge_branch_01.png)

#### 删除分支

合并完分支后，可以删除`dev`分支。删除`dev`分支就是把`dev`指针给删掉，删掉后，我们就剩下了一条`master`分支：

![alt](./images/delete_branch.png)



## Git 分支的合并
#### 情景1
在`master`分支上，创建并切换到新的分支`dev`，在`dev`分支做了修改并提交后，又切换回到`master`分支，如何在`master`分支上合并`dev`分支？

![alt](./images/new_branch_commit.png)

解决方案：直接使用`git merge dev`命令将`dev`分支合并到`master`分支（当前分支）上，此时采用的是一种`Fast-forward`（快进模式）的合并方式，也就是直接将`master`指向 `dev`的当前提交。

![alt](./images/merge_branch_01.png)


#### 情景2
`Git`用`Fast forward`模式合并分支后，如果删除分支，会丢掉分支信息，如何保留分支信息？

![alt](./images/delete_branch.png)

解决方案：强制禁用`Fast forward`模式（参数`--no-ff`），此时`Git`就会在合并时生成一个新的提交，这样，从分支历史上就可以看出分支信息。强制禁用`Fast forward`模式的命令`git merge --no-ff -m "merge with no-ff" dev`。

![alt](./images/merge_branch_02.png)


#### 情景3
在`master`分支创建并切换到新的分支`dev`，在`dev`分支做了修改并提交，然后切换回到`master`分支，在`master`分支上也做了修改并提交（且修改的内容与在 `dev`分支修改的内容发生冲突），如何合并分支？

![alt](./images/git_conflict.png)

解决方案：如果直接使用`git merge dev`命令，`Git`将报告文件存在冲突，此时必须手动解决冲突后再提交。

![alt](./images/git_conflict_solve.png)


#### 情景4
当前正在 `dev`分支上工作，但工作还未完成，无法提交，但同时需要修复另外一个新的 bug，怎么办？

解决方案：将当前`dev`分支（有修改当没有提交）的工作现场储藏起来，等以后恢复现场后再继续工作

## 分支策略
+ `master`分支：`master`分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活
+ `dev`分支：干活都在`dev`分支上，比如1.0版本发布时，再把`dev`分支合并到`master`上，在`master`分支发布1.0版本
+ `bug`分支：`bug`分支常用于修复某一个 Bug，
+ `feature`分支：`feature`分支常用于开发某一个新功能

![alt](./images/branch_types.png)

参考：[廖雪峰的 Git 教程](https://www.liaoxuefeng.com/wiki/896043488029600)