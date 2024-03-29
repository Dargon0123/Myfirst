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

   

## 0.2 Git的全局配置

1. 设置默认的文本编辑器 `vim` 

```shell
git config --global core.editor "vim"
```

这会将全局的`Git` 配置中的默认编辑器更改为 `vim` 

2. 设置默认配置提交信息模板`git commit message` 

```bash
# 1 创建提交模板文件，必须是 .xxx 开头的文件
# 路径不固定，比如 ~ 是桌面开始； / 表示根目录
 touch ~/.gitmessage

# 2 编辑提交模板文件
vim ~/.gitmessage

# 类型: <类型>
# 描述: <描述>
# 问题编号: <问题编号>
#
# 例子：
# 类型: 修复
# 描述: 修复了一个关于登录页面的样式问题
# 问题编号: #123

# 3 配置 Git 使用该提交模板
git config --global commit.template ~/.gitmessage
```

这样设置之后，当你每次运行 `git commit` 之后，会自动在提交描述上使用该模板信息，将会按照模板规范填写信息。

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

   





# 🍑2 `Git`本地使用

## 2.0  常用`90%`的操作

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

## 2.1 `branch ` 操作

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

```bash
git branch -a
# 查看所有分支，包括本地、远程分支
```

```bash
git ls-remote --heads origin
# 查看远程仓库的分支名字
```

问题描述：当该本地分支有改变，增添等操作的时候，1）需要先提交之后，才能切换到别的分支上；2）暂存本地更改

```bash
# way 01
$ git checkout feature2

error: Your local changes to the following files would be overwritten by checkout:
        Git的使用与常见问题/Git_GuideLine.md
Please commit your changes or stash them before you switch branches.
Aborting
# 需要先提交本地的改变之后，才能 checkout 其它分支
```

```bash
# way 02
$ git stash
Saved working directory and index state WIP on feature2: 81f4e0e solve merge confliction
# feature2* 将把更改保存在一个临时存储区中，并将工作目录恢复到干净的状态，
# 一边切换到其他分支

# 完成其他分支操作后，再切换到分支feature2上
git checkout feature2;
git stash apply;
# 恢复之前的分支

# 或者，在应用暂存的更改后，删除暂存，可以使用
git stash pop; #(暂且未进行实验)
```



## 2.2 `merge` 合并操作

```shell
git merge bugFix
# 在当前 main 分支下，把bugFix合并到main里面，出现一个新的节点，同时包含两个 parent 节点
# 后续，再将 main 分支合并到 bugFix里面
```

```shell
git checkout bugFix; git merge main;
# 这样每一个分支都包含了代码库的所有修改
```

## 2.3 `rebase` 合并操作

```shell
git rebase main
# 注意，在当前bugFix分支下，执行之后，将bugFix分支的工作，rebase到main分支上
# 但是 main还没有更新

git checkout main; git rebase bugFix;
# 切换分支到main上，然后rebase即可
```

```shell
git rebase mian bugFix
# 当前分支在 main*， 合并 bugFix 分支到 main 分支里面
# 可以直接 使用两个分支名字进行合并操作
```



## 2.4 `HEAD` 分离说明

```shell
git checkout main^
# 返回 [HEAD]，其中一个 ^ 表示返回上一级别, ~3表示返回上三层
# ^ 向上增加，只能用 分支名 + ^ ,不能使用 C3^这类提交名字作为操作
```

```shell
git branch -f main HEAD~3
# 将main 分支，强制指向 HEAD 的第三级 parent提交，只允许在 [HEAD]的节点基础上进行移动操作。
```

## 2.5  `reset/revert`撤销提交

