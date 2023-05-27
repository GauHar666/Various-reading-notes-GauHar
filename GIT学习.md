# GIT学习

## 版本控制

每次都会有版本迭代，希望有个版本管理器。简单说就是用于管理多人协同开发项目的技术。

常见的版本控制工具：

- git
- SVN 

git和SVN的区别：

将所有数据放在服务器上，本地用户只有自己以前同步的版本，不联网就看不到。这就是SVN，集中式的版本控制。



**git是分布式的版本控制**

![image-20230324153605507](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230324153605507.png)

每个电脑上都有自己的控制中心。

每个人都拥有全部代码。



SVN是集中式版本控制系统，**版本库是集中放在中央服务器的，**而工作的时候，用的都是自己的电脑，所以首先要从中央服务器得到最新的版本，然后工作，完成工作后，需要把自己做完的活推送到中央服务器。集中式版本控制系统是**必须联网**才能工作，对网络带宽要求较高。

Git是分布式版本控制系统，**没有中央服务器**，每个人的电脑就是一个完整的版本库，工作的时候不需要联网了，因为版本都在自己电脑上。协同的方法是这样的：比如说自己在电脑上改了文件A，其他人也在电脑上改了文件A，这时，你们两之间只需把**各自的修改推送给对方，就可以互相看到对方的修改了。Git可以直接看到更新了哪些代码和文件！**



## git的配置

查看不同级别的配置文件

```cpp

#查看系统config
git config --system --list
　　
#查看当前用户（global）配置
git config --global  --list
```

1）、Git\etc\gitconfig  ：Git 安装目录下的 gitconfig   --system 系统级

2）、C:\Users\Administrator\ .gitconfig   只适用于当前登录用户的配置  --global 全局

当你安装Git后首先要做的事情是设置你的用户名称和e-mail地址。这是非常重要的，因为每次Git提交都会使用该信息。它被永远的嵌入到了你的提交中：

```c
git config --global user.name "GauHar"  #名称
git config --global user.email gaohan000206@163.com   #邮箱
```



## git的基本理论

三个区域：

- 工作目录（Working Directory）
- 暂存区(Stage/Index)
- 资源库(Repository或Git Directory)

再加上远程的git仓库，有的时候可以看成是四个工作区域。

- Workspace：工作区，就是你平时存放项目代码的地方
- Index / Stage：暂存区，用于临时存放你的改动，事实上它只是一个文件，保存即将提交到文件列表信息
- Repository：仓库区（或本地仓库），就是安全存放数据的位置，这里面有你提交到所有版本的数据。其中HEAD指向最新放入仓库的版本
- Remote：远程仓库，托管代码的服务器，可以简单的认为是你项目组中的一台电脑用于远程数据交换



git的工作流程：

- Workspace：工作区，就是你平时存放项目代码的地方
- Index / Stage：暂存区，用于临时存放你的改动，事实上它只是一个文件，保存即将提交到文件列表信息
- Repository：仓库区（或本地仓库），就是安全存放数据的位置，这里面有你提交到所有版本的数据。其中HEAD指向最新放入仓库的版本
- Remote：远程仓库，托管代码的服务器，可以简单的认为是你项目组中的一台电脑用于远程数据交换

![image-20230324155136579](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230324155136579.png)

**工作区-----暂存区（本质是一个文件）-----本地库（HEAD指向哪个分支）-----远程库**

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230324155836673.png" alt="image-20230324155836673" style="zoom:67%;" />

提交命令：

- **git add**
- **git commit**
- **git push**

拉取命令：

- **git pull**
- **git reset**
- **git checkout**





## git实操

本地仓库的搭建：

创建本地仓库的方法有两种：一种是创建全新的仓库，另一种是克隆远程仓库。

- 创建全新仓库，在指定的路径打开git bash，然后：

```cpp
# 在当前目录新建一个Git代码库
$ git init
```

- 克隆远程仓库

