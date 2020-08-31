# git 基础知识

## git 对象模型

### SHA

所有用来表示项目历史信息的文件，是通过一个40个字符的{40-digits}的对象名来索引的。每个对象名都是对对象内容SHA1哈希计算得来的，就是说每个不同内容的对象会有不同的对象名，内容相同的对象就算在不同的仓库中，也会有相同的对象名，因为每个仓库的对象名的计算方法是一样的。

### 对象

四种对象类型：blob、tree、commit、tag。每个对象包括3个部分：类型、大小、内容。大小指内容的大小。内容取决于对象的类型。所有对象均用哈希值来表示。

- **blob** 存储文件数据，通常是一个文件。
- **tree** 有点像目录，管理文件和子目录，即“blob”和“tree”。
- **commit** 一个“commit”只指向一个“tree”，用来标记项目某一时间点的状态。包含一些关于时间点的元数据，如时间戳，提交的作者，指向上次提交的{commits}的指针。
- **tag** 一个“tag”是用来标记某一个提交（commit）的方法。

### 1.bolb对象

一个bolb对象通常用来存储文件的内容。

bolb对象没有指向其它任何对象，只是一块二进制数据，甚至连文件名都没有。如果在同一仓库或同一“tree”下的两个文件内容完全相同，那么它们实际共享同一“bolb”对象。bolb对象和其对应文件所在路径，文件名是否被更改没有关系。

使用**git show** 命令可以查看bolb对象的内容。

### 2.tree对象

一个tree对象拥有一串用来指向“tree”和“bolb”的指针，一般用来表示不同内容之间的层次关系。

一条指针指向一个条目，一个条目内容包括：mode值、对象类型、SHA1值和名字。

使用**git show**或**git ls-tree**(详细)都可以查看tree对象。

### 3.commit对象

commit对象指向一个tree对象，并且带有相关的描述信息。

commite对象由一下内容组成：

- tree对象：tree对象的SHA1签名
- 父对象（parent(s)）:提交前一步的项目历史的SHA1签名。若是第一次提交，则为根提交。每个项目都有一个根提交，也可以有多个根提交（不好的做法）。
- 作者（Author）:做此次修改的人的名字，还有修改日期。
- 提交者（committer）：实际创建提交的人的名字，还有提交日期。

ps:一个提交并没有包括任何信息来说明此次提交做了那些修改；所有的修改都是同父提交的内容进行比较而得出的。

一般用**git commit**来创建一个提交，这个提交的父对象一般是当前分支（curren HEAD），同时把存储在当前索引（index）的内容全部提交。

### 4.对象组合

![](C:\Users\gnawgnat\Pictures\git对象组合.png)

![](C:\Users\gnawgnat\Pictures\git对象组合1.png)



### 5.tag对象

一个标签对象包括一个对象名（object）(译者注:就是SHA1签名), 对象类型（type）, 标签名（tag）, 标签创建人的名字(tagger), 还有一条可能包含有签名(signature)的消息. 可以用 git cat-file 命令来查看这些信息。



------

## Git目录与工作目录

### Git目录

Git目录是为你的项目存储所有历史和元信息的目录。包括所有的对象，这些对象指向不同的分支。

每一个项目只能有一个Git目录，即“.git”。这个目录在你项目的根目录下（默认设置，不是必须的）。以下是一些重要文件：

- HEAD #这个git项目当前处在哪个分支里
- config #项目的配置信息，git config命令会改变它
- description #项目的描述信息
- hooks/ #系统默认的脚本目录
- index #索引文件  现在没有了倒是有个branchs/
- logs/ #各个refs的历史信息  现在已经没有了 info/
- objects/ #Git本地仓库中的所有对象（bolbs、trees、commits、tags）
- refs/ #标识你项目里的每个分支指向哪个提交（commit）。

### 工作目录

Git的 '工作目录' 存储着你现在签出(checkout)来用来编辑的文件. 当你在项目的不同分支间切换时, 工作目录里的文件经常会被替换和删除。所有历史信息都保存在 'Git目录'中 ;　工作目录只用来临时保存(checkout) 文件的地方, 你可以编辑工作目录的文件直到下次提交(commit)为止。

### Git索引

Git索引是一个在工作目录和项目仓库之间的暂存区（staging area）。这样可以把许多内容的修改一起提交（commit）。如果创建了一次提交，那么提交的是索引下的内容，而不是工作目录里的内容。

### 查看索引

使用**git status**可以看到那些文件被暂存了，那些文件修改了但未提交，那些文件未被跟踪。



----

## git的安装、配置

### 安装

本地包管理系统安装：`$yum intstall git-core`或`$apt-get install git-core`

### 配置

使用git的第一件事是配置你的name和email，这是你提交时的签名。

`$git config --global user.name "your name"`

`$git config --global user.email "youremail@gmail.com"`

执行上面命令后，会在你的home目录下生成一个.gitconfig文件，内容一般为：

```bash
[user]
		name=your name
		email=youremail@gmail.com
```

上面是全局变量，如果要使用个性化（另外的签名），（在项目下使用命令）可以不加参数`--global`，这样会在该目录下生成.gitconfig文件。



------

## 基本用法

### 1.获得一个git仓库

- **克隆**

git URL：仓库项目的地址能在许多协议下使用，如：ssh://、http(s)://、git://或只是以用户名为前缀（这回认为是ssh）。git://协议快速有效。但是多数情况却是不得不使用http(s)。