```shell
git reset HEAD~1
# 通过把分支记录回退 1 个提交记录来实现撤销改动。该指令向上移动一个分支，原来指向的提交记录就跟从来没有提交过一样，称之为"改写历史"，使得本地代码根本不知道有这回事。
# 仅在自己的本地有效
# Vscode的git插件，支持本地进行直接的撤销操作
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

## 2.6 `git stash`高阶用法

在切换 `branch `的`2.1 branch 操作`小节中，提到了`stash`的用法，你可以将它理解为一种栈的使用方法。

使用场景：

当你在本地开发自己负责部分的代码之后，想要提交到远程仓库上。这时，其它人肯定先你之前，提了很多笔代码，就是你本地的代码，并不是最远端仓库上最新的。直接提交，必定产生冲突。

解决这个问题，首先，你需要先和远端仓库代码进行同步。同步之前，需要先暂存一下本地的代码，这时候就需要使用 `git stash`的操作了。

1. 保存：`git stash save "save message"` 可以`stash`的时候，附带上自己的信息；
2. 查看：`git stash list` 查看当前  栈中，有多少`stash`在等待操作
3. 弹出：`git stash pop`弹出栈中最上面的那个 `=` `git stash pop stash@{0}`的操作， 应用并弹出第二个，则是 `git stash pop stash@{1}`
4. 应用：`git stash apply stash@{n}`，只是应用该`satsh`，不需要从栈中进行弹出来，表示是其它分支，也可以使用该`stash`了。
5. 删除：所有的`list`使用，`git stash clear`；删除指定的`list`，使用 `git stash drop stash@{0}` 字面意思即是 `drop`拖拽下来一个`list`项。

关于 `stash`的一些状态描述：当我们工作区的本地之前存在，当前进行了修改，且没有进行`add`的文件，也可被 `stash`进去栈中暂存；但是，新建的文件，未被追踪的文件，则不能被`stash`到栈中，需要先`add`到缓存区里才可以。



## 2.7 `git checkout`高级用法

在工作中一次 `commit`失败之后，需要中心退回操作

1. 首先使用 `git reset --soft HEAD~`来退回上次的 `commit`之前的那个操作
2. 回退之后，所有的文件在`staged`暂存区，即全是`add .` 之后的状态
3. 使用`git restore --stage <文件>`以取消暂存，回到`add .` 之前的原始状态
4. 使用 `git checkout <文件>`来放弃对这个文件的修改

#  🥭3 `Git`移动使用

前面学习了 `Git`的基础知识 -- 提交、分支以及在提交树上移动。这些概念涵盖了`90%`的功能，同样也足够满足开发者的日常需求。

下面来学习这 `10%`的操作 ，去处理复杂的工作流。

## 3.1 `git cherry-pick Ci` 整理提交记录

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

* 提交的技巧`1`：使用`git rebase -i HEAD~[n]`

```shell
git rebase -i HEAD~2 
# 排序到最前

git commit --amend 
# 进行修改提交

git rebase -i HEAD~2 
# 调回原来顺序

git branch -f main HEAD
# 把main修改到最前端

```

* 提交的技巧`2`：使用`git cherry-pick`

由于在技巧`1`中的操作，使用`rebase -i`需要对提交记录进行两次重新排序，可能造成由`rebase`而导致的冲突，所以，还是需要学习`cherry-pick`操作来看看。

心里牢记 `cherry-pick` 可以将提交树上的任何地方的提交记录，取过来追加到`HEAD`上（只要不是`HEAD`上游的提交就没问题）

```shell
git cherry-pick C2
# 注意，不能抓取当前分支 上游的提交记录
```

## 3.2 `git tag`操作

他们可以（在某种程度上 -- 因为标签可以被删除后，重新在另外一个位置创建同名的标签）永久地将某个特定的提交命名为里程碑，然后就可以像分支一样引用了。

且会随着新的提交而移动。你也不能切换到某个标签上面进行修改提交，它就像是提交树上的一个锚点，标识某个特定的位置。

```shell
git tag v1 C1
# 将这个标签 v1，明确指向提交C1。如果不指定位置，默认是选择当前HEAD所指向的位置
```

## 3.3 `git describe`操作

由于`tag`在代码库中起着[锚点]的作用，`Git`专门为此设计了一个命令用来**描述离你最近**的锚点（也就是标签）。

`git describe`能帮你在提交历史中，移动了多次以后找到方向。

语法：

```shell
git describe <ref>
# <ref>可以是任何能被 git 识别成提交记录的引用，若没有指定的话，Git会使用你目前所在的位置[HEAD]。

