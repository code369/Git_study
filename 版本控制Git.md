### 								**版本控制Git**

#### 一.Git是什么

版本控制工具！Git是目前世界上最先进的分布式版本控制系统（没有之一）。

这个软件用起来就应该像这个样子，能记录每次文件的改动

  ![](../git/笔记 版本控制/认识git.jpg)

  这样，你就结束了手动管理多个“版本”的史前时代，进入到版本控制的20世纪。

#### 二.Git发展史

cvs  --svn

在2002年以前，世界各地的志愿者把源代码文件通过diff的方式发给Linus，然后由Linus本人通过手工方式合并代码！你也许会想，为什么Linus不把Linux代码放到版本控制系系统呢？不是有CVS、SVN这些免费的版本控制系统吗？因为Linus坚定地反对 CVS和SVN，这些集中式的版本控制系统不但速度慢，而且必须联网才能使用。有一些商用的版本控制系统，虽然比CVS、SVN好用，但那是付费的，和 Linux的开源精神不符。

Linus花了两周时间用C写了一个分布式版本控制系统，这就是Git！一个月之内，Linux系统的源码已经由Git管理了！Git迅速成为最流⾏的分布式版本控制系统，尤其是2008年，GitHub网站上线了，它为开源项目免费提供Git存储，无数开源项目开始迁移到GitHub，包括jQuery，PHP，Ruby等等。

#### 三.git运行方式

**1.集中式VS分布式**

Linus一直痛恨的CVS及SVN都是集中式的版本控制系统，而Git是分布式版本控制

（1）集中式版本控制系统，

```
	版本库是集中存放在中央服务器的，你干活的时候，用的都是自己的电脑，所以要先从中央服务器取得最新的版本，然后开始干 活，干完活了，再把自己的活推送给中央服务器。中央服务器就好比是一个图书馆，你要改一本书，必须先从图书馆借出来，然后回到家自己改，改完了，再放回图书馆。集中式版本控制系统最大的弊端就是必须联网才能工作，如果在局域网内还好，速度够快，可如果在互联网上，遇到网速慢的话，可能提交个10M的文件就需要5分钟，这还不得把人给憋死啊。
```

 （2）分布式版本控制系统根本

```
没有“中央服务器”，每个⼈的电脑上都是一个完整的版本库，这 样，你工作的时候，就不需要联网了，因为版本库就在你自己的电脑上。既然每个认电脑上都有个完整的版本库，那多个人如何协作呢？比如说你在自己电脑上改 了文件A，你的同事也在他的电脑上改了文件A，这时，你们俩之间只需把各自的修改推送给对方，就可以互相看到对方的修改了。和集中式版本控制系统相比，分布式版本控制系统的安全性要好很多，因为每个电脑里都有完整的版本库，某个人的电脑坏掉了不要紧，而集中式版本控制系统的中央服务器要是出了问题，所有人都没法干活了
```

git运行方式如图

![](day11/git.png)

**2.工作区和暂存区**

Git和其他版本控制系统如SVN的一个不同之处就是有暂存区的概念

工作区（Working Directory）：就是你在电脑⾥能看到的目录，

版本库（Repository）：工作区有个隐藏目录“.git”，这个不算工作区，而是Git的版本
库，Git的版本库存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还
有Git为我们主动创建的第一个分支master，以及指向master的一个指针叫HEAD。

我们把文件往Git版本库中添加的时候，是分两步执行的：

```
第一步是用“git add”把文件添加进去，实际上就是把文件修改添加到暂存区；第二步是用“git commit”提交更改，实际上就是把暂存区的所有内容提交到当前分支。因为我们创建Git版本库时，Git主动为我们创建了唯一一个master分支，所以，现在，commit就是往master分支上提交更改。你可以简单理解为，需要提交的⽂件修改通通放到暂存区，然后，一次性提交暂存区的所有修改
```

####四.常用git服务器

1.github==全球最大的开源网站

2.码云==免费的，国内的

3.coding==国内的

####五.安装Git

##### 1.Linux系统安装GIt

(1)方法一：yum安装

yum search Git===查看是否有git如果有就下载

Git --version====查版本

下最新版本官网：git-scm.com

注意：默认`yum install git` 安装的为git 1.7.1版本
	coding上面让要使用的git版本为1.8.0以上，而且这个版本clone的时候有错，所以需要手动安装git

（2）方式二：手动安装git

