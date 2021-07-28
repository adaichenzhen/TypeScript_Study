## SSH Key 的创建

> SSH Key 与计算机的用户一一对应，同一个计算机上的不同用户拥有不同的 SSH Key ，不同计算机的用户的 SSH Key 也不相同

#### 查看是否创建
在用户主目录下，看看有没有`.ssh`目录，如果有，再看看这个目录下有没有`id_rsa`和`id_rsa.pub`这两个文件，如果已经有了，就说明已经创建了

#### 创建命令
创建时需要指定用户的邮件地址
```
ssh-keygen -t rsa -C "youremail@example.com"
```

## SSH Key 的关联

> `id_rsa`和`id_rsa.pub`这两个文件就是SSH Key的秘钥对
> 
> `id_rsa`是私钥，不能泄露出去
> 
> `id_rsa.pub`是公钥，可以放心地告诉任何人

将自己的 SSH 公钥（即`id_rsa.pub`文件的内容）作为`Key`值提供给相应的平台（如`GitHub`、`Gitee`）即可完成关联