# 输出的结果
<tag>_<numCommits>_g<hash>
# <tag> 是离<ref> 最近的标签，<numCommits> 是<ref> 与 <tag> 相差有多少个提交记录，<hash> 表示 <ref> 的提交记录哈希值的前几位。

# 当 <ref> 提交记录上有某个标签是，则之输出标签名称。

```

# 🍏4 `Git`高级话题

## 4.1 多分支 `rebase` 

```shell
# 同上操作

git rebase main bugFix
# 当前分支在 main*， 合并 bugFix 分支到 main 分支里面
# 可以直接 使用两个分支名字进行合并操作
```

* 使用操作数`~`和`^`，来选择 `parent` 提交记录

`~[nums]` 表示向上追`nums`个提交记录；

`^[nums]` 则是改变这一默认向上追踪的路径。

```shell
git checkout main^
# 正常使用方法，默认(合并提交的第一个 parent)在main 这条线上追

git checkout main^2
# ^ + [nums] 可以改变上述默认追溯行为
# 可以合并前的分支上移动，加上 ^2 ，则改变这一默认追踪线路
```

```shell
git checkout HEAD~
# 向上移动一个
git checkout HEAD^2
# 改变到 分支追溯
git checkout HEAD~2
# 连续追溯

git checkout HEAD~^2~2
```

答案

```shell
git branch bufWork main^^2^
# main*, 直接使用 ^ 向上走一个，^2 切换到其它分支，^ 在向上索引一个
# git branch 直接建立新分支
```

## 4.2  `cherry-pick`纠缠不清的分支操作

把`main`分支上的最近几次提交做不同的调整后，分别添加到各个的分支上。

1. `one`需要重新排序并删除 `c5` ，

2. `two`仅需要重新排序

3. `three`需要提交一次。

```shell
git checkout one;
git cherry-pick c4 c3 c2;
# 处理 one 分支，直接使用cherry-pick进行抓取

git checkout two;
git cherry-pick c5 c4 c3 c2;
# 处理 two 分支，直接使用cherry-pick进行抓取

git branch -f three c2
# 直接移动到 c2 即可
```

# 🍓5 `Git`远程仓库

他们实际上只是你的仓库在另外一台计算机上的拷贝，你可以通过因特网与这台计算机通信 -- 也就是增加或是获取提交记录

远程仓库的特性：

1. 远程仓库是一个强大的备份；
2. 远程让代码更加社交化。

下面根据概念熟悉远程仓库的操作

* 远程分支

```shell
git checkout o/main; git commit;
# 切换到远程分支 自动进入分离 HEAD 状态
# 当添加新的提交是 o/main 也不会更新，这是因为
# o/main 只有在远程仓库中相应的分支更新了以后才会更新
```

* 抓取获取

```shell
git fetch
# 会做的2件事
# 从远程仓库中下载本地仓库中缺失的提交记录
# 更新远程分支指针，如 o/main

# 不会做的事
# 并不改变你本地仓库的状态
# 不更新你的本地 main 分支，更不会修改你磁盘上的文件

```

理解上面这几点很重要，执行`git fetch`之后，不是本地仓库就与远程仓库同步了。

其只是单纯的下载操作而已。

## 5.1 `git pull`同步远程仓库的操作

由于先抓取数据`git fetch`，再重新合并到本地分支这个流程很常用，因此`Git`专门提供 `git pull`一条命令来完成如下两个命令的操作

```shell
git fetch;
# main* 分支上，一个单纯的下载操作
# 将o/main 分支与远程仓库的分支保持同样

git merge o/main;
# 将 o/main 分支与本地 main 分支进行合并
# merge 操作本身会出现一个新节点，包含两个分支的parent
```

```shell
git pull
# 就是完成上述两个命令的操作
```

* `git fakeTeamwork`模拟队友在远程仓库上的操作

```shell
git clone
# 克隆仓库

git fakeTeamwork main 2
# 在刚创建的远程仓库模拟一些操作: 假装在远程仓库上提交了2次

git commit
# 在自己的本地分支做一些提交

