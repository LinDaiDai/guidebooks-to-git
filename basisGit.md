# Git 基础
<!--update-->
### 第一章 下载以及使用



下载地址:

https://github.com/



#### 1.1配置git



​	在命令行模式里输入以下命令

​      git config --global user.name "用户名"

​      git config --global user.email "邮箱名"

  注:全英文,不能用中文

​	输入完后检查是否输入成功

​	git config --list

  若:

![img1](https://github.com/LinDaiDai/guidebooks-to-git/blob/master/basisGitImg/img1.png?raw=true)

​	显示除了user.name 以及 user.email   即输入成功;

 

#### 1.2Git理论基础

	##### 		1.三颗树

​			工作区域      暂存区域      Git仓库

![img2](https://github.com/LinDaiDai/guidebooks-to-git/blob/master/basisGitImg/img2.png?raw=true)

		#####  		2.Git的工作流程

​			1.在工作目录中添加,修改文件

​			2.将需要进行版本管理的文件放入暂存区域

​			3.将暂存区域的文件提交到Git仓库

​		Git管理的三种状态:

​			1.以修改		modified

​			2.以暂存		staged

​			3.已提交		committed

	#### 1.3 创建Git项目

​	1.在磁盘中创建一个文件夹MyProject  用来存放你的Git项目

​	2.然后打开命令CMD   进入存放MyProject 的磁盘  ,  并用输入 cd   MyProject 进入文件夹

​	3.输入命令     git  init        会显示初始化了一个空的git仓库(如图):

​	![img3](https://github.com/LinDaiDai/guidebooks-to-git/blob/master/basisGitImg/img3.png?raw=true) 

  		并且在文件夹中创建了一个git文件(如图):

​	![img4](https://github.com/LinDaiDai/guidebooks-to-git/blob/master/basisGitImg/img4.png?raw=true)



​	4.在当前MyProject文件夹内创建一个md类型的文本(文本名为README)  并以notepad++打开(为防止乱码,可把notepad++内的编码格式改为 UTF-8无BOM编码格式;   (即工作流程中的第一步)

​	5.输入命令:  git add README.md    (即工作流程中的第二步,将README文件添加至暂存区域,若要添加全部的文件可用 --all)

​	 回车之后再输入:     git commit -m "add a readme file"    (commit 提交,即工作流程中的第三步,将暂存区域内的README文件提交到git仓库)

​				引号内是写入对这次提交做的一个说明(做了什么),

​		显示如下图:	

![img5](https://github.com/LinDaiDai/guidebooks-to-git/blob/master/basisGitImg/img5.png?raw=true)

​		

#### 1.4 git status 

> 作用: 查看此时 git 的状态

​		输入  git status  即可查看此时git的状态 (如图):

​		![img6](https://github.com/LinDaiDai/guidebooks-to-git/blob/master/basisGitImg/img5.png?raw=true) 

​		 在一个默认的分区 master 中

​		 没有需要提交的文件,当前的工作目录是干净的

#### 1.5添加协议 开源

​	1.在当前文件夹创建一个md  (文件名为 LICENSE)  ,里面写MIT的开源协议

​	将README内的内容进行编辑;

​	此时 在 git status 下查看  ,可发现:

​	![img7](https://github.com/LinDaiDai/guidebooks-to-git/blob/master/basisGitImg/img7.png?raw=true)		

​		此时发现 , README.md 是已经添加到了暂存区域并提交的

​		而  LICENSE.md 是未被跟踪的状态  ( 即在工作区域内的,圆括号内代表git给我们的建议 );

​	

​	2.将LECENSE添加至暂存区域并查看状态

​	![img8](https://github.com/LinDaiDai/guidebooks-to-git/blob/master/basisGitImg/img8.png?raw=true)

​	

#### 1.6 git reset HEAD

将LECENSE添加至暂存区域后,会提示出 是否使用 git reset HEAD 的操作(若不 操作则不用理他)

> 作用: 撤销上一次的操作 ,返回上一个版本   HEAD表示当前版本  上一个表示HEAD~
>
> 是将git仓库中的内容恢复到暂存区域中

一般  会   HEAD~(1~100) 这样写

​		git reset   <版本快照 文件名/路径> 也可以指定文件名

1.git reset  --mixed HEAD~			(默认)

​	-移动HEAD的指向,将其指向上一个快照

 	-将HEAD移动后指向的快照回滚到暂存区域

2. git reset   --soft  HEAD~			(仅仅只是修改了HEAD指针,相当于撤销git commit 这一步而已

     -移动HEAD的指向,将其指向上一个快照 

     3. git reset  --hard  HEAD~		(同时影响了三颗树)

​       -移动HEAD的指向,将其指向上一个快照

​       -将HEAD移动后指向的快照回滚到暂存区域

​       -将暂存区域的文件还原到工作目录

区别详情请参考1.9的例1

  快照1   快照2  快照3    当HEAD处于快照3时,使用git reset --hard HEAD~ 回到快照2 ,若此时再想返回快照3:

​	方法1:  查看以前的历史记录  找到快照3的id 并使用git reset -hard 快照3id  ;

​	方法2: 若找不到快照3的id ,可使用git reflog  (注:用来记录你的每一次指令)查看你的快照3的id名   ,然后再执行git reset --hard 快照3id

#### 1.7 git checkout 

> 作用1: 	git checkout --<file>			将暂存区内的文件内容覆盖工作目录的文件内容
>
> 作用2:	git checkout 分支名			切换到指定分区

如在1.5的操作中,我们将LICENSE的这个文件提交到了暂存区域中,在使用git commit -m " add a license file" 命令将其提交到git仓库;

之后,如果我们对LICENSE内的内容进行编辑或者修改,如将LICENSE协议内首行的<year>换为2017; 

( 此时可以理解为LICENSE有俩个版本,一个是最开始在暂存区中的版本(即year),一个是工作目录下的版本(即2017)

此时,在输入 git status 来查看git的工作状态,会提示出 

  1.  是否将已改动的文本添加至暂存区域中 ;

  2.  是否将暂存区域中对应的这个文件内容覆盖工作目录的文件内容

      如下图( README 和  LICENSE  俩个文件都是改动过的 ):

![img9](https://github.com/LinDaiDai/guidebooks-to-git/blob/master/basisGitImg/img9.png?raw=true)

此时 若输入git add LICENSE.md  回车

​		    git commit -m " add a license file" 

​		则将暂存库里和工作目录中的LICENSE 的内容都修改了 

​	若输入 git checkout -- LICENSE.md 

​		则暂存库里的内容没被修改,并且工作目录中的内容也会变为暂存库中的内容

#### 1.8 git log

>  作用: 查看历史提交

 	 历史提交 最新的提交在最头上;

​	git log --decorate	--oneline	只显示快照的说明 ID 不显示作者,日期等其他信息(能精简快照历史信息)

​			--graph    以图形的方式显示

​			--all  	显示所有的分支

​	如下图:有俩个分支master feature	

​	![img15](https://github.com/LinDaiDai/guidebooks-to-git/blob/master/basisGitImg/img15.png?raw=true)

​	d1d14c6表示的是俩个分支共同拥有的		

#### 1.9 git reset 和 git checkout 的区别

![img10](https://github.com/LinDaiDai/guidebooks-to-git/blob/master/basisGitImg/img10.png?raw=true)

​	不难看出

​		checkout  是将工作区域内的内容恢复成暂存区域

​		reset 是将git仓库内的内容恢复成上一个版本

​	**恢复文件**:

​		checkout 命令和 reset 命令都可以用于恢复指定快照的指定文件,并且他们都不会改变HEAD指针的指向.

​		区别是: reset 命令只将指定文件恢复到暂存区域(--mixed) , 而checkout 命令是同时覆盖暂存区域和工作目录.

​		( 如果你想使用 git reset --hard HEAD~ README.md 命令让reset 同时覆盖工作目录,但git会告诉你不行,因为此时,reset不允许使用--soft或者--hard 选项.SO 恢复文件上,reset要安全一些)

​	区别:

​		1.对于reset --hard 命令,checkedout 命令更安全,因为 checkedout 命令在切换分支前会先检查一下当前的工作状态,如果不是 "clean"的话,git不会允许你这样做,而 resert --hard 命令则是直接覆盖所有数据;

​		2.如何更新HEAD指向, reset 命令会移动 HEAD所在分支的指向,而 checkout 命令只会移动HEAD自身来指向另一个分支.

**例1:**

​	1.在master 中创建3个txt , 1.txt	2.txt   3.txt 并添加到git 仓库,

​	2.git checkout -b feature	创建一个分支feature并将指针指向它,

​	3.在分支feature中创建1个名为 feature1.txt 的文件并添加到git仓库,

​	4.使用 git checkout master 跳回到 master中,再在master中创建1个名为 master1.txt 的文件并添加到git仓库中,

​	5.再执行	git reset --hard feature 	此时查看git log 对比第4步和第5步

​		![img17](https://github.com/LinDaiDai/guidebooks-to-git/blob/master/basisGitImg/img17.png?raw=true)

​		说明:	git reset  --hard feature命令将HEAD 指向的分支(即master)以及HEAD本身都切到了feature分支里,换句话说,原来的快照已经消失了(master1.txt那个快照不见了).

​	6.此时执行  git reset --soft HEAD~    和 git reset HEAD~	

​		![img18](https://github.com/LinDaiDai/guidebooks-to-git/blob/master/basisGitImg/img18.png?raw=true)

​		说明 :	--soft 仅仅将指针HEAD指向了上一个快照,    --mixed 也会将指针HEAD指向上一个快照, mixed还会将HEAD指针移动后的快照回滚到暂存区域		此时查看git status:

​	![img19](https://github.com/LinDaiDai/guidebooks-to-git/blob/master/basisGitImg/img19.png?raw=true)

​		说明: 回到了" 还没有将3.txt 添加到暂存区域 " 时

#### 例子

  1.  在E盘创建文件夹MyProject,

  2.  在CMD 进入E盘中的MyProject文件夹内:       E:    回车      cd  MyProject     ;

  3.  创建空的git仓库:    git init 

  4.  在MyProject 文件夹内创建README.md 文件

  5.  将README.md文件添加到暂存区域:      git add README.md

  6.  将README.md文件提交到git仓库:         git commit -m " add a readme file";

  7.  在MyProject文件夹内创建LICENSE.md文件,并写上MIT协议

  8.  将LICENSE.md文件添加到暂存区域:     git  add LICENSE.md

  9.  修改LICENSE.md文件内的year 改为2017

  10.  执行 :    git status        弹出:     1. use " git add <file>.."    2. use " git checkout -- <file>.."

  11.  执行 :    git add LICENSE.md   和  git commit -m " add a license file";

  12.  执行 :    git log 查看历史记录:

       ![img11](https://github.com/LinDaiDai/guidebooks-to-git/blob/master/basisGitImg/img11.png?raw=true)

结构模型:

![img12](https://github.com/LinDaiDai/guidebooks-to-git/blob/master/basisGitImg/img12.png?raw=true)

14. 执行 git reset HEAD~       回车               git status 

    ![img13](https://github.com/LinDaiDai/guidebooks-to-git/blob/master/basisGitImg/img13.png?raw=truef git\img13.png)

结构模型

![img14](https://github.com/LinDaiDai/guidebooks-to-git/blob/master/basisGitImg/img14.png?raw=true)

此时,git会检测到工作区域内的LICENSE版本比暂存区域内的版本新,所以会有提示,是否要更新

### 第二章  版本对比

#### 1. git diff

a、查看尚未暂存的文件更新了哪些部分，不加参数直接输入
​    git diff
此命令比较的是工作目录(Working tree)和暂存区域快照(index)之间的差异
也就是修改之后还没有暂存起来的变化内容。

b、查看已经暂存起来的文件(staged)(即git仓库中的快照)的差异
​    git diff --cached  快照ID			没加ID名就是和上次提交时的快照之间(HEAD)最新的git仓库中的快照的差异
​    git diff --staged	  快照ID
显示的是下一次commit时会提交到HEAD的内容(不带-a情况下)

c  比较俩个历史版本之间的快照

   git diff   STAID1   STAID2

d.比较 工作目录(Working tree) 和git仓库中的快照

 git diff   STAID(要比较的那个快照的ID名)

### 第三章 实用小技巧

#### 1.修改最后一次提交


​	情景一:	版本刚一提交(commit)到仓库,突然想起漏掉俩个文件还没有添加(add);

​	情景二: 	版本刚一提交到仓库,突然想起版本说明写得不够全面,

执行带 --amend  选项的commit操作 Git就会"更正"最近的一次提交:	git commit --amend

​		进入更正界面		大写I  	将要修改的地方修改	esc		shift + s 保存并退出  此时查看历史,发现快照并没有增加一个,而是在原本的快照基础上进行了修改

​		若不想修改		大写Q      输入q! 回车  	退出当前更正界面

#### 2.恢复删除的文件

​	若在文件夹中不小心将文件删除,

​	git checkout -- <file>	即可看到文件又恢复到了文件夹中

#### 3.从git中删除文件

​	情形一:

​		若一个文件你已经提交到了git仓库,想让它删除掉并且没有任何记录

​	先执行:

​	git rm <file>

​		该命令删除的只是工作目录和暂存区域的文件,也就是取消跟踪,在下次提交时不纳入版本管理.(但在git仓库还是会有快照的历史记录)

​	再执行:

​	git reset --soft HEAD~

​		此时再查看git log  就发现历史记录中并没有刚刚删除的那个快照;

​	情形二:

​		若一个文件你添加到了暂存区域,之后又对工作区域的文件进行的修改,

​			执行:	git rm <file> 	时,git 会提示你 此时 暂存区域和工作区域有俩个版本的文件,问要删除哪一个;

​			若执行:	git rm -f <file>				git 会将俩个版本都删除(一个-)

​					git rm --cached <file>			git会删除暂存区域, 保留工作区域(俩个-)

	#### 4.git重命名文件

​	git mv <原来的文件名>  <改之后的文件名>

​	例: 	git mv game.html workgame.html



### 第四章 Git分支

	#### 1:创建分支

​	git brance 分支名

​	![img16](E:\每日笔记\course of git\img16.png)

	#### 2:切换分支

​	git checkout 分支名	

​	git checkout -b feature2	创建并切换到feature2的分支

#### 3.合并分支

​		git  merge 分支名

​		如此时再master分支中,想将feature 的分支合并过来:		git merge feature 

​		若不同分支中有相同名称的文件,文件内容却不同,此时合并时git会提示有冲突CONFLICT,需要我们人为去合并

​			打开文件将HEAD 内的内容和feature的内容合并起来保存并退出

​			此时再执行 git status 操作, 可发现git提示你git add <file> 	执行git add <file>后,执行 git commit -m " add fixed file";

​			执行git log --decorate --oneline --graph --all

​			会发现俩分支合并到了一起	

#### 4.删除分支

​	git brand -d 分支名

### 第五章: 将本地项目上传到GitHub

​	1.在GitHub上创建一个git 仓库 : 点Great a new repository;

​	2.在Github上设置好SSH密钥并创建好git远程仓库后,就可以和本地关联了 在本地git仓库的命令栏中输入:

​		$ git remote add origin <GitHub上创建好的仓库的地址>

​	3.将本地库里的所有内容推送到远处仓库(也就是GitHub上了)通过:

​		$ git push -u origin master

​	4.由于新建的远程仓库是空的 所以第一次推送要加上 -u   等远程仓库有了内容之后就可以直接通过:

​		$ git push  origin master	

​	注: 这里有个坑需要注意一下，就是在上面第七步创建远程仓库的时候，如果你勾选了Initialize this repository with a README（就是创建仓库的时候自动给你创建一个README文件），那么到了第九步你将本地仓库内容推送到远程仓库的时候就会报一个failed to push some refs to https://github.com/guyibang/TEST2.git的错。

​	     这是由于你新创建的那个仓库里面的README文件不在本地仓库目录中，这时我们可以通过以下命令先将内容合并以下：

```
$ git pull --rebase origin master
```

​	然后你在执行 push 就可以了.



**注:**

​	执行  git reflog	查看所有快照的id等等

​	若push时有一些关于 REBASE的提示,可执行 git  rebase master



### 第六章: Fork

当你觉得gitbub上有人的项目写的特别好,你也想和他一起完善这个项目的时候,你就可以使用Fork

1.在别人的项目里点击Fork,此时返回自己的github 可以发现自己的profile下多了一个别人的项目

2.使用clone自己的这个项目到本地,在本地进行修改操作

3.修改完之后,使用指令



```
$ git add --all
$ git commit -m "add some file"
$ git push
$ git remote add upstream 别人的这个项目的git仓库地址
```

4.执行完后可以使用git remote -v查看是否添加成功,

```
origin  git@github.com:LinDaiDai/vue2-axf.git (fetch)
origin  git@github.com:LinDaiDai/vue2-axf.git (push)
upstream        https://github.com/tangcaiye/vue2-axf.git (fetch)
upstream        https://github.com/tangcaiye/vue2-axf.git (push)

```

5.到你的github找到刚刚的项目,点击New pull request 将你刚刚要添加的内容提及上去,等待对方同意就ok

###第七章：SSH Keys

1.要确定你的电脑上安装了git 并且添加到了环境变量中
2.在开始中找到git bash并打开，输入 $ssh-keygen -t rsa -C "username@email.com" 
此时会提示你输入存储key的文件名（我输入github），并提示你输入密码与确认密码（我这里选择不输入），接着会生成连个文件名一个是公钥与私钥文件并存储在C:\Users\***文件夹下：github，github.pub
![img17](E:\每日笔记\course of git\img16.png)
![img18](E:\每日笔记\course of git\img16.png)
3.在github上 settings -> SSH and GPG keys -> new SSH key 
title 随便输 
key 填入 C:\Users\cestbon\.ssh\id_rsa.pub 内的内容
