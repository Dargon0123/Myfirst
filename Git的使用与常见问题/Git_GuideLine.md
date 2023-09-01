[TOC]

# 🍐0  关于工具的配置

## 0.1 Git 与 GitHub的配置（Ubuntu）

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

## 0.2 Git 与 GitHub的配置（win10）

1. 检查`git`的安装

   ```shell
   $ git
   usage: git [--version] [--help] [-C <path>] [-c <name>=<value>]
              [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
              [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--bare]
              [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
              [--super-prefix=<path>] [--config-env=<name>=<envvar>]
              <command> [<args>]
   ```

2. 检查`ssh`的安装

   ```shell
   $ ssh
   usage: ssh [-46AaCfGgKkMNnqsTtVvXxYy] [-B bind_interface]
              [-b bind_address] [-c cipher_spec] [-D [bind_address:]port]
              [-E log_file] [-e escape_char] [-F configfile] [-I pkcs11]
              [-i identity_file] [-J [user@]host[:port]] [-L address]
              [-l login_name] [-m mac_spec] [-O ctl_cmd] [-o option] [-p port]
              [-Q query_option] [-R address] [-S ctl_path] [-W host:port]
              [-w local_tun[:remote_tun]] destination [command [argument ...]]
   ```

3. 利用`ssh`生成秘钥

   ```shell
   $ ssh-keygen -t rsa
   Generating public/private rsa key pair.
   Enter file in which to save the key (/c/Users/dar/.ssh/id_rsa):
   Created directory '/c/Users/dar/.ssh'.
   Enter passphrase (empty for no passphrase):
   Enter same passphrase again:
   Your identification has been saved in /c/Users/dar/.ssh/id_rsa
   Your public key has been saved in /c/Users/dar/.ssh/id_rsa.pub
   The key fingerprint is:
   SHA256:X4yp5F4DUjmUAE91iZF8ELplb2GxLvRVgmkzF0i7jBM dar@LAPTOP-OR0DR9JU
   The key's randomart image is:
   +---[RSA 3072]----+
   |    ..o+*O+=o..  |
   |     o o=oX+.o   |
   |      o Eo=+.    |
   |       * X B     |
   |      o S X o    |
   |       + B .     |
   |        o +      |
   |       . . .     |
   |        .        |
   +----[SHA256]-----+
   ```

4. 在`github`网页上进行配置

   ```shell
   
   dar@LAPTOP-OR0DR9JU MINGW64 ~/Desktop
   $ ssh -T git@github.com
   ssh: connect to host github.com port 22: Connection refused
   
   
   dar@LAPTOP-OR0DR9JU MINGW64 ~/Desktop
   $ ssh -T git@github.com
   The authenticity of host 'github.com (140.82.114.4)' can't be established.
   ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
   This key is not known by any other names
   Are you sure you want to continue connecting (yes/no/[fingerprint])?
   ```

   



# 🍋1 常用命令

## 1.1 本地仓库

1. 初始化
   
   ```shell
   git init 
   # 本地初始化一个文件夹，为gii仓库，初始化完成之后，文件夹中会多出.git 文件
   ```
   
2. 查看仓库状态，常用操作
   
   ```shell
   git status
   # 显示仓库的状态信息，查看仓库的状态
   ```
   
3. 添加新开发文件
   
   ```shell
   git add
   # 将本地仓库的新开发的文件，通过add 命令添加搭到，[仓库缓冲区]的地方，此时还未提交到仓库，等待commit
   git add . 
   # 针对该本地仓库中，多个新开发的文件，进行一次性添加到 缓冲区
   ```
   
4. 提交到仓库
   
   ```shell
   git commit -m "text message"
   # 正式将[仓库缓冲区]的文件，提交到该本地仓库,等待push 到远端仓库，即是github 上面
   ```
   
5. 输出`git`日志信息
   
   ```shell
   git log
   # 打印出 仓库的提交日志，是一个完整的提交记录，包括 author date and commit message
   
   git log -1 HEAD
   # 打印出上次commit的一个完整记录，包括author，date，commit message
   
   git log --oneline
   # 打印上次一条 commit message
   ```
   
6. 查看分支
   
   ```shell
   git branch
   # 查看当前仓库的分支，*master 意味着当前所在的分支
   
   git branch -a
   # 查看当前仓库中所有以及隐藏的分支
   
   git branch a 
   # 新建分支a 
   
   git checkout -b b
   # 新建分支 b 并且切换到分支b 
   ```
   
7. 切换分支
   
   ```shell
   git checkout [分支名]
   # git checkout a ; 切换到分支a
   # git checkout master ; 切换到分支master
   ```
   
8. 合并
   
   ```shell
   git merge [分支名]
   # 将分支切换到 master
   # git merge a ; 合并a 分支到master
   # note: 合并的两个分支内容不能有冲突，否则合并不成功
   ```
   
9. 删除分支
   
   ```shell
   git branch -d [分支名]
   # 删除该分支
   ```
   