git pull <==> git fetch + git merge
# 再拉取远程仓库的变更
```

* `git push`提交代码到远程仓库上

```shell
git push
# 将本地代码push 到远端仓库上
# 本地分支main 和o/main 也是同步
```

## 5.2 `pull --rebase`偏离的细节

工作中最常见的问题（面试中好像被问到过）

>假设你周一`git clone` 一个仓库，然后开始研发某个新功能。到周五时，你的新功能开发测试完毕，可以发布了。
>
>但是，你的同事这周写了一堆代码，更改了许多你的功能中使用的`API`，使得你的新开发的功能变得不可用。并且你的同事已经`push`到远程仓库了。
>
>导致，你的工作就变成了基于**旧版**项目的代码了，与远程仓库最新的代码不匹配了。

这种情况下执行`git push`，出现未知操作了，是直接让远程仓库回到星期一那天的状态码？还是直接在新代码的基础上添加你的代码？还是直接忽略你的提交？

`Git`会要求你，先`git pull`同步远程仓库的代码，再推送你的代码。

```shell
git fetch;
# 更新本地仓库的 o/main 分支

git rebase o/main;
# main* 将本地main分支的提交，移动到最新的 o/main分支下
# rebase是将当前分支，合并到 目标分支上
# 而 merge 是将目标分支，合并到 当前分支上来

git push;
# 两者同步后，合并到远端仓库
```

同样也可以使用`git merge`进行合并操作

```shell
git fetch;
# 更新本地仓库的 o/main 分支

git merge o/main;
# main* 合并新变更到本地分支main上来

