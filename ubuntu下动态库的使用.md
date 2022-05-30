# 问题描述

关于在ubuntu环境下，自行创建动态库，在运行`link`阶段出现错误，无法加载到这个库的解决办法

```shell
dargon@dd:~/桌面/CSAPP/TestCode$ ./snooze 
./snooze: error while loading shared libraries: libcsapp.so: cannot open shared object file: No such file or directory
```

* 方法1: export 下当前的该库所在的位置

  此时由于将`libcsapp.so`放在`/usr/local/lib`目录下面，但是第一次加进去，程序在`link`阶段的时候，会出现错误。

  1. ```shell
     # 查看下变量 LD_LIBRARY_PATH 
     dargon@dd:~/桌面/CSAPP/TestCode$ echo $LD_LIBRARY_PATH
     
     # 设置 LD_LIBRARY_PATH 
     # Note: 第一次用，应该直接export，否则会报错：No command exist 
     dargon@dd:~/桌面/CSAPP/TestCode$ export LD_LIBRARY_PATH=/usr/local/lib
     
     # 设置后，在进行查看一下 
     dargon@dd:~/桌面/CSAPP/TestCode$ echo $LD_LIBRARY_PATH
     /usr/local/lib
     
     # ./it can run my prog
     dargon@dd:~/桌面/CSAPP/TestCode$ ./snooze  10
     ^CSlept for 2 of 10 escs. 
     
     ```

  2. 缺点 ，只对当前shell 窗口有效，当重新开始一个窗口的时候，需要重新进行配置

* 方法2： 直接设置`ldconfig`

  1. ```shell
     # 直接进行配置一下 link dynamic library
     sudo ldconfig
     ```

  2. 关于该命令的作用描述 `ldconfig creates the necessary links and cache to the most recent shared libraries found in the directories specified on the command line, in the file /etc/ld.so.conf, and in the trusted directories (/lib and /usr/lib).`