```

	1、安装git依赖包
		yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel gcc perl-ExtUtils-MakeMaker
	2、删除已有的git
		yum remove git
	3、下载git源码
		wget https://www.kernel.org/pub/software/scm/git/git-2.8.3.tar.gz 
		tar -zxvf git-2.8.3.tar.gz
		cd git-2.8.3
		./configure prefix=/usr/local/git/
		make && make install
	4、将git指令添加到bash中,添加到环境变量中
		vi /etc/bashrc
		在最后一行介入
		export PATH=$PATH:/usr/local/git/bin
		source /etc/bashrc  即可
		git --version   git已经安装好，可以查看git版本
```

##### 2.window中安装

这里我们演示Win系统的安装，暂不考虑linux系统

下载安装客户端,安装成功检查是否安装是否成功

	**方法一：桌面右击鼠标出现git bash here** 

		在界面中输入git --version显示版本

	**方法二：运行cmd中输入git --version显示版本**

####六、Git操作（以Github网站为例）

**1.注册并登录Github网站**

常规注册，注意一点需要邮箱认证，否则不能创建项目

**2.Github上创建仓库**

（1）新建一个仓库（Repositories），填写项目名和项目说明，创建成功会生成一个网址

**3.获取项目—从服务器（云端）获取项目到本地**

本地找一个文件夹存放文件，然后右键打开git执行下面代码，可将自己或者别人项目拿到本地

```
git clone https地址====将仓库克隆到本地
```



注意：【创建ssh密钥】也可以在之前创建

创建的目的是为了保证安全性，只有具有密钥的管理员才可上传，其他人只可以下载

git中输入指令可以生成密钥===`ssh-keygen`，生成私钥id_rsa和公钥id_rsa.pub

将公钥粘贴到网站中的

![](../git/笔记 版本控制/密钥1.jpg)

![](../git/笔记 版本控制/密钥2.jpg)

**4.下拉项目更新本地**

在本地看到服务器最新的代码（更新修改情况）

```
git pull    ====  从服务器更新代码
```

**5.本地推送到服务器**

先在本地实施版本控制，即创建版本库，又叫仓库（repository）

（1）创建仓库（版本库),选择一个合适的位置创建一个空目录

```
mkdir +文件名     #文件名和路用英文，文件编辑可用notepad++
cd 文件名
```

(2)进入目标文件夹（想推送的文件所在文件夹）

```
git init    初始化Git仓库，将这个目录可以变为仓库
git add +文件名    添加指定文件
（或者git add .     添加所有文件）

git status  查看当前状态
```

(3)提交文件

```
git  commit  -m  "我写的内容原因"   
(注意：提交原因必须写，否则不能推送)
```

（4）推送文件到服务器

```
git push 
或者git push origin(服务器项目默认名字) master
```

#### 七.配置免密码推送

在网站上创建项目的时候会有两种方式https和ssh

1、Linux中免密码push和pull（使用https方式）

```
1、cd ~
2、vi .git-credentials
		在里面写入  https://{username}:{password}@github.net
3、git config --global credential.helper store
```

2、windows系统中设置免密码

```
windows下面的 ~ 就是这个目录  C:\Users\ZBLi
【注】在windows下面创建以点 开头的文件，需要使用gitbash
打开gitbash
然后和上面的操作一模一样，完成后只有第一次需要输入密码
```

3、使用ssh方式免密码登录

```
1、使用 ssh-keygen 生成公钥和私钥，直接按3个回车即可
2、在  ~/.ssh/id_rsa.pub 里面的内容复制到coding上面的个人设置公钥中
3、git clone git@git.coding.net:phpmonkey/hehe.git  即可
```

#### 八、冲突解决

  	 a和b同时修改同一个文件的同一行代码就会产生冲突，如果a先push，那么b在push的时候就会报错。所以，为了保险起见，只要想向服务端push内容，首先需要pull内容，pull下来之后就会将服务端的代码和本地的代码进行合并，如果有冲突，就会显示冲突(git diff)，如果没有冲突，那就合并成功，然后再push上去即可，如果有冲突，商量解决冲突即可

```
git pull    下拉文件
git diff    查看冲突
```

#### 九、分支学习

```
主分支：master，默认分支
新建分支： git branch 分支名
查看分支： git branch
切换分支： git checkout 分支名
（实际项目中，每个人都要在自己的分支上工作，最后再合并到如果要在master上面合并分支，需要先切回到master（master是默认的主目录）

合并分支： git merge +分支名字
删除分支：git brunch -d +分支名
（如果分支没有合并不能删除）
强制删除: git brunch  -D +分支名字
（如果分支没有合并要删除可以使用）
```

#### 十、开发步骤

一个master，一个dev 

```
（1）新建一个dev
（2）切换到dev进行开发
（3）在dev添加文件并且提交文件
（4）切换到master分支
（5）将dev分支合并到master分支
            git merge dev
（6）推送master到服务端
（7）继续切换到dev进行开发
```