git push;
# 两者同步后，合并到远端仓库
```

简写命令

```shell
git pull --rebase <==> git fetch + git rebase
```

🥲个人感觉，还是把最新的代码拉过来，将自己的提交保证到远程的最新基础上（但是这个时候，会出现新更新的库代码，影响了自己新功能的使用啊，我认为这一点没有解决），最后，`git push`到远端即可。

### 例1：添加文件:

1. 首先其它的本地仓库，对分支`origin/feature2`添加一个`test`文件，`commit、push`到远端仓库。

2. 然后，在自己本地进行对分支`origin/feature2`在添加一个`test2`文件，`commit`之后，`push`到分支`origin/feature2`会出现错误

   ```bash
   $ git push origin feature2
   
   To github.com:Dargon0123/Myfirst.git
    ! [rejected]        feature2 -> feature2 (fetch first)
   error: failed to push some refs to 'github.com:Dargon0123/Myfirst.git'
   hint: Updates were rejected because the remote contains work that you do
   hint: not have locally. This is usually caused by another repository pushing
   hint: to the same ref. You may want to first integrate the remote changes
   hint: (e.g., 'git pull ...') before pushing again.
   # 意思是需要你先更新最新的远程仓库到本地
   # 然后，再基于最新的远程仓库 push 你的代码到远端仓库
   
   ```

3. 执行 `git pull --rebase`之后

   ```bash
   $ git pull --rebase
   
   remote: Enumerating objects: 4, done.
   remote: Counting objects: 100% (4/4), done.
   remote: Compressing objects: 100% (1/1), done.
   Unpacking objects: 100% (3/3), 245 bytes | 11.00 KiB/s, done.
   remote: Total 3 (delta 1), reused 3 (delta 1), pack-reused 0
   From github.com:Dargon0123/Myfirst
      2f1a62b..865fb31  feature2   -> origin/feature2
   Successfully rebased and updated refs/heads/feature2.
   # feature* 拉取远端仓库代码，到本地
   # 同时，将本地分支feature2的提交，合并到origin/feature2上
   ```

4. 重新进行`push`

   ```bash
   $ git push origin feature2
   
   Enumerating objects: 3, done.
   Counting objects: 100% (3/3), done.
   Delta compression using up to 20 threads
   Compressing objects: 100% (2/2), done.
   Writing objects: 100% (2/2), 233 bytes | 233.00 KiB/s, done.
   Total 2 (delta 1), reused 0 (delta 0), pack-reused 0
   remote: Resolving deltas: 100% (1/1), completed with 1 local object.
   To github.com:Dargon0123/Myfirst.git
      865fb31..2e527f3  feature2 -> feature2
   # push到远端仓库成功
   ```


### 例2：添加内容，修改冲突

* `git push`失败

1. 首先，其它本地仓库的文件，对分支`origin/feature2``test`文件，添加一些自己的代码，`commit、push`到远端仓库。

2. 然后，自己在不知道前者已经修改了`text`文件后，自己在本地仓库也增添了一些自己的代码。这时候，问题来了，当自己在本地仓库`commit`之后，`push`直接失败

   ```bash
   $ git push origin feature2
   To github.com:Dargon0123/Myfirst.git
    ! [rejected]        feature2 -> feature2 (fetch first)
   error: failed to push some refs to 'github.com:Dargon0123/Myfirst.git'
   hint: Updates were rejected because the remote contains work that you do
   hint: not have locally. This is usually caused by another repository pushing
   hint: to the same ref. You may want to first integrate the remote changes
   hint: (e.g., 'git pull ...') before pushing again.
   hint: See the 'Note about fast-forwards' in 'git push --help' for details.
   
   # push 被 reject ，因为你没有基于最新的仓库，进行push代码的，由于其他仓库贡献者也push了代码待该分支，你需要做的应该首先pull新的代码到自己仓库，再进行提交。
   ```

3. `git pull`拉取最新的代码

   ```bash
   $ git pull origin feature2
   
   remote: Enumerating objects: 5, done.
   remote: Counting objects: 100% (5/5), done.
   remote: Compressing objects: 100% (1/1), done.
   remote: Total 3 (delta 1), reused 3 (delta 1), pack-reused 0
   Unpacking objects: 100% (3/3), 262 bytes | 10.00 KiB/s, done.
   From github.com:Dargon0123/Myfirst
    * branch            feature2   -> FETCH_HEAD
      81f4e0e..bb96018  feature2   -> origin/feature2
   Auto-merging Test.txt
   CONFLICT (content): Merge conflict in Test.txt
   Automatic merge failed; fix conflicts and then commit the result.
   
   # 需要修改相应的冲突
   ```

   ```bash
   kkkkzzzz
   wang menglong test！
   <<<<<<< HEAD
   add content test
   =======
   eeeeee
   >>>>>>> bb96018a035b205793644ba809bf0fdd94531f35
   
   # 修改之后 （将git的提示慈也清理掉）
   kkkkzzzz
   wang menglong test！
   add content test
   eeeeee
   ```

   重新走一遍`add，commit， push`的流程

   ```bash
   $ git commit -m "fix merge conflict"
   [feature2 cbb8f7a] fix merge conflict
   
   $ git push origin feature2
   Enumerating objects: 10, done.
   Counting objects: 100% (10/10), done.
   Delta compression using up to 20 threads
   Compressing objects: 100% (5/5), done.
   Writing objects: 100% (6/6), 594 bytes | 594.00 KiB/s, done.
   Total 6 (delta 2), reused 0 (delta 0), pack-reused 0
   remote: Resolving deltas: 100% (2/2), completed with 1 local object.
   To github.com:Dargon0123/Myfirst.git
      bb96018..cbb8f7a  feature2 -> feature2
   
   # Ok ,解决冲突成功
   ```

   

* `git pull`失败

1. 执行`git pull`命令时，发生了合并冲突，`Git`尝试将远程分支的更改合并到本地分支时，发现与本地分支上已有更改相冲突的情况。

2. 需要进入相应的文件里面，解决合并冲突，通常冲突部分如下

   ```bash
   <<<<<<< HEAD
   本地分支的更改
   =======
   远程分支的更改
   >>>>>>> 远程/分支名
   # 编辑文件，将冲突部分解决为你希望的结果
   # 比如，全部都保留（需要将Git提示删除掉）
   # 只保留如下内容即可
   本地分支的更改
   远程分支的更改
   ```

3. 保存文件后，使用`git add . ` 和 继续`git commit -m "解决合并冲突"`

4. 之后，可以正常使用`git pull/push`这些指令



* 锁定的`main`原则

```shell
git branch feature
git checkout feature
# main* 本地建立新分支，并且切换到该分支

git push
# 新分支推到仓库上

git checkout main;
git reset HEAD~1;
# 切换到main 分支，且后退一步操作,和远程仓库的main 保持一致