目录名：默认将URL最后的‘*.git’去掉，使用\*作为克隆项目的目录名。

- **新建**

将未进行版本控制的文件进行版本控制。

**初始化仓库：**`$ git init`

**修改文件、将修改的内容添加到索引中：**`$ git add file1 file2 file3`

已为commit做好准备

可以使用`$ git diff --cached`看看那些文件将被提交，也可以使用`git status`看看当前项目的状态

**提交索引中的文件：**`$ git commit -m "description about this commit"`

另外，也可以使用`$ git commit -a`添加所有修改过的文件（不包括新建的文件），提交索引目录

*这里有一个关于写commit注释的技巧和大家分享:commit注释最好以一行短句子作为开头，来简要描述一下这次
commit所作的修改(最好不要超过50个字符)；然后空一行再把详细的注释写清楚。这样就可以很方便的用工具把
commit释变成email通知，第一行作为标题，剩下的部分就作email的正文。*



git 跟踪的是内容而不是文件，`$ git add`可以将新建的文件添加到索引中，也可以将修改过但已在版本库中的文件添加到索引，为之后的提交到版本控制库中做准备。

### 2.分支和合并

一个git仓库可以维护很多开发分支。

### 创建新的分支：

`$ git branch experimental`[^1]

**查看项目中所有分支列表：**`$ git branch`

如下：

```bash
$ * master
$   experimental
```

星号“*”标识了当前工作再哪个分支。

**切换分支：**`$ git checkout experimental`

之后各自做不同的修改，所在分支就有不同的版本。



### 合并分支：

`$ git merge experimental`

将experimental这个分支合并到当前分支

如果这两个分支没有冲突（conflict），那么合并就完成了

如果产生了冲突[^2]，用下面的命令查看那些文件产生了冲突：

`$ git diff`

将文件编辑以解决冲突，之后就可以提交了（在解决冲突之前，提交都会出错）

`$ git commit -a`

`$ gitk`执行了此命令后有显示项目的历史的图形（我试过，我没有这个命令）

之后可以删除experimental这个分支了（也可以不用删除）

`git branch -d experimental`

上面这个命令只能删除已经合并了的分支，如果要删除未合并的分支（设为bad_idea）

`$ git branch -D bad_idea`



**撤销一个合并：**`$ git reset --hard HEAD`回到合并前的状态

或者已经将合并后的代码提交，可以使用：

`$ git reset --hard ORGI_HEAD`

但是刚才这条命令在某些情况会很危险，如果你把一个已经被另一个分支合并的分支给删了，那么 以后在合并相
关的分支时会出错。



**快速向前合并：**还有一种需要特殊对待的情况，在前面没有提到。通常，一个合并会产生一个合并提交(commit), 把两个父分支里的每一行内容都合并进来。但是，如果当前的分支和另一个分支没有内容上的差异，就是说当前分支的每一个提交(commit)都已经存在另一个分支里了，git 就会执行一个“快速向前"(fast forward)操作git 不创建任何新的提交(commit),只是将当前分支指向合并进来的分支。



## 显示历史

### git日志

**查看显示所有的提交：**`gti log`

`$ git log v2.5..` # commits since (not reachable from) v2.5
`$ git log test..master`# commits reachable from master but not test
`$ git log master..test` # commits reachable from test but not master
`$ git log master...test` # commits reachable from either test or 
	#_master, but not both
`$ git log --since="2 weeks ago"` # commits from the last 2 weeks
`$ git log Makefile` # commits that modify Makefile
`$ git log fs/` # commits that modify any file under fs/
`$ git log -S'foo()'` # commits that add or remove any file data 
	#_matching the string 'foo()'
`$ git log --no-merges` # don't show merge commits

可以组合上面的命令

git会根据参数按时间顺序显示相关的提交

**显示补丁**（patchs）

`git log -p`

### 日志统计

如果用 --stat 选项使用'git log',它会显示在每个提交(commit)中哪些文件被修改了, 这些文件分别添加或删除了多少行内容.

### 格式化日志

你可以按你的要求来格式化日志输出。‘--pretty'参数可以使用若干表现格式，如‘oneline'，或者你也可以使用 'short' 格式，你也可用‘medium','full','fuller','email' 或‘raw'。如果这些格式不完全符合你的相求， 你也可以用‘--pretty=format'参数(参见：git log)来创建你自己的“格式”。

另一个有趣的事是：你可以用'--graph'选项来可视化你的提交图(commit graph),它会用ASCII字符来画出一个很漂亮的提交历史(commit history)线。

### 日志排序

你也可以把日志记录按一些不同的顺序来显示。注意，git日志从最近的提交(commit)开始，并且从这里开始向它们父分支回溯。然而git历史可能包括多个互不关联的开发线路，这样有时提交(commits)显示出来就有点杂乱。如果你要指定一个特定的顺序，可以为git log命令添加顺序参数(ordering option).按默认情况，提交(commits)会按逆时间(reverse chronological)顺序显示。但是你也可以指定‘--topo-order'参数，这就会让提交(commits)按拓朴顺序来显示(就是子提交在它们的父提交前显示). 如果你用git log命令按拓朴顺序来显示git仓库的提交日志，你会看到“开发线"(development lines)都会集合在一起。













[^1]:experimental 实验性的
[^2]:冲突，即同一文件在远程分支与本地分支里按不同的方式实现了