#### 十一、git常用操作小总结

	 git init    =====  建仓库， 初始化Git仓库
	
	git add 说明.txt  =====     把文件（这里指“说明.txt")纳入暂存区(还没有真正纳入版本控制，需要再一步确认)
	
	git status =======查看暂存区状态
	
	git commit  -m '...'  提交纳入仓库（要写原因所以要加 -m）====git commit  -m  "说明内容"
	
	注意：第一次提交需要先提交姓名和邮箱，否则会报错
	
	git log  ===== 查看提交日志
	
	git  checkout  - -  ====删除文件还原：
	
	git reset  -- hard     =====版本号码（至少写五位)       回到历史版本号版本
	
	git reflog    =======   回到删除的未来版本（过去将来时）

#### 十二、两个小案例

##### 1.在Linux本地做版本控制

(1)在用户主目录创建文件夹,命名为gitdemo====mkdir gitdemo

    进入文件夹cd    gitdemo--->ls查看

```
[root@izwz9ao2nl8wvmgaymeyr0z ~]# mkdir gitdemo
[root@izwz9ao2nl8wvmgaymeyr0z ~]# ls
abc   def       eakkkk.txt  git-2.18.0.tar  index.html    mycal.py  Python-3.6.5      
code  dump.rdb  git-2.18.0  gitdemo         index.html.1  mysql     Python-3.6.5.tar 
```

(2) git初始化，将gitdemo文件夹变成git仓库==git init   

```
[root@izwz9ao2nl8wvmgaymeyr0z ~]# git init 
```

（3)创建一个文本文件，命名为hello.txt，放入内容==**echo命令，用 >进行重定向**

```
echo"Hello,Git" > "hello.txt"
注意：输出重定向符号 > =====将Hello,Git内容显示在hello.txt文件中，再次输出内容不变
```

  查看文件写好了没有  cat  hello.txt

 可以再追加一点内容  

```
echo "goodbey world" >> hello.txt
```

(4)将内容纳入版本控制===git add+文件名  

```
[root@izwz9ao2nl8wvmgaymeyr0z gitdemo]# git add hello.txt
```

 **完成这一步并没有真正的纳入版本控制，只是放到了暂存区（是隐藏文件）**，

通过命令ls -a 可以 查看该路径下所有文件（包括隐藏文件，a代表all)，看到隐藏文件...git     

```
[root@izwz9ao2nl8wvmgaymeyr0z gitdemo]# ls -a
.  ..  .git  hello.txt
```

**【补充命令操作】**

  **git rm --cashed  +文件名**   撤销删除文件（ 内容已经放到暂存区了，把删除的文件撤销删除，从暂存区拿回）



 **git checkout** -- hello.txt       工作区写的文件b还没有放到暂存区，把暂存区文件a拿回来回到工作区，用暂行区内容a覆盖工作区内容b（**注意双连接线两侧的空格）**

```
[root@izwz9ao2nl8wvmgaymeyr0z gitdemo]# rm hello.txt
rm: remove regular file ‘hello.txt’? y
[root@izwz9ao2nl8wvmgaymeyr0z gitdemo]# ls       ======此时文件显示为空
[root@izwz9ao2nl8wvmgaymeyr0z gitdemo]# git checkout -- hello.txt
[root@izwz9ao2nl8wvmgaymeyr0z gitdemo]# ls     =======此时文件恢复回来
hello.txt
 [root@izwz9ao2nl8wvmgaymeyr0z gitdemo]# cat hello.txt =====查看一下文本内容，也没有丢失，重新恢复
Hello,Git
goodbey World
```

（5）提交到=====**git commit  -m** 提交（-m的目的是要求写原因）

```
[root@izwz9ao2nl8wvmgaymeyr0z gitdemo]# git commit -m "新增了hello.txt文件"
1 file changed, 2 insertions(+)
 create mode 100644 hello.txt
```

     【注意】第一次提交前需要进行全局设置，用户名和邮箱，名字任意

```
[root@izwz9ao2nl8wvmgaymeyr0z gitdemo]# git config --global user.email "333@example.com"
[root@izwz9ao2nl8wvmgaymeyr0z gitdemo]# git config --global user.name "hao"
```

（6）【补充】--其他操作

每次提交会产生一个日志**git  log** ====查看日志

```
[root@izwz9ao2nl8wvmgaymeyr0z gitdemo]# git log
commit 37e58587772d49119a14b68decc02ed155945d06 (HEAD -> master)
Author: hao <333@example.com>
Date:   Mon Jul 30 09:47:47 2018 +0800

    新增了hello.txt文件
```



 查看历史版本=======**git  reset  --hard**   +版本号（最少5位）可以找到历史版本

				方法二：**git reset --hard HEAD^**======回到当前版本的上一个版本

