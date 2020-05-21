#git
##将本地仓库上传github
* 在Git Bash控制台上测试一下，输入：ssh -T git@github.com
* git config --global user.name “qingya”
* Git config --global user.email “@qq.om”
* Ssh-keygen -t rsa -C “@example.com”,如果你是windows用户，那么公钥生成的目录是C:\Users\用户名\.ssh下
* Git remote add origin git@github.com:xxxx.git
* Git push origin master
* Git remote -v ，显示项目目前的远程仓库，如果为新建项目则为空    
<p>**备注:**如果初次提交，需要运行命令
>git push --set-upstream origin master   
>git branch --set-upstream-to=origin/master   
>[git branch --set-upstream dev origin/dev](http://blog.csdn.net/forevercjl/article/details/52982356)      
>[git branch --track branch名称 远端branch分支](http://blog.sina.com.cn/s/blog_605f5b4f010194fg.html)

##git使用过程中的问题
###Git error: open(“somefile.VC.opendb”): Permission denied
参考网址：
<https://stackoverflow.com/questions/34975423/visual-studio-2015-git-error-opensomefile-vc-opendb-permission-denied-fa/34979320>

###git无法pull仓库refusing to merge unrelated histories
![](https://i.imgur.com/JBIGRbo.png)

先pull，因为两个仓库不同，发现refusing to merge unrelated histories，无法pull
因为他们是两个不同的项目，要把两个不同的项目合并，git需要添加一句代码，在git pull，这句代码是在git 2.9.2版本发生的，最新的版本需要添加--allow-unrelated-histories.

###git clone
* 本地克隆<p>
在目标文件夹下，启动git bash，运行命令，命令中的路径为被克隆的仓库：  
>git clone /e/selfStudy/gitFile

* 远程克隆<P>
>git clone https://github.com/nlohmann/json.git

###git submodule
* 新建一个空目录，通过git init初始化为git仓库，通过运行   
>git submodule add /e/gitignore  destationFolder     

将目标位置的仓库克隆到本仓库，并将其设置为本仓库的子模块。</p>    

* 克隆带有子模块的git仓库
>方法一：   
>git clone /e/selfStudy/gitFile --recursive    
> 方法二：    
> git clone /e/selfStudy/gitFile   
> cd gitignore   
> git submodule init  
> git submodule update   
![](https://i.imgur.com/ljsVtCR.png)

![](https://i.imgur.com/jF51MOG.png)    
git submodule add git@github.com:forhappy/cpy-leveldb.git

###git push
在git push代码到仓库时，遇到如下错误：
![](https://i.imgur.com/3pwU3D6.png)    
这是由于git默认拒绝了push操作，需要进行设置，修改.git/config文件后面添加如下代码：   
[receive]   
denyCurrentBranch = ignore   

###git init 和git init --bare的具体区别
一般个人使用，用git init，这时候你的工作区也在这里。你要是想建立一个固定的地址让大家一起用，就在服务器上用git --bare init。

其实你可以看到，init建立的.git目录内容和--bare建立的目录内容是差不多的。

在初始化远程仓库时最好使用 git --bare init   而不要使用：git init。这样在使用hooks的时候，会有用处。

如果使用了git init初始化，则远程仓库的目录下，也包含work tree，当本地仓库向远程仓库push时,   如果远程仓库正在push的分支上（如果当时不在push的分支，就没有问题）, 那么push后的结果不会反应在work tree上,  也即在远程仓库的目录下对应的文件还是之前的内容，必须得使用git reset --hard才能看到push后的内容.   

参考网址：<https://my.oschina.net/u/141149/blog/677294>

###git tag
如何取得某一个tag的代码？   
1. git clone 整个代码仓库；      
2. git checkout tag_name可以取得tag对应的代码；         

此时代码处于“detached HEAD"状态，因为tag是一个快照，是不能更改它的代码的，如果需要在tag代码的基础上修改代码，需要新建分支；  
git checkout -b branch_name tag_name

###git diff
基本的git diff输出    

![](https://i.imgur.com/bEzzbGn.png)       

<p>第一行是git diff的header，进行比较的是a版本的.vcxproj（变动前）和b版本的.vcxproj（变动后）。      
第二行是两个版本的hash值以及文件模式（100644表示是文本文件）。     
第三、四行表示进行比较的两个文件，---表示变动前的版本，+++表示变动后的版本。
第五行是一个thunk header（可能会有多个），提供变动的上下文，“-163,6”表示变动前的从163行开始的6行，“+163,7”表示变动后从163行开始的7行。
接下来几行就是具体的变动内容，它将两个文件的上下文合并显示在一起，每一行前面是一个标识为，“ ”（空）表示无变化（是一个上下文行），“-”表示变动后删除的行，“+”表示变动后增加的行。

###git branch 分支重命名
* 重命名本地分支    
重命名当前分支： git branch -m [new name ]           
重命名其他分支：git branch -m [old name] [new name]     

###push到github时，每次都需要输入用户名和密码
<p>问题原因：使用了https方式的push   
在命令行窗口输入：   git remote -v   
![](https://i.imgur.com/SEQbSNU.png)

<p>下面把https换成ssh方式     
1. git remote rm origin    
2. git remote add origin git@github.com:ztchu/testAmbigurity.git    
3. git push --set-upstream origin master    

###删除远程分支
<p>向远程分支推送一个空的本地分支即可:     
**git push origin :OoxmlSerializ1.0.9**

###git apply用法

###git config
<p>设置自动转换换行符   
git config --global core.autocrlf    
git config core.autocrlf     
*设置本地的自动转换，以及全局的自动转换，本地具有更高的优先级。* 
  
<p>查看所有的全局配置  
git config --global -l   
<p>编辑git全局配置参数   
git config --global -e

###获取分支的提交数
* 获取当前分支的提交数    
	git rev-list --count HEAD   
* 获取指定分支的提交数
	git rev-list --count <branch-name>     
[https://stackoverflow.com/questions/11657295/count-the-number-of-commits-on-a-git-branch](https://stackoverflow.com/questions/11657295/count-the-number-of-commits-on-a-git-branch)    