10. 打标签
    
    ```shell
    git tag [标签名]
    # git tag v1.0 ; 给当前分支 add 标签名
    # 方便查找 git checkout v1.0 就相当于 git checkout [该分支]
    # 详情参考 git 官方网站 [git tags 标签使用方式](https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E6%89%93%E6%A0%87%E7%AD%BE)
    ```
    
11. [Git 基础 - 打标签](https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E6%89%93%E6%A0%87%E7%AD%BE)
    
11. 查看关系（暂时没有用过这个）
    
    ```shell
    git --all &
    # 查看当前的仓库的关系
    ```
    
13. 

## 1.2 与远程仓库交互

1. 推代码到云端仓库
   
   ```shell
   git push origin master
   # 将本地代码仓库推到远程仓库，保持两者同步
   ```
   
2. 拉代码从云端仓库
   
   ```shell
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
   # 第一步先关联
   git remote add origin [仓库地址]
   # 关联远程仓库，同步本地与远程的信息
   
   # 第二步直接同步远程仓库的代码到本地
   git pull origin master
   
   # 后面在进行add commit 提交本地代码到仓库中
   ```

5. 更新/删除仓库中的文件，先将远程仓库拉过来，然后本地删除相应的文件，后面紧接着`add, commit，push`结束操作。 

5. 删除远程仓库中的某个分支

   ```shell
   git push origin :[分支名]
   # 直接删除远程仓库中该分支
   ```

## 1.3 合并`Github`上的两个分支

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

   





# 🍑2 关于Git工具的使用

* 常用

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

* `Branch ` 操作

早建分支，多用分支！

创建再多的分支也不会造成储存或内存上的开销，并且按逻辑分解工作到不同的分支，要比维护那些特别臃肿的分支简单多了。

```shell
git branch newBranch
# 建立新分支
```

```shell
git checkout newBranch; 
# 切换到新分支
```

```shell
git checkout -b newBranch
# 创建一个分支，并且切换过去
```

* `merge` 合并操作

```shell
git merge bugFix
# 在当前 main 分支下，把bugFix合并到main里面，出现一个新的节点，同时包含两个 parent 节点
# 后续，再将 main 分支合并到 bugFix里面
```

```shell
git checkout bugFix; git merge main;
# 这样每一个分支都包含了代码库的所有修改
```

* `rebase` 合并操作

```shell
git rebase main
# 注意，在当前bugFix分支下，执行之后，将bugFix分支的工作，rebase到main分支上
# 但是 main还没有更新

git checkout main; git rebase bugFix;
# 切换分支到main上，然后rebase即可
```



* `HEAD` 分离说明

```shell
git checkout main^
# 返回 [HEAD]，其中一个 ^ 表示返回上一级别, ~3表示返回上三层
# ^ 向上增加，只能用 分支名 + ^ ,不能使用 C3^这类提交名字作为操作
```

```shell
git branch -f main HEAD~3
# 将main 分支，强制指向 HEAD 的第三级 parent提交，只允许在 [HEAD]的节点基础上进行移动操作。
```

* 撤销变更

```shell
git reset HEAD~1
# 通过把分支记录回退 1 个提交记录来实现撤销改动。该指令向上移动一个分支，原来指向的提交记录就跟从来没有提交过一样，称之为"改写历史"，使得本地代码根本不知道有这回事。
# 仅在自己的本地有效
c0 <-- c1 <-- c2[HEAD]
|
c0 <-- c1[HEAD]
```

```shell
git revert HEAD
# 也是变更，可以共享，
c0 <-- c1 <-- c2[HEAD]
|
c0 <-- c1 <-- c2 <-- c2'[HEAD]
# 其中 c2'是和c1的状态是同样的，把撤销c2 操作当作是一次提交。
```

##  移动提交记录

前面学习了 `Git`的基础知识 -- 提交、分支以及在提交树上移动。这些概念涵盖了`90%`的功能，同样也足够满足开发者的日常需求。

下面来学习这 `10%`的操作 ，去处理复杂的工作流。

* `git cherry-pick Ci` 整理提交记录

讨论整理提交记录，开发人员有时会说，

> "我想要把这个提交放到这里，那个提交放到刚才那个提交的后面。"

```shell
git cherry-pick C2 C4
# 可以将 其它分支上的 不连续 C2 C4，复制（抓过来）放到当前的分支下了。
# 前提是，当你知道自己所需要的提交记录（如C2，C4，或者知道这些提交记录的哈希值）
# 非常值得推荐使用 cherr-pick命令
```

假如不知道自己所需要的提交记录，使用交互式的`rebase`来解决

```shell
git rebase -i HEAD~4
# -i --> interactive? 会相应调出一个交互界面，选出自己需要提交即可
```



```shell
git rebase -i # 排序到最前
git commit --amend # 进行修改
git rebase -i # 调回原来顺序
# 把main修改到最前端

```





