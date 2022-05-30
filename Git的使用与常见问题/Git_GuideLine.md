[TOC]

# 00 关于工具的配置

## 01 Git 与 GitHub的配置（Ubuntu）

1. 检查`Git`的安装

   ```shell
   # Git的安装
   sudo apt install git
   
   # 检查
   dargon@dd:~/桌面$ git version
   git version 2.25.1
   ```

2. `Git`与`github`是通过`ssh`生成的公钥与秘钥进行授权的，想要在本地与`github`上的仓库进行连接，就需要分别配置两者的联系

3. ```shell
   # 生成SSH key
   dargon@dd:~$ ssh-keygen -t rsa
   Generating public/private rsa key pair.
   Enter file in which to save the key (/home/dargon/.ssh/id_rsa): 
   Enter passphrase (empty for no passphrase): 
   Enter same passphrase again: 
   ```

4. 把生成的`id_rsa.pub`公钥内容，赋值添加到`Github`上面，这样本地的秘钥才可以与`github`上的公钥进行匹配授权

5. 验证连接是否成功

   ```shell
   dargon@dd:~$ ssh -T git@github.com
   Hi Dargon0123! You've successfully authenticated, but GitHub does not provide shell access.
   ```

6. 以上完成`Git`与`github`的绑定

# 01 本地仓库常用命令

1. ```shell
   git init 
   # 本地初始化一个文件夹，为gii仓库，初始化完成之后，文件夹中会多出.git 文件
   ```

2. ```shell
   git status
   # 显示仓库的状态信息，查看仓库的状态
   ```

3. ```shell
   git add
   # 将本地仓库的新开发的文件，通过add 命令添加搭到，[仓库缓冲区]的地方，此时还未提交到仓库，等待commit
   git add . 
   # 针对该本地仓库中，多个新开发的文件，进行一次性添加到 缓冲区
   ```

4. ```shell
   git commit -m "text message"
   # 正式将[仓库缓冲区]的文件，提交到该本地仓库,等待push 到远端仓库，即是github 上面
   ```

5. ```shell
   git log
   # 打印出 仓库的提交日志，是一个完整的提交记录，包括 author date and commit message
   
   git log -1 HEAD
   # 打印出上次commit的一个完整记录，包括author，date，commit message
   
   git log --oneline
   # 打印上次一条 commit message
   ```

6. ```shell
   git branch
   # 查看当前仓库的分支，*master 意味着当前所在的分支
   
   git branch -a
   # 查看当前仓库中所有以及隐藏的分支
   
   git branch a 
   # 新建分支a 
   
   git checkout -b b
   # 新建分支 b 并且切换到分支b 
   ```

7. ```shell
   git checkout [分支名]
   # git checkout a ; 切换到分支a
   # git checkout master ; 切换到分支master
   ```

8. ```shell
   git merge [分支名]
   # 将分支切换到 master
   # git merge a ; 合并a 分支到master
   # note: 合并的两个分支内容不能有冲突，否则合并不成功
   ```

9. ```shell
   git branch -d [分支名]
   # 删除该分支
   ```

10. ```shell
    git tag [标签名]
    # git tag v1.0 ; 给当前分支 add 标签名
    # 方便查找 git checkout v1.0 就相当于 git checkout [该分支]
    ```

11. ```shell
    gitk --all &
    # 查看当前的仓库的关系
    ```

12. 

## 02 与远程仓库交互

1. ```shell
   git push origin master
   # 将本地代码仓库推到远程仓库，保持两者同步
   ```

2. ```shell
   git pull origin master
   # 将远程仓库代码拉到本地，保持同步
   ```

3. 在本地没有仓库，先在clone出一个仓库，下面就是在本地仓库上进行的开发，然后add，commit，最终push到远程仓库上面

   ```shell
   git clone [Github仓库地址]
   # 针对本地没有仓库，将该仓库克隆到本地
   ```

4. 本地有仓库，先初始化，再**关联远程仓库**， `origin`是默认的远程仓库的名字 ，开发，提交，最终push

   ```shell
   git remote add origin [仓库地址]
   # 关联远程仓库，同步本地与远程的信息
   
   git pull origin master
   # 同步两个仓库的代码
   ```

5. 更新/删除仓库中的文件，先将远程仓库拉过来，然后本地删除相应的文件，后面紧接着`add, commit，push`结束操作。 

5. 删除远程仓库中的某个分支

   ```shell
   git push origin :[分支名]
   # 直接删除远程仓库中该分支
   ```

## 03 合并`Github`上的两个分支

1. 一般地，在本地进行`git clone`命令时候，默认是`clone`到的远程仓库的`master `分支，合并分支的时候就需要另一个分支，如何在当地拉取另一个分支的内容

   ```shell
   # 01 显示所有的branch
   $ git branch -a
   * master
     remotes/origin/main
     remotes/origin/master
   
   # 02 目录切换到分支main的内容 
   git checkout origin/main 
   
   $ git branch -a
   * (HEAD detached at origin/main)
     master
     remotes/origin/main
     remotes/origin/master
   
   # 03 查看成功切换到main 这里
   git checkout main
   $ git branch
   * main
     master
     
   $ git branch -a
   * main
     master
     remotes/origin/main
     remotes/origin/master
   
   
   # 04 merge
   # 先切换到 branch master
   # occur error
   $ git merge main
   fatal: refusing to merge unrelated histories
   # solve error
   $ git merge main --allow-unrelated-histories
   Merge made by the 'recursive' strategy.
    hit.txt | 1 +
    1 file changed, 1 insertion(+)
    create mode 100644 hit.txt
   # merge successful
   
   $ git push origin master
   # push 到远程仓库
   ```

   





# 02 关于Git工具的使用



```shell
These are common Git commands used in various situations:

start a working area (see also: git help tutorial)
   clone             Clone a repository into a new directory
   init              Create an empty Git repository or reinitialize an existing one

work on the current change (see also: git help everyday)
   add               Add file contents to the index
   mv                Move or rename a file, a directory, or a symlink
   restore           Restore working tree files
   rm                Remove files from the working tree and from the index
   sparse-checkout   Initialize and modify the sparse-checkout

examine the history and state (see also: git help revisions)
   bisect            Use binary search to find the commit that introduced a bug
   diff              Show changes between commits, commit and working tree, etc
   grep              Print lines matching a pattern
   log               Show commit logs
   show              Show various types of objects
   status            Show the working tree status

grow, mark and tweak your common history
   branch            List, create, or delete branches
   commit            Record changes to the repository
   merge             Join two or more development histories together
   rebase            Reapply commits on top of another base tip
   reset             Reset current HEAD to the specified state
   switch            Switch branches
   tag               Create, list, delete or verify a tag object signed with GPG

collaborate (see also: git help workflows)
   fetch             Download objects and refs from another repository
   pull              Fetch from and integrate with another repository or a local branch
   push              Update remote refs along with associated objects

```
