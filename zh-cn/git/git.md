# git的基本使用流程
# git的快速使用
## 1、git常用命令速查表
![](../../images/git/git.jpg 'git命令')

## 2、Git的配置
```shell
# 显示当前的Git配置
$ git config --list

#设置用户名和邮箱，即提交代码时的用户信息
$ git config [--global] user.name "[name]"
$ git config [--global] user.email "[email address]"
```
## 3、添加/删除文件(到暂存区，即add操作）
```shell
#可以添加一个或多个
$ git add <file1> <file2>...

#添加所有修改的和新添加的
$ git add .
#另一种写法
$ git add -A

#添加指定目录
$ git add <dirname>

#由暂存区恢复到工作区（发现提交错了，退回一步）
$ git reset HEAD <file>

#恢复上一次add提交的所有file
$ git reset HEAD

#撤销修改操作，恢复到修改之前的，撤销add后位于工作区下进行的
$ git checkout -- <file>

#删除文件,并将文件放入暂存区
$ git rm <file1> <file2>
#改文件名，并将修改后的文件放入暂存区
$ git mv <file-original> <file-rename>
```

## 4、提交到本地仓库（commit操作）
```shell
#提交暂存区的所有文件(后面的message不可缺少)
$ git commit -m <message>
#提交暂存区的指定文件
$ git commit <file1> <file2> -m <message>
```
## 5、分支操作（branch）
```shell
# 列出所有本地分支
$ git branch

# 列出所有远程分支
$ git branch -r

# 列出所有本地分支和远程分支
$ git branch -a

# 新建一个分支，并切换到该分支
$ git checkout -b [branch]

# 切换到指定分支，并更新工作区
$ git checkout [branch-name]

#从远程分支检出指定分支
$ git clone -b <branchname> <master>

# 合并指定分支到当前分支（主分支合并自定义分支）
$ git merge [branch]

# 删除分支
$ git branch -d [branch-name]

# 删除远程分支
$ git push origin --delete [branch-name]
$ git branch -dr [remote/branch]
```
## 6、查看信息：
```shell
# 显示有变更的文件
$ git status

# 显示当前分支的版本历史
$ git log
```
## 7、.gitignore的配置
>缘由：当我们导入一个git项目时，开发环境会改变里面的一些配置，当我们修改完代码后，add，commit操作后，系统更改的配置信息，并不想去提交，这个时候就会用到这个配置，配置完成后，才更好的去add .和commit -m去操作。
用法规则和语义：

```shell
# 此为注释 – 将被 Git 忽略
*.a       # 忽略所有 .a 结尾的文件
!lib.a    # 但 lib.a 除外
/TODO     # 仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO
build/    # 忽略 build/ 目录下的所有文件
doc/*.txt # 会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
```


>一般我们总会有些文件无需纳入 Git 的管理，也不希望它们总出现在未跟踪文件列表。 通常都是些自动生成的文件，比如日志文件，或者编译过程中创建的临时文件等。 在这种情况下，我们可以创建一个名为 .gitignore 的文件，列出要忽略的文件模式。 来看一个实际的例子：

```shell
$ cat .gitignore
*.[oa]
*~
```
第一行告诉 Git 忽略所有以 .o 或 .a 结尾的文件。一般这类对象文件和存档文件都是编译过程中出现的。 <br>
第二行告诉 Git 忽略所有以波浪符(~)结尾的文件，许多文本编辑软件(比如 Emacs)都用这样的文件名保存副本。 此外，你可能还需要忽略 log，tmp 或者 pid 目录，以及自动生成的文档等等。 要养成一开始就设置好 .gitignore 文件的习惯，以免将来误提交这类无用的文件。

>文件 .gitignore 的格式规范如下：<br>
    所有空行或者以 ＃ 开头的行都会被 Git 忽略。<br>
    可以使用标准的 glob 模式匹配。<br>
    匹配模式可以以(/)开头防止递归。<br>
    匹配模式可以以(/)结尾指定目录。<br>
    要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号(!)取反。<br>



## 8、从现有的git仓库中克隆下来
>当你执行 git clone 命令的时候，默认配置下远程 Git 仓库中的每一个文件的每一个版本都将被拉取下来。如果服务器的磁盘坏掉了，通常可以使用任何一个克隆下来的用户端来重建服务器上的仓库。

```shell
$ git clone [仓库地址]
```
如果想在克隆远程仓库的时候，自定义本地仓库的名字，可以使用如下命令：
```shell
$ git clone [仓库地址] [自定义名称]
```

## 9、从现有的目录中初始化仓库
>如果不克隆现有的仓库，而是打算使用 Git 来对现有的项目进行管理。只需要进入该项目的根目录执行命令如下：

```shell
$ git init
```
>该命令将创建一个名为 .git 的子目录，这个子目录含有初始化的 Git 仓库中所有的必须文件，这些文件是 Git 仓库的骨干。 <br>
>但是，在这个时候，我们仅仅是做了一个初始化的操作，项目里的文件还没有被跟踪。<br>
>如果是在一个已经存在文件的文件夹(而不是空文件夹)中初始化 Git 仓库来进行版本控制的话，应该开始跟踪这些文件并提交。<br>
>可通过 git add 命令来实现对指定文件的跟踪，<br>
>然后执行 git commit 提交

```shell
$ git add [文件名]
$ git commit -m '提交的修改内容描述'
```

## 10、本地仓库和远程的空仓库关联，并推送到远程仓库上

```shell
# 关联远程仓库
$ git remote add origin [远程仓库的地址]
# 推送到远程仓库
$ git push -u origin master

```

```shell
#修改远程仓库地址
    先删后加

 git remote rm origin
 git remote add origin [url]

```
## 11、分支合并

```shell
git merge [别的分支名字]
```

## 12、删除分支
```shell
$ git branch -d [分支名字]
```




# 常用的命令

    查看分支：git branch

    创建分支：git branch <name>

    切换分支：git checkout <name>

    创建+切换分支：git checkout -b <name>

    合并某分支到当前分支：git merge <name>

    删除分支：git branch -d <name>