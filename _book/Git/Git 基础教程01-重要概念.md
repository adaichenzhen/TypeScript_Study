## Git 的关键概念

1. 工作区（Working Directory）：本地能看到的目录
2. 版本库（Repository）：也称之为仓库，实际上就是工作区中的 `.git` 目录，版本库中包括很多东西，其中最重要的就是称为 `stage` （或者叫 `index` ）的**暂存区**，还有 `Git` 为我们自动创建的第一个分支 `master` ，以及指向 `master` 的一个指针叫 `HEAD`

## 提交修改的机制

1. git add（添加文件到仓库）将工作区的文件修改添加到暂存区；
2. git commit（提交修改）实际上就是把暂存区的所有内容提交到当前分支；
3. 提交完成后，暂存区就没有任何内容了。

![alt](./images/git_add.jpg)

![alt](./images/git_commit.jpg)

## Git 和 SVN 的区别

+ 版本号：`SVN` 中，版本号为递增的数字（0，1，2，3……），`Git` 中，版本号是一个 `SHA1` 计算出来的一个非常大的数字（十六进制表示，如 842d7d2d8a953c59af1f858a5df20bfe120d823f）
+ 协议：`Git` 支持多种协议，包括 `Https` ，但通过 `SSH` 支持的原生 `Git` 协议速度最快
+ 分支：`SVN` 也有分支管理，但创建、切换和删除分支上，`Git` 的速度更快



参考：[廖雪峰的 Git 教程](https://www.liaoxuefeng.com/wiki/896043488029600)