git checkout feature 
# 完成操作
```

## 5.3 `Git`远程高级仓库

* `git rebase`合并特性分支

在大型项目中开发人员通常会在（从`main`上分出来的）特性分支上工作，工作完成后只做一次集成。

但是有些开发人员只在`main`上做`push，pull`，这样的话，`main`总是最新的，始终与远程分支`(o/main)`保持一致。

对于接下来的工作流，我们集成了两个步骤：

1.  将特性分支集成到`main`上
2. 推送并更新远程分支。

```shell
git pull --rebase <==> git fetch + git rebase;
git push
# 从远程仓库pull下来，然后将自己的分支合并rebase到远程分支o/main上
# 推送到远程仓库
```

```shell

# Task！

git pull --rebase
# 拉去远程新的分支，更新本地的o/main分支

# BOSS 3个特性分支 -- side1，side2，side3
git checkout side1;
git rebase main;
git checkout main;
git rebase side1;
# 将side1合并到 main分支，并更新main

git checkout side2;
git rebase main;
git checkout main;
git rebase side2;
# 将side2合并到 main分支，并更新main

git checkout side3;
git rebase main;
git checkout main;
git rebase side3;
# 将side3合并到 main分支，并更新main

git push
# 按顺序推送到远程仓库
# 远程仓库被更新过来，需要把那些工作合并过来
```

简洁办命令操作

```shell
git fetch;
# 仅从远程仓库下载到本地

git rebase o/main side1;
# 将side1合并到 o/main分支上，切换到side1*分支

git rebase side1 side2;
# 将side2合并到 side1 分支上，切换到side2*分支

git rebase side2 side3;
# 将side3合并到 side2 分支上，切换到side3*分支

git rebase side3 main;
# 将main 分支合并到 side3，只是快速前进操作
# 切换到 main*

git push;
# 推到远程仓库上
```



* `git merge`合并特性分支

一些开饭人员喜欢保留提交历史，因此更爱`merge`操作，而其他人员更喜欢干净的提交树，于是更偏爱`rebase`。

仁者见仁，智者见智。

使用

```shell
# 使用 git merger 完成Task
git fetch;
# 进行下载操作

git merge o/main;
# main*，将o/main合并过来

git merge side1, side2, side3;
# main*，依次将side1，2，3合并到main分支上

git push;
# 推送到远端代码
```

* 远程跟踪分支

不一定使用`main`分支追踪`o/main`分支了，可以设置某一分支追踪`o/main`分支了

```shell
# 1
git checkout -b foo o/main;
git pull;
# 创建一个新分支foo，并切换过去

git checkout -b foo o/main;
git commit;
git push;
# 创建一个新分支foo，并切换过去

# 2
git branch -u o/main foo;
# foo 分支就会追踪 o/main了
```

## 5.4 `git push`的参数

在`git push`中，`Git`是通过当前所在分支的属性来确定远程仓库以及要`push`的目的地，这是未指定参数时的行为，我们可以为`push`指定参数。

```shell
# 语法
git push <remote> <place>
# <remote>: 远端仓库名
# <place>: 分支名

# 翻译过来
git push origin main
# 意思：切换到本地仓库的 main 分支，获取所有的提交，
# 再到远程仓库 origin 中找到 main 分支，将远程仓库中没有的提交记录都添加上去，搞定之后告诉我
```

```shell
# Task
# 可以将代码 push 到不同的分支上去
```

 `place`参数的来源和去向不一致的情况：比如想把本地的`foo`分支推送到远程仓库的`bar` 分支。

### 🤔`way01`本地分支关联远程分支：使用`push`

使用`:` 将两个地址连起来就可以了。

```bash
git push origin <source>:<destination>

git push origin foo^:main
# foo^ 表示foo当前的上一个提交点，push到远端仓库的 main 分支上