```cpp
# 克隆一个项目和它的整个代码历史(版本信息)
$ git clone [url]  # https://gitee.com/kuangstudy/openclass.git
```



git的文件操作：

文件的四种状态：

- **Untracked: 未跟踪,** 此文件在文件夹中, 但并没有加入到git库, 不参与版本控制. 通过==git add== 状态变为Staged.
- **Unmodify: 文件已经入库**, 未修改, 即版本库中的文件快照内容与文件夹中完全一致. 这种类型的文件有两种去处, 如果它被修改, 而变为Modified. 如果使用==git rm==移出版本库, 则成为Untracked文件
- **Modified: 文件已修改**, 仅仅是修改, 并没有进行其他的操作. 这个文件也有两个去处, 通过git add可进入暂存staged状态, 使用==git checkout==则丢弃修改过, 返回到unmodify状态, 这个git checkout即从库中取出文件, 覆盖当前修改 !
- **Staged: 暂存状态**. 执行==git commit==则将修改同步到库中, 这时库中的文件和本地文件又变为一致, 文件为Unmodify状态. 执行git reset HEAD filename取消暂存, 文件状态为Modified

查看文件状态命令：

```cpp
#查看指定文件状态
git status [filename]

#查看所有文件状态
git status
```



```cpp
# git add .                  添加所有文件到暂存区
# git commit -m "消息内容"    提交暂存区中的内容到本地仓库 -m 提交信息
```





有些时候我们不想把某些文件纳入版本控制中，比如数据库文件，临时文件，设计文件等

在主目录下建立".gitignore"文件，此文件有如下规则：

1. 忽略文件中的空行或以井号（#）开始的行将会被忽略。
2. 可以使用Linux通配符。例如：星号（*）代表任意多个字符，问号（？）代表一个字符，方括号（[abc]）代表可选字符范围，大括号（{string1,string2,...}）代表可选的字符串等。
3. 如果名称的最前面有一个感叹号（!），表示例外规则，将不被忽略。
4. 如果名称的最前面是一个路径分隔符（/），表示要忽略的文件在此目录下，而子目录中的文件不忽略。
5. 如果名称的最后面是一个路径分隔符（/），表示要忽略的是此目录下该名称的子目录，而非文件（默认文件或目录都忽略）。

```cpp

#为注释
*.txt        #忽略所有 .txt结尾的文件,这样的话上传就不会被选中！
!lib.txt     #但lib.txt除外
/temp        #仅忽略项目根目录下的TODO文件,不包括其它目录temp
build/       #忽略build/目录下的所有文件
doc/*.txt    #会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
```



## 本机绑定SSH公钥，实现免密登录

```cpp
# 进入 C:\Users\Administrator\.ssh 目录
# 生成公钥
ssh-keygen (-t rsa)
```

![image-20230324161606786](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230324161606786.png)

在这个文件夹下面把你的.pub结尾的文件里面的公钥，复制到github的ssh中

![image-20230324161647061](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230324161647061.png)



## GIT中分支相关

master分支标识主分支

常用的分支命令：

```cpp

# 列出所有本地分支
git branch

# 列出所有远程分支
git branch -r

# 新建一个分支，但依然停留在当前分支
git branch [branch-name]

# 新建一个分支，并切换到该分支
git checkout -b [branch]

# 合并指定分支到当前分支
$ git merge [branch]

# 删除分支
$ git branch -d [branch-name]

# 删除远程分支
$ git push origin --delete [branch-name]
$ git branch -dr [remote/branch]
```

如果同一个文件在合并分支时都被修改了则会引起冲突：解决的办法是我们可以修改冲突文件后重新提交！选择要保留他的代码还是你的代码！

master主分支应该非常稳定，用来发布新版本，一般情况下不允许在上面工作，工作一般情况下在新建的dev分支上工作，工作完后，比如上要发布，或者说dev分支代码稳定后可以合并到主分支master上来。