【例】对这两种方法演示

	步骤a: 先复制一个文件，这利用之前的code文件下的share_fish为例

       **注：** Linux cp命令主要用于复制文件或目录。格式： **cp   ./code/test/   newtest**====将code目录下的test文件复制到新目录newtest

```
[root@izwz9ao2nl8wvmgaymeyr0z gitdemo]# cp ../code/share_fish.py ./    将分鱼文件复制到当前文件
[root@izwz9ao2nl8wvmgaymeyr0z gitdemo]# ls
hello.txt  share_fish.py
```

     步骤b:   添加share_fish文件，并查状**态git add和git status命令**

```
[root@izwz9ao2nl8wvmgaymeyr0z gitdemo]# git add share_fish.py
[root@izwz9ao2nl8wvmgaymeyr0z gitdemo]# git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   share_fish.py
```

     步骤c:提交----此时文件夹下增加了分鱼文件，此时提交git commit -m

```
[root@izwz9ao2nl8wvmgaymeyr0z gitdemo]# git commit -m "新增了share_fish.py文件"
[master f6fb32a] 新增了share_fish.py文件
 1 file changed, 22 insertions(+)
 create mode 100755 share_fish.py
```

步骤d:查看日志git log，此时出现了两个版本

```
[root@izwz9ao2nl8wvmgaymeyr0z gitdemo]# git log
commit f6fb32a62450153c7213cd408c1aa1851268715d (HEAD -> master)
Author: hao <333@example.com>
Date:   Mon Jul 30 09:58:49 2018 +0800

    新增了share_fish.py文件

commit 37e58587772d49119a14b68decc02ed155945d06
Author: hao <333@example.com>
Date:   Mon Jul 30 09:47:47 2018 +0800

    新增了hello.txt文件
```

**注意：最新的版本head指向谁谁就是最新版本**

步骤e:回到刚才版本======**git reset --hard HEAD^**

```
[root@izwz9ao2nl8wvmgaymeyr0z gitdemo]# git reset --hard HEAD^
HEAD is now at 37e5858 新增了hello.txt文件
[root@izwz9ao2nl8wvmgaymeyr0z gitdemo]# git log
commit 37e58587772d49119a14b68decc02ed155945d06 (HEAD -> master)
Author: hao <333@example.com>
Date:   Mon Jul 30 09:47:47 2018 +0800

    新增了hello.txt文件
```

注意;此时回到了之前的版本，想查看刚才的分鱼文件用git log 查看不到,需要用过去将来式**git reflog查看**

```
[root@izwz9ao2nl8wvmgaymeyr0z gitdemo]# git reflog
37e5858 (HEAD -> master) HEAD@{0}: reset: moving to HEAD^
f6fb32a HEAD@{1}: commit: 新增了share_fish.py文件
37e5858 (HEAD -> master) HEAD@{2}: commit (initial): 新增了hello.txt文件
```

步骤f:现在想从目前为止恢复回来share_fish状态，不能用git reset --hard HEAD^了，需要用历史版本号，通过上面的代码我们找到文件代码为f6fb32a

```
[root@izwz9ao2nl8wvmgaymeyr0z gitdemo]# git reset --hard f6fb32a
HEAD is now at f6fb32a 新增了share_fish.py文件
[root@izwz9ao2nl8wvmgaymeyr0z gitdemo]# ls
hello.txt  share_fish.py
```

##### 2.Linux本地和服务器项目做关联（以coding网为例）

本地实施完想放到云端，（即本地做了版本控制，在云端建了项目）一般先在服务器将仓库建好，然后再克隆clone下来，往里面加东西。

（1）登录coding新建项目，命名为gitdemo；生成项目的URL,复制一下

（2）加远端仓库

**【命令】git remote add  origin +url地址**======关联远端仓库(origin是默认的)

```
root@izwz9ao2nl8wvmgaymeyr0z gitdemo]# git remote add origin https://git.coding.net/qingpingle/gitdemo.git
```

这样本地和远端项目建立联系

（3）配置环境变量（否则会报错）：

进主目录 ---->s输入vim  .bash  profile