```

使用`git push `命令的`-u`选项来推送本地分支，同时关联远程分支。假设在本地有个分支`local_branch`，要将其推送到远程并关联到`remote_branch`，执行以下命令：

```bash
git push -u origin local_branch:remote_branch
# 其具体语法和上述类似
# -u 会自动设置本地分支跟踪远程分支，此后，在该 local_branch 分支上使用
# git push 和 git pull命令是，Git将知道与哪个远程分支进行交互。
```



### 🤔`way02`本地分支关联远程分支：使用`branch`

```bash
git branch --set-upstream-to=origin/remote-branch local-branch
# 使用 --set-upstream-to选项，将本地分支与远程分支关联起来
```

举例本地有分支 `dev`，需要关联到远程分支`origin/dev`。可以先使用`git branch -vv`命令来查看本地分支和仓库分支的对应关系。再使用上述命令，即：

```shell
git branch --set-upsteam-to=origin/dev dev
```



### 😎新建远程分支的一种方法

😎重点：如果你要推送到的目的分支不存在会怎么样？`Git`会在远程仓库中帮你创建这个分支！

```shell
git push origin main:newBranch;
```

## 5.5 `git fetch`参数

仅仅是和`git push`的方向相反而已，`push`是上传，`fetch`是下载到本地。

```shell
git fetch origin foo;
# Git 会到远程仓库的 foo 分支上，获取所有本地不存在的提交，放到本地的 o/foo 上。
# 只下载了远程仓库中 foo 分支中的最新提交记录，并更新了本地的 o/foo

git fetch origin foo~1:bar
# 注意和push main^不同的是，这里是foo~1，来进行向上的移动操作
```

### 😎删除远程分支的一种方式：奇怪用法

✍️重要：在使用`git push/fetch origin :side`不去添加`<source>`选项。

提供另一种删除的方法

```shell
git push origin :foo;
# 若 push 的<source>为空，则会删除远程分支上foo

