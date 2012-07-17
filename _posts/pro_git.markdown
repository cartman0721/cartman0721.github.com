Title: pro git 学习记录
Author: Dazuo Sun
Date: Sat March 24 2012 15:37:00 GMT+0800 (China Standard Time)
Lang: git

   
   花了两个小时简单看了下这本书的前几章，为的是以后用起来更顺手一些，好记性不如烂笔头，顺手做些笔记。原书见http://progit.org/book/

## 一.关于svn 与 git的区别

   从原理上讲，svn和git最大的区别在于svn存的是difference，git存的是snapshot。git会在reversion A 和 reversion B下对同一个文件存多份（当这个文件在reversion A 和 reversion B下存在差异的时候），而svn不会，svn存的是这个文件从版本A到版本B的差异。
   理解这一点对后续理解git命令非常有帮助，比如git commit 不是将代码提交到server端，而是在本地将代码打一个snapshot。通常通过git提交代码需要这几步：
      
      1.git add  
   将文件纳入git管理范围之内，这个svn add 起到的效果是一样。
   
      2.git commit  
   注意这一步不是将代码提交到服务器端，这个命令是将本地的代码打一个snapshot。git的强大的之处在于有一天即便你存代码的服务器挂掉了，你也可以通过本地的文件恢复到服务器上。所以你可以想象成你本地也有个git代码库，commit命令只是把你的代码提交到本地的那个库而已。
      
      3.git push origin master 
   这个命令才是真正将你本地的代码提交到server端。
   origin 是代码分支的别名，通过这个命令  
      
      git remote add origin git@github.com:username/Hello-World.git 
   将orign别名为git@github.com:username/Hello-World.git
   master 是分支名，在git中属于主干，相当于svn中的trunk。
   所以这个命令式将代码提交到git@github.com:username/Hello-World.git的master主干上。
## 二.一些常用的命令

主要是第二章的摘录，如果你也像我一样只是想简单用用git，阅读第二章就已经足够了，用文章的原话说
If you can read only one chapter to get going with Git, this is it。
除了上面讲的这三个命令以外

    1.git init 
   初始化，生成.git文件夹 跟svn 的init一样

    2.git clone git://github.com/schacon/grit.git 
   下载代码，相当于svn checkout，值得注意的是git check out 别有用途，别和svn checkout 搞混了。后续会讲到这个命令的用途。

    3.git status 
   显示当前文件夹下文件被git跟踪的情况

    I：untracked：文件没有被纳入git管理，需要用git add

    II：to be commited,文件被纳入git管理了却没有被提交，需要git commit（没有被打snapshot）。
    
    III：nothin to be commit，这种情况说明本地已经被打了snapshot，下一步可以用git push 将代码push到你想要的分支上。
   <br>
   
    4.git commit -a -m "test" 
   这是一个非常有用的命令，在理解了git commit是将本地代码打一个快照之后，git commit -a 就是讲本地所有修改或者删除的文件打一个快照（所有文件鼻息是tracked，否则就要先使用git add），为git push 做准备。
    
    5.git log 
   查看每次commit的日志。
    
    6.git branch 
   查看当前所在到分支如：如目前就在master分支下面，在哪个分支下和push无关，因为push到时候反正是要指定分支的，但与pull和fetch有关。

    cartman@ubuntu:~/workshop/nodejs_beginner$ git branch
    * master
    merge2
    nodejs_beginner
<br>

    7. git branch -D merge2
   删除分支：
   
    cartman@ubuntu:~/workshop/nodejs_beginner$ git branch -D merge2
    Deleted branch merge2 (was eb013c8)。
   这只是在本地删掉而已，还要push到服务器
   
    cartman@ubuntu:~/workshop/nodejs_beginner$ git push origin :merge2
    Username for 'https://github.com': cartman0721
    Password for 'https://cartman0721@github.com':
    To https://github.com/cartman0721/nodejs_beginner
    - [deleted] merge2
   <br>
   
    8.git reomte -v 
   查看项目路径

    9.git fetch
   这个命令拉取不对冲突做任何处理
   
    10.git pull
   会标记错误：如
   
    C:\work\mycode\nodejs\beginner>git pull origin master
    From github.com:cartman0721/nodejs_beginner
    * branch            master     -> FETCH_HEAD
    Auto-merging tt.txt
    CONFLICT (content): Merge conflict in tt.txt
    Automatic merge failed; fix conflicts and then commit the result.
   tt.txt变成下边的摸样：
   
    <<<<<<< HEAD
    ddddttttt
    test from cartman@windows
    =======
    ddddddddd
    test from cartman@ubantu
    >>>>>>> eb013c8ae7e04eb082564e4214613c14e1091e85