在path后面添加====PATH=$PATH:/usr/local/python36/**bin/usr/local/libexec/git-core**

（4）将远端仓库的内容pull到本地：

		 git pullhttps://git.coding.net/jackfrued/gitdemo.git master  

		git pull =====从远端的master分支拉下来

                      

 将本地已经实施了版本控制的内容push到远端仓库： 

         **【命令】git push origin master     (注意第一次使用，需要-u，目的是为了本地和远端做合并)**

           push  -u  (第一次要-u,这样才能实现本地和远端的合并，下一次就不用 - u了)

```
[root@izwz9ao2nl8wvmgaymeyr0z gitdemo]# git push -u origin master
Username for 'https://git.coding.net': 
```



（5）部署公钥（coding项目中左侧部署公钥选择，将生成的密钥可粘贴进去）

【命令】**ssh-keygen**===生成密钥对

输入格式（注意空格和大小写）=====ssh-keygen    -t rsa  -b 4096 -C"jackess@126.com"（邮箱地址）

***注意：	 rsa(加密类型)***

		***4096（密码的强度）**

```
Enter file in which to save the key (/root/.ssh/id_rsa): 
/root/.ssh/id_rsa already exists.
Overwrite (y/n)? y
Enter passphrase (empty for no passphrase):                   这里输入直接跳过
Enter same passphrase again:                                    跳过，一直回车，最后显示出密钥
Your identification has been saved in /root/.ssh/id_rsa.
Your public key has been saved in /root/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:gPbFDtmdioByI4S+E0tJL7PF3OyZXK9/1mZe5wxkAcs SSSDAD@126.com
The key's randomart image is:
+---[RSA 4096]----+
|..          .    |
|o. . . + . o o   |
|= O * + + o E .  |
| @ B = B .     . |
|. O o * S     o  |
| =   =   .   o   |
|  .     .   . ...|
|       .   o +.+.|
|        ..o +.  o|
+----[SHA256]-----+
```

此时在 cd    /root/.ssh中会生成文件id_rsa

```
root@izwz9ao2nl8wvmgaymeyr0z ~]# cd .ssh
[root@izwz9ao2nl8wvmgaymeyr0z .ssh]# ls
authorized_keys  id_rsa  id_rsa.pub  known_hosts
```

cat id_rsa.pub

```
[root@izwz9ao2nl8wvmgaymeyr0z .ssh]# cat id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQDerB2x/lVOBz5LjR+mhJpigcPXMSwHsiPdK81AKo7lagvP6250aNVoRTouhEaGtDg646CVTknXhF2L5nLMSLjCf3LwtOnu6/eI685LBJ/JCgyAdE73aBRR+mRLeQkRIAdPUy3oNOmnQ1UMX/TeJj3hBr+lDmxmNleSUle7TIl3hHDbQcNHTFnNgWAY4Qn/hujq6rp9fekd594YfuR8Ykd+tJjUHCteQElWRhSxckFQYbJ41d+XgugrVtO18PDZGEvkOTmimwzZylbwnCQDwbGiSDfXZZYuqNH0ZzyqJpyO9CUAh3GzVERuAsJM/f28VoyGRJQSwPivOXsVTgvGy/e4tDpYZ/BIcc03CArcxy8Ztvp2nJYXtca8EasDVwqXneB5nMQoYn2pJg5/SaPU+pPo+Nb4J6e1ea7WwcXjhgM3dpU3rhOko75ZPkX+RvaNH7jHrt5UXDO6uADKT7r9jnhhsznU41E+ifxXSZpg4nGS9DIKY2YyNUAiiQOpU0BsxrsZQTbue1gbbMN1/3CjkVTeX7nFVlBARpauQ3MSc8TwnFSm6CXnDbUfYkymzCzVAMJl7PhC6UQ8gHv4J+GychS/jkhbB2y9NPRTc1Bd6vG5anakRtG2DROOmVmFGQ0b9GegZ1FScL0MtNEwYsYqFrGQSeHp8opxVjsDeo6bOOI5Ww== SSSDAD@126.com
```



将公钥粘贴到coding项目中“部署公钥”

（5）克隆到本地并建分支

在coding网新建项目gitflow

复制Url

git clone +url=====克隆到本地

**git  branch**   new-cool-function(新分支名字)  =====建分支,命名为new-cool-function



**git checkout**  new-cool-function（分支名字） ====== 切换到分支（这里分支名字为new-cool-function)

**git checkout -b** issue -1120        =======创建并切换到这个分支，即如果没有分支会直接建立这个分支（常用）

（实际项目中，每个人都要在自己的分支上工作，最后再合并到

如果要在master上面合并分支，需要先切回到master**（master是默认的主目录）**

**git merge** +分支名字   =======合并分支

**git brunch   -d** +分支名字======删除分支

（如果分支没有合并不能删除）

**git brunch  -D** +分支名字====强制删除

（如果分支没有合并要删除可以使用）

