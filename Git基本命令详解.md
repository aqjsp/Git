# 一、Git  

Git是一个很强大的分布式版本管理工具，它不但适用于管理大型开源软件的源代码（如：Linux、kernel）,管理私人的文档和源代码也有很多优势（如：wsi-lgame-pro）.  ![image](https://raw.githubusercontent.com/aqjsp/Pictures/main/202401172148489.png)  

## 1、git clone  

```git
git clone https://github.com/...  
git clone 支持多种协议，除了http/https以外，还支持ssh、git、本地文件协议等。  
git clone http[s]:// example.com/...  
git clone ssh://...  
git clone git://...  
git clone /opt/git/project.git  
git clone file:///opt/git/...  
git clone ftp[s]://example.com/...  
git clone rsync://example.com/...  

```

克隆版本库的时候，所使用的远程主机自动被Git命名为origin。如果想用其他主机，需要用git clone命令的-o选项指定。  

```
git clone -o jQuery https://github.com/jquery/jquery.git  
git clone -b 分支名  仓库地址  
```

## 2、git remote  
```
git remote show命令加上主机名，可以查看该主机的详细信息  
git remote show <主机名>  
git remote add命令用于添加远程主机  
git remote add <主机名><网址>  
git remote rm命令用于删除远程主机  
git remote rm <主机名>  
git remote rename命令用于远程主机的改名  
git remote rename <原主机名><新主机名> 
```

## 3、git fetch  
一旦远程主机的版本有了更新，需要将这些更新取回本地，这时就需要用到git fetch命令。这个命令将某个远程主机的更新，全部取回本地。  
git fetch命令通常用来查看其他人的进程，因为它取回的代码对你本地的开发代码没有影响。默认情况下，git fetch取回所有分支（branch）的更新，如果只想取回特定分支的更新，可以指定分支名。  
git fetch <远程主机名><分支名>  
比如，取回origin主机的master分支:  
git fetch origin master  
所取回的更新，在本地主机上要用“远程主机名/分支名”的形式读取。比如origin主机的master，就要用origin/master读取。  

## 4、git branch  
branch的基本操作：  

```
git branch // 查看本地所有分支  
git branch -r // 查看远程所有分支  
git branch -a // 查看本地和远程的所有分支  
git branch -d  // 删除本地分支  
git branch -d -r // 删除远程分支，删除后还需推送到服务器  
git push origin // 删除后推送至服务器  
git branch -m  // 重命名本地分支  

```

git中一些选项解释：  

```
-d   --delete : 删除  
-D   --delete  --force的快捷键  
-f   --force ：强制  
-m   --move：移动或重命名  
-M   --move --force 的快捷键  
-r   --remote ：远程  
-a   --all ： 所有  

```

以上命令表示，本地主机的当前分支是master，远程分支是origin/master。  
取回远程主机的更新以后，可以在它的基础上，使用git checkout命令创建一个新的分支。  
git checkout -b newBranch origin/master  
创建分支命令：git branch (branchname)  
切换分支命令：git checkout (branchname)  
合并分支命令：git merge  
列出所有分支基本命令：git branch  
git checkout -b (branchname) 来创建新分支并立即切换到该分支下  
删除分支命令：  
git branch -d (branchname)  
git branch * master newtest  
README  test.txt  test2.txt  
git merge newtest  
将newtest分支合并到主分支去,test2.txt文件被删除  
以上命令表示在当前分支上，合并origin/master  

## 5、git pull与git push  
git pull命令的作用是，取回远程主机某个分支的更新，再与本地的指定分支合并。  
git pull <远程主机名> <远程分支名>:<本地分支名>  
比如，取回origin主机的next分支，与本地的master分支合并，需要这样写：  
git pull origin next:master  
如果远程分支是与当前分支合并，则冒号后面的部分可以省略。  
git pull origin next  
以上命令表示，取回origin/next分支，再与当前分支合并。实质上，这等同于先做git fetch，再做git merge  
git fetch origin  
git merge origin/next  
在某些场合，git会自动在本地分支与远程分支之间，建立一种追踪关系（tracking）。比如，在git clone的时候，所有本地分支默认与远程主机的同名分支，建立追踪关系，也就是说，本地的master分支自动“追踪”origin/master分支。  
git也允许手动建立追踪关系  
git branch --set-upstream master origin/next  
以上命令指定master分支追踪origin使用-u选项指定一个默认主机，这样后面就可以不加任何参数使用git push  
git push origin --tags  
最后，git push不会推送标签（tag），除非使用-tags选项。  
以上命令使用-force选项，结果导致远程主机上更新的版本被覆盖。除非你很确定要这样做，否则应该尽量避免使用-force选项。  
git push --force origin  
如果远程主机的版本比本地版本更新，推送时git会报错，要求现在本地做git pull合并差异，然后再推动到远程主机，这时，如果你一定要推送，可以使用-force选项。  
上面命令表示，将所有本地分支都推动到origin主机  
git push --all origin  
还有一种情况，就是不管是否存在对应的远程分支，将本地的所有分支都推送到远程主机，这时需要使用-all选项  
git config --global  push default matching 或者  git config --global  push.default  simple  
不带任何参数的git  push，默认只推送当前分支，这叫做simple方式，此外还有一种matching方式，会推送所有有对应的远程分支的本地分支。git 2.0版本之前，默认采用matching方法，现在改为默认采用simple方式，如果需要修改这个命令，可以采用git config命令。  
上面命令将本地的master分支推送到origin主机，同时指定为默认主机，后面就可以不加任何参数使用git push了  

```
git push -u origin master  
git push  
```

如果当前分支只有一个追踪分支，那么主机名就可以省略。  
上面命令表示，将当前分支推送到origin主机的对应分支。  

```
git push originnxt
```

如果当前分支与远程分支存在追踪关系，git  pull就可以省略远程分支名。  

```
git pull origin
```

 如果当前分支与远程分支存在追踪关系，则本地分支和远程分支都可以省略。  
上面命令表示删除origin主机的master分支。  

```
git push origin ：master 或者 git push origin --delete master
```

 如果省略本地分支名，则表示删除指定的远程分支，因为这等同于推送一个空的本地分支到远程分支。  
上面命令表示，将本地的master分支推送到origin主机的master分支，如果后者不存在，则会被新建  

```
git push origin master  
```

如果省略远程分支名，则表示将本地分支推送与之存在“追踪关系”的远程分支，如果该远程分支不存在，则会被新建。  
注意：分支推动顺序的写法是<来源地>：<目的地>，所有git pull是<远程分支>：<本地分支>，而git push是<本地分支>：<远程分支>。 

```
git push <远程主机名> <本地分支名>：<远程分支名>  
git  push命令用于将本地分支的更新推送到远程主机  
git pull -p 或者 git fetch --prune origin  
git fetch -p  
```

加上参数-p就会在本地删除远程已经删除的分支  

```
git pull --rebase <远程主机名> <远程分支名>：<本地分支名>  
```

如果合并需要采用rebase模式，可以使用-rebase选项。  
上面命令表示，当前分支自动与唯一一个追踪分支进行合并。  

```
git pull  
```

如果当前分支只有一个追踪分支，连远程主机名都可以省略。  
上面命令表示，本地的当前分支自动与对应的origin主机“追踪分支”（remote-tracking  branch）进行合并。  

```
git pull origin  
```

如果当前分支与多个主机存在追踪关系，则可以使用-u选项指定一个默认主机，这样后面就可以不加任何参数使用git push  
## 6、git rev-parse  
准备工作：  
在工作区中建立目录a/b/c，进入该目录。  

```
cd /path/to/my/workspace/demo/  
mkdir -p a/b/c  
cd /path/to/my/workspace/demo/a/b/c 
```

 显示版本库 .git目录所在的位置  

```
git rev-parse --git-dir  
/path/to/my/workspace/demo/.git  
```

显示工作区根目录  

```
git rev-parse --show-toplevel  
/path/to/my/workspace/demo
```

显示相对于工作区根目录的相对目录  

```
git rev-parse --show-prefix  
a/b/c  
```

显示从当前目录（cd）后退（up）到工作区的根的深度  

```
git rev-parse --show-cdup  
../../..
```

获取当前最后一个commit hash  

```
git rev-parse HEAD  
```

这个命令中的HEAD可以替换成branch name，如:  

```
git rev-parse dev获取dev分支的最后一次提交  
git rev-parse --abbrev-ref HEAD获取当前分支名
```

这个命令都说是获取当前的xx，也就是说运行命令时所在的git目录，如果在任何目录运行可以获取当前的xx，需要明确指出 .git目录的位置以及git对应的工作目录。  

```
git --git-dir='./maleskine/.git' rev-parse --abbrev-ref HEAD  
```

通过设置--git-dir选项，也可以正确的获取到maleskine项目当前的分支名。git还有一个选项--work-tree可以指定git的工作目录。  
## 7、git reset  
将版本库还原到历史的某个时刻的状态  

```
git reset --hard logid(logid的前几位即可)  
```

将版本库还原到上一次commit之前的状态  

```
git reset --hard HEAD^   
```

有时候，进行了错误的提交，但是还没有push到远程分支，想要撤销本次提交，可以使用git reset –-soft/hard命令。  
回退到某个版本，只回退了commit的信息，代码修改过的没变。如果还要提交，直接commit即可；  

```
git reset –-soft 
```

 彻底回退到某个版本，本地的源码也会变为上一个版本的内容，撤销的commit中所包含的更改被冲掉，即commit与修改过代码都撤销，变为原来的某个版本；  

```
git reset -–hard
```

##  8、git config  

添加版本库的用户名到本地配置文件  

```
git config --global user.name 'username'
```


添加版本库的用户邮箱到本地配置文件  

```
git config --global user.emal 'emal' 
```

## 9、git diff  
执行git diff来查看执行git status的结果的详细信息。  
git diff命令显示已写入缓存与已修改但尚未写入缓存的改动的区别。  
尚未缓存的改动：  

```
git diff
```

查看已缓存的改动:  

```
git diff --cached  
```

查看已缓存的与未缓存的所有改动:  

```
git diff HEAD  
```

显示摘要而非整个diff:  

```
git diff --stat 
```

举个栗子：  

```
git status -s  
git diff  
git add hello.php  
git status -s  
git diff --cached   
```

## 10、git commit  

```
git commit -m 'test comment from w3cschool.cn' 
```

 提交缓存的流程太过繁琐，Git 也允许你用 -a 选项跳过这一步  

```
git add  
git commit -am 'changes to hello file'
```

表示提交的信息中带有署名信息  

```
git commit --signoff -m 'xxx'  
```

表示对上一次提交的信息,进行修改提交  

```
git commit --amend 'xxx'  
```

## 11、git rm  
将文件从缓存区中移除  

```
git rm  
git rm hello.php
```

将文件从缓存区和你的硬盘中（工作目录）删除。 如果要在工作目录中留着该文件  

```
git rm file  
git rm --cached   
```

## 12、git log  

```
git log  查看提交历史  
git log --oneline            --oneline 选项来查看历史记录的简洁的版本  
git log --oneline --graph    -graph 选项，查看历史中什么时候出现了分支、合并。  
git log --reverse --oneline  '--reverse'参数来逆向显示所有日志  
git log --author=Linus --oneline -5   --author , 例如，比方说我们要找 Git 源码中 Linus 提交的部分  
git log --oneline --before={3.weeks.ago} --after={2010-04-18} --no-merges 
```

## 13、git tag  
查看所有标签  

```
git tag
```

-a选项意为“创建一个带注解的标签”。不用-a选项也可以执行，但它不会记录这标签是啥时候打的，谁打的，也不会让你添加标签的注解 

```
git tag -a v1.0  
git log --online --decorate --graph  --decorate 时，我们可以看到我们的标签  
```

追加标签  

```
git tag -a v0.9 85fc7e7  
git log --oneline --decorate --graph  
```

指定标签信息命令  

```
git tag -a  -m "w3cschool.cn标签"
```

PGP标签命令  

```
git tag -s  -m "w3cschool.cn标签"
```

查看版本：  

```
git tag
```

创建版本：  

```
git tag [name]  
```

删除版本：  

```
git tag -d [name]  
```

查看远程版本：  

```
git tag -r  
```

创建远程版本(本地版本push到远程):  

```
git push origin [name]
```

删除远程版本：  

```
git push origin :refs/tags/[name] 
```

 合并远程仓库的tag到本地：  

```
git pull origin --tags  
```

上传本地tag到远程仓库：  

```
git push origin --tags
```

创建带注释的tag：  

```
git tag -a [name] -m 'yourMessage'   
```

# 二、Git与SVN比较  

SVN是当前使用最多的版本控制工具。与它相比，Git最大的优势在于两点：易于本地增加分支和分布式的特性。  
![image](https://raw.githubusercontent.com/aqjsp/Pictures/main/202401172149000.png)  

## 1、本地增加分支  

图中Git本地和服务器端结构都很灵活，所有版本都存储在一个目录中，你只需要进行分支的切换即可达到在某个分支工作的效果。  
而SVN则完全不同，如果你需要在本地试验一些自己的代码，只能本地维护多个不同的拷贝，每个拷贝对应一个SVN服务器地址。  
举个例子：  
使用SVN作为版本控制工具，当正在试图增强一个模块，工作做到一半，由于会改变原模块的行为导致代码服务器上许多测试的失败，所以并没有提交代码。
这时候假如现在有一个很紧急的Bug需要处理， 必须在两个小时内完成。我只好将本地的所有修改diff，并输出成为一个patch文件，然后回滚有关当前任务的所有代码，再开始修改Bug的任务，等到修改好后，在将patch应用回来。前前后后要完成多个繁琐的步骤，这还不计中间代码发生冲突所要进行的工作量。
可是如果使用Git， 我们只需要开一个分支或者转回到主分支上，就可以随时开始Bug修改的任务，完成之后，只要切换到原来的分支就可以优雅的继续以前的任务。只要你愿意，每一个新的任务都可以开一个分支，完成后，再将它合并到主分支上，轻松而优雅。  
## 2、分布式提交  

Git 可以本地提交代码，所以在上面的图中，Git有利于将一个大任务分解，进行本地的多次提交；  
而SVN只能在本地进行大量的一次性更改，导致将来合并到主干上造成巨大的风险。  
## 3、日志查看  

Git 的代码日志是在本地的，可以随时查看；  
SVN的日志在服务器上的，每次查看日志需要先从服务器上下载下来。  
例如：代码服务器在美国，当每次查看几年前所做的工作时，日志下载可能需要十分钟，这不能不说是一个痛苦。但是如果迁移到Git上，利用Git日志在本地的特性，查看某个具体任务的所有代码历史，每次只需要几秒钟，大大方便了工作，提高了效率。  
当然分布式并不是说用了Git就不需要一个代码中心服务器，如果你工作在一个团队里，还是需要一个服务器来保存所有的代码的。  
