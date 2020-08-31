# 一个主机登录两个git账户

**相关描述：**

<font color=green>ERROR: Permission to count_B/repo1.git denied to count_A.</font>

<font color=green>fatal: Could not read from remote repository.</font>

<font color=green>Please make sure you have the correct access rights and the repository exists.</font> 



**原因：**

一台电脑上已经有了一个公钥，这个公钥和账户A配对，使用这个公钥可以登录账户A。但是，当你想要把本地仓库推送到账户B中时，却不能推送（push）成功。这是因为你的公钥是和账户A配对的，登录远程仓库时，就是用自己的私钥去配对公钥，而此时公钥却和账户A配对了，自然不能登录账户B的远程仓库。所幸一台主机可以拥有多个私钥从而配对多个git账户。



**解决方法：**

1. 生成新的ssh key。生成ssh key的命令是`$ ssh-keygen -t rsa -C "your email"`。将其保存在某一目录下（默认是\~/.ssh/id_rsa，但是已经被前一账户占用，就另起炉灶，如：~/.ssh/id_rsa_countB）。
2. 将\~/.ssh/id_rsa_countB.pub文件内容复制到Github后台（去掉后面的邮箱地址）。
3. 打开（没有的话就创建）\~/.ssh/config文件。建一个账户B的github别名，以区分账户A。

``` shell
  #Default GitHub
  Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa
  
  #New GitHub
  Host github_other
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_countB
```

4. 将GitHub ssh仓库地址中的git@github.com替换成新建的别名。使用`$ git remote -v`查看原地址。使用`$ git remote set-url origin(default repository name) (git@)github_other:countB/repo1.git`修改地址，之后再次使用`$ git remote -v`查看是否更改成功。
5. 使用`$ ssh -T git@github`还是原来的账户，使用`$ ssh -T github_other`就是另一账户了。
6. 之后的push，fetch操作都应正常。

**如果github账户还是显示之前的id_rsa密钥账户的话，就把你的密钥加入sshAgent代理中**

`eval "$(ssh-agent -s)"`