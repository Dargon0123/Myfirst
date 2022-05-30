[toc]

# 00 问题

* 本地通过`ssh`与`github`尝试连接的时候，出现问题。

* ```she
  Could not resolve host: github.com
  
  or
  
  ssh: Could not resolve hostname github.com: Name or service not known
  ```

* 尝试着修改DNS，未解决

# 01 方法

* 将`github` 的IP地址添加到本地的`DNS`的`hosts`文件中，改文件位于 `C:\Windows\System32\drivers\etc`，添加

* ```shell
  # Copyright (c) 1993-2009 Microsoft Corp.
  #
  # This is a sample HOSTS file used by Microsoft TCP/IP for Windows.
  #
  # This file contains the mappings of IP addresses to host names. Each
  # entry should be kept on an individual line. The IP address should
  # be placed in the first column followed by the corresponding host name.
  # The IP address and the host name should be separated by at least one
  # space.
  #
  # Additionally, comments (such as these) may be inserted on individual
  # lines or following the machine name denoted by a '#' symbol.
  #
  # For example:
  #
  #      102.54.94.97     rhino.acme.com          # source server
  #       38.25.63.10     x.acme.com              # x client host
  
  # localhost name resolution is handled within DNS itself.
  #	127.0.0.1       localhost
  #	::1             localhost
  
  140.82.114.4  github.com # 添加改行地址即可
  ```

* 再次进行`ping github.com`的时候，可以`ping`通。

* ```shell
  C:\Users\xxx>ping github.com
  
  正在 Ping github.com [140.82.114.4] 具有 32 字节的数据:
  来自 140.82.114.4 的回复: 字节=32 时间=238ms TTL=44
  来自 140.82.114.4 的回复: 字节=32 时间=238ms TTL=44
  来自 140.82.114.4 的回复: 字节=32 时间=230ms TTL=44
  来自 140.82.114.4 的回复: 字节=32 时间=230ms TTL=44
  
  140.82.114.4 的 Ping 统计信息:
      数据包: 已发送 = 4，已接收 = 4，丢失 = 0 (0% 丢失)，
  往返行程的估计时间(以毫秒为单位):
      最短 = 230ms，最长 = 238ms，平均 = 234ms
      
  # 进行重新验证下ssh 与github的ssh 连接即可
  
  C:\Users\xxx>ssh git@github.com
  The authenticity of host 'github.com (140.82.114.4)' can't be established.
  ECDSA key fingerprint is SHA256:p2QAMXNIC1TJYWeIOttrVc98/R1BUFWu3/LiyKgUfQM.
  Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
  Warning: Permanently added 'github.com,140.82.114.4' (ECDSA) to the list of known hosts.
  PTY allocation request failed on channel 0
  Hi Dargon0123! You've successfully authenticated, but GitHub does not provide shell access.
  Connection to github.com closed.
  ```

  