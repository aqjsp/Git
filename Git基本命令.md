# Git  
### 必知必会的Git命令  

#### git checkout -b xxx

git checkout xxx是指切换到xxx相当于复制了remote的仓库到本地的xxx分支上，-b就是branch，即创建新的分支，所以这条指令的意思就是创建并切换到xxx。  

#### git diff 

查看自己对代码做出的改变，也就是查看暂存区与disk区文件的差异。  

#### git add xxx

将xxx文件添加到暂存区。  

#### git commit

将暂存区内容添加到local区的当前分支。  

#### git push

将local去的LocalBranchName分支推送到RemoteHostName主机的同名分支（若加-f表示无视本地与远程分支的差异强行push）。  

#### git branch -d xxx

删除本地的git分支；git branch -D xxx：不加-D表示创建新的local分支xxx，加-D表示强制删除local分xxx。  

#### git pull

同上，不过改成从远程主机下载远程分支并与本地同名分支合并。  

#### git rebase xxx

假设当前分支与xxx分支存在共同部分common，该指令用xxx分支包括common在内的整体替换当前分支的common部分（原先xxx分支内容为common->diversityA，当前分支内容为common->diversityB，执行完该指令后当前分支内容为common->diversityA->disverityB）。  

#### git checkout main

切换回main分支。  

#### git checkout xxx

回到xxx分支。  

#### git pull origin master(main)

将远端修改过的代码再更新到本地。  

#### git base main

我在xxx分支上，先把main移过来，然后根据我的commit来修改成新的内容（中途可能会出现，rebase conflit ---> 手动选择保留哪段代码）。  

#### git push -f origin xxx

把rebase后并且更新过的代码再push到远端github上（-f ---> 强行）。  