git fetch origin :foo
# 若 fetch 的<source>为空，则会建立一个foo分支到本地
```

* `git pull`的参数

`git pull <==> git fetch + git merge`同等的操作。

```shell
git pull origin main
# git fetch; bar*，将main分支下载到o/main 上
# git merge o/main; 合并 o/main 到当前分支 bar* 上面
```

当然，也支持`<source>:<destination>`的操作

```shell
git pull origin main:foo
# 从远处仓库 main 下载分支到本地分支 foo 上
# 再 merge 到我们当前所在的分支 bar* 上
```



## 5.6 `git commit --amend`的使用

工作中有两种情况需要用到 `commit --amend`，从其字面意思就可大致了解到，`amend`表示缝合，修正的意思，避免无用提交。

1. 提交（`commit`）过一次代码之后，发现一个地方改错了，现在需要改过来，当再次提交的时候，不想再多一次提交记录，重新叠加到上次的提交记录上；
2. 上一次提交的 `commit message`的信息描述有误，可以直接使用该命令，修改`message`内容。

✨例子描述

1. 代码补交举例：基于下面的例子`2`的基础，看代码发生改变之后情况

   首先，使用`git log`查看当前提交历史，和最近提交的 `commit ID`

   ```shell
   PS F:\Codefield\Github\MyGitHubProject\Myfirst> git log
   commit 8d1884597fc2590371fc78e21beda930e2ea5612 (HEAD -> master) # 对应的 commit ID
   Author: Dargon0123 <dargon0123@163.com>
   Date:   Sat Nov 4 15:11:42 2023 +0800
   
       Add `git commit --amend` usage 1
   
   commit b23f782bf2cf829848deb31672f4c84fb6225651
   Merge: 2a2eb7e 10a0c2f
   Author: Dargon0123 <dargon0123@163.com>
   Date:   Sat Nov 4 15:05:58 2023 +0800
   
       Merge branch 'master' of github.com:Dargon0123/Myfirst
   
   ```

   接着，将代码部分进行修改操作

   ```shell
   # 通过git status查看当前工作区修改状态
   PS F:\Codefield\Github\MyGitHubProject\Myfirst> git status
   On branch master
   Your branch is ahead of 'origin/master' by 3 commits.
     (use "git push" to publish your local commits)
   
   Changes not staged for commit:
     (use "git add <file>..." to update what will be committed)
     (use "git restore <file>..." to discard changes in working directory)
           modified:   Git的使用与常见问题/Git_GuideLine.md
   
   no changes added to commit (use "git add" and/or "git commit -a")
   ```

   使用`git commit --amend`之后，查看`git log`的操作

   ```shell
   PS F:\Codefield\Github\MyGitHubProject\Myfirst> git log
   commit a3fc580d230c76735dce378c40c3c49e568b5864 (HEAD -> master) # 对应的 commit ID,相当于将上次的 ID overwrite掉了
   Author: Dargon0123 <dargon0123@163.com>
   Date:   Sat Nov 4 15:11:42 2023 +0800
   
       Add `git commit --amend` usage 2
   
   commit b23f782bf2cf829848deb31672f4c84fb6225651
   Merge: 2a2eb7e 10a0c2f
   Author: Dargon0123 <dargon0123@163.com>
   Date:   Sat Nov 4 15:05:58 2023 +0800
   
       Merge branch 'master' of github.com:Dargon0123/Myfirst
   ```

   

2. 修改上次`commit message`，先使用`git log`看下当前的提交记录 

   ```shell
   PS F:\Codefield\Github\MyGitHubProject\Myfirst> git log
   commit acea56c75a02578d6fcc3b8f5d7b2b6ee314c716 (HEAD -> master) # 对应的 commit ID
   Author: Dargon0123 <dargon0123@163.com>
   Date:   Sat Nov 4 15:11:42 2023 +0800
   
       Add `git commit --amend` usage
   
   commit b23f782bf2cf829848deb31672f4c84fb6225651 # 对应的 commit ID
   Merge: 2a2eb7e 10a0c2f
   Author: Dargon0123 <dargon0123@163.com>
   Date:   Sat Nov 4 15:05:58 2023 +0800
   
       Merge branch 'master' of github.com:Dargon0123/Myfirst
   ```
   
   接着，使用`git commit --amend`命令
   
   ```shell
   PS F:\Codefield\Github\MyGitHubProject\Myfirst> git commit --amend
   [master 8d18845] Add `git commit --amend` usage 1
    Date: Sat Nov 4 15:11:42 2023 +0800
    1 file changed, 66 insertions(+)
    
   # 重新查看 git log，发现上次更改的 message 信息
   PS F:\Codefield\Github\MyGitHubProject\Myfirst> git log
   commit 8d1884597fc2590371fc78e21beda930e2ea5612 (HEAD -> master) # 对应的 commit ID发生了更改
   Author: Dargon0123 <dargon0123@163.com>
   Date:   Sat Nov 4 15:11:42 2023 +0800
   
       Add `git commit --amend` usage 1
   
   commit b23f782bf2cf829848deb31672f4c84fb6225651
   Merge: 2a2eb7e 10a0c2f
   Author: Dargon0123 <dargon0123@163.com>
   Date:   Sat Nov 4 15:05:58 2023 +0800
   
       Merge branch 'master' of github.com:Dargon0123/Myfirst
   ```
   
   但是，这个方法，会改变你原来的`commit ID`。
   
   之所以不会更改代码，是因为此时，本地修改的代码，没有`add`到暂存区，本地代码相对上次是没有发生改变，所以，仅仅是变更，提交了`commit message`信息。

 ✨小插曲

上面使用的 `git commit --amend`虽然可以实现将本次的更改，重新叠加到上次的提交记录上。但是，这个操作更新了我上次提交的`ID`。

在工作中，你可能在代码评审的时候，需要这个`ID`。比如，你提交一笔代码，结果代码审核没通过，给了你一些修改意见，你基于本地修改后，就需要在同一个 `ID`上来提交，表明解决这个问题，为了使得代码和问题都有追溯性，显然不能将上一个`ID`给覆盖了。

这样，就需要一个这样的 `git commit --amend`命令，即可修改代码，且提交之后，还保留着上次的 `ID` 

直接使用 `git push -f [commit ID]`

工作中使用 `cr push -f [commit ID]`就可以完成上述操作。

😥暂时在 `git`中没有找到相应的操作。



## 问题

1. 如何新建一个分支？本地新建一个分支，能否推送到远端仓库上面？还是先在远端创建一个分支，本地的分支可以提交代码到远端新分支里面。
