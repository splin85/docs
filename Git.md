# git 操作

1. `git reset HEAD file`  
    将文件file从暂存区回退到工作区  
    
2. `git reset hard HEAD file`

3. 删除未跟踪的文件  
    `git clean -nf`   //删除未跟踪文件  
    `git clean -nfd`  //连未跟踪的目录一起删除
    
4. 删除本地有但远程没有的分支  
    `git remote show origin`  
    `git remoter prune origin`