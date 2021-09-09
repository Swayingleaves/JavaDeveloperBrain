# Linux
## 文件和目录的操作
- `ls` 显示文件和目录列表
- `cd` 切换目录
- `pwd` 显示当前工作目录
- `mkdir` 创建目录
- `rmdir` 删除空目录
- `touch` 生成一个空文件或更改文件的时间
- `cp` 复制文件或目录
- `mv` 移动文件或目录、文件或目录改名
- `rm` 删除文件或目录
- `ln` 建立链接文件
- `find` 查找文件
- `file/stat` 查看文件类型或文件属性信息
- `echo` 把内容重定向到指定的文件中 ，有则打开，无则创建
- `管道命令 |` 将前面的结果给后面的命令，例如：`ls -la | wc `，将ls的结果加油wc命令来统计字数
- 重定向 `>` 是覆盖模式，`>>` 是追加模式
  - 例如：`echo "Java3y,zhen de hen xihuan ni" > qingshu.txt `把左边的输出放到右边的文件里去
## 查看文件	  
- `cat` 查看文本文件内容
- `more` 可以分页看
- `less` 不仅可以分页，还可以方便地搜索，回翻等操作
- `tail -10` 查看文件的尾部的10行
- `head -20` 查看文件的头部20行
## 管理用户
### 用户管理
- `useradd` 添加用户
- `usermod` 修改用户
- `userdel` 删除用户
### 组管理
- `groupadd` 添加组 
- `groupmod` 修改组 
- `groupdel` 删除组
### 批量管理用户：
- 成批添加/更新一组账户：`newusers`
- 成批更新用户的口令：`chpasswd`
### 组成员管理：
- 向标准组中添加用户
  - `gpasswd -a <用户账号名> <组账号名>`
  - `usermod -G <组账号名> <用户账号名>`
- 从标准组中删除用户
  - `gpasswd -d <用户账号名> <组账号名>`
### 口令管理
- 口令时效设置： 修改 /etc/login.defs 的相关配置参数
- 口令维护(禁用、恢复和删除用户口令)： `passwd`
- 设置已存在用户的口令时效： `change`
### 切换用户
- `su`
- `sudo`
### 用户相关的命令：
- `id`：显示用户当前的uid、gid和用户所属的组列表
- `groups`：显示指定用户所属的组列表
- `whoami`：显示当前用户的名称
- `w/who`：显示登录用户及相关信息
- `newgrp`：用于转换用户的当前组到指定的组账号，用户必须属于该组才可以正确执行该命令
## 进程管理
- `ps`：查找出进程的信息 查看自己的进程
  - `ps -l` 查看系统所有进程
  - `ps aux` 查看特定的进程
  - `ps aux | grep threadx` 
- `nice`和`renice`：调整进程的优先级
- `kill`：杀死进程
- `free`：查看内存使用状况
- `top` ：查看实时刷新的系统进程信息
- `netstat` 查看占用端口的进程
  - `netstat -anp | grep port`
- 进程状态
  - `R` running or runnable (on run queue)正在执行或者可执行，此时进程位于执行队列中。
  - `D` uninterruptible sleep (usually I/O)不可中断阻塞，通常为 IO 阻塞。
  - `S` interruptible sleep (waiting for an event to complete)可中断阻塞，此时进程正在等待某个事件完成。
  - `Z` zombie (terminated but not reaped by its parent)僵死，进程已经终止但是尚未被其父进程获取信息。
  - `T` stopped (either by a job control signal or because it is being traced)结束，进程既可以被作业控制信号结束，也可能是正在被追踪。
- `SIGCHLD` 当一个子进程改变了它的状态时（停止运行，继续运行或者退出），有两件事会发生在父进程中
  - 得到 SIGCHLD 信号；
  - waitpid() 或者 wait() 调用会返回。
    - wait() 父进程调用 wait() 会一直阻塞，直到收到一个子进程退出的 SIGCHLD 信号，之后 wait() 函数会销毁子进程并返回。 如果成功，返回被收集的子进程的进程 ID；如果调用进程没有子进程，调用就会失败，此时返回 -1，同时 errno 被置为 ECHILD。 参数 status 用来保存被收集的子进程退出时的一些状态，如果对这个子进程是如何死掉的毫不在意，只想把这个子进程消灭掉，可以设置这个参数为 NULL。
    - waitpid() 作用和 wait() 完全相同，但是多了两个可由用户控制的参数 pid 和 options。 pid 参数指示一个子进程的 ID，表示只关心这个子进程退出的 SIGCHLD 信号。如果 pid=-1 时，那么和 wait() 作用相同，都是关心所有子进程退出的 SIGCHLD 信号。 options 参数主要有 WNOHANG 和 WUNTRACED 两个选项，WNOHANG 可以使 waitpid() 调用变成非阻塞的，也就是说它会立即返回，父进程可以继续执行其它任务。
  - 其中子进程发送的 SIGCHLD 信号包含了子进程的信息，比如进程 ID、进程状态、进程使用 CPU 的时间等。
  - 在子进程退出时，它的进程描述符不会立即释放，这是为了让父进程得到子进程信息，父进程通过 wait() 和
  - waitpid() 来获得一个已经退出的子进程的信息。
- 僵尸进程孤儿进程什么原因导致的，哪个危害大，怎么解决
  - `孤儿进程` 一个父进程退出，而它的一个或多个子进程还在运行，那么这些子进程将成为孤儿进程。 孤儿进程将被 init 进程（进程号为 1）所收养，并由 init 进程对它们完成状态收集工作。 由于孤儿进程会被 init 进程收养，所以孤儿进程不会对系统造成危害。
  - `僵尸进程` 一个子进程的进程描述符在子进程退出时不会释放，只有当父进程通过 wait() 或 waitpid() 获取了子进程信息后才会释放。如果子进程退出，而父进程并没有调用 wait() 或 waitpid()，那么子进程的进程描述符仍然保存在系统中，这 种进程称之为僵尸进程。 僵尸进程通过 ps 命令显示出来的状态为 Z（zombie）。
    - 系统所能使用的进程号是有限的，如果产生大量僵尸进程，将因为没有可用的进程号而导致系统不能产生新的进程。
    - 要消灭系统中大量的僵尸进程，只需要将其父进程杀死，此时僵尸进程就会变成孤儿进程，从而被 init 进程所收养，
    - 这样 init 进程就会释放所有的僵尸进程所占有的资源，从而结束僵尸进程。
- 作业管理
  - jobs：列举作业号码和名称
  - bg: 在后台恢复运行
  - fg：在前台恢复运行
  - ctrl+z：暂时停止某个进程
- 自动化任务
  - at
  - cron
- 管理守护进程
  - chkconfig
  - service
  - ntsysv
## 打包和压缩文件
### 压缩
- `gzip filename`
- `bzip2 filename`
- `tar -czvf filename`
### 解压
- `gzip -d filename.gz`
- `bzip2 -d filename.bz2`
- `tar -xzvf filename.tar.gz`
## grep+正则表达式
- `grep -n mystr myfile` 在文件 myfile 中查找包含字符串 mystr的行
- `grep  '^[a-zA-Z]'  myfile `显示 myfile 中第一个字符为字母的所有行
## Vi编辑器
### 普通模式
- `G`用于直接跳转到文件尾
- `ZZ`用于存盘退出Vi
- `ZQ`用于不存盘退出Vi
- `/`和`？`用于查找字符串
- `n`继续查找下一个
- `yy`复制一行
- `p`粘帖在下一行，P粘贴在前一行
- `dd` 删除一行文本
- `u` 取消上一次编辑操作（undo）
### 插入模式
- 使用i或a或o进去插入模式
- 使用esc返回普通模式
### 命令行模式
- `w`保存当前编辑文件，但并不退出
- `w newfile`  存为另外一个名为 “newfile” 的文件
- `wq` 用于存盘退出Vi
- `q!`用于不存盘退出Vi
- `q`用于直接退出Vi （未做修改)
### 设置Vi环境
- `set autoindent`  缩进,常用于程序的编写
- `set noautoindent` 取消缩进
- `set number` 在编辑文件时显示行号
- `set tabstop=value` 设置显示制表符的空格字符个数
- `set` 显示设置的所有选项
## 权限管理
- 改变文件或目录的权限：chmod
- 改变文件或目录的属主（所有者）：chown
- 改变文件或目录所属的组：chgrp
- 设置文件的缺省生成掩码：umask
- 文件扩展属性
  - 显示扩展属性：`lsattr [-adR] [文件|目录]`
  - 修改扩展属性：`chattr [-R] [[-+=][属性]] <文件|目录>`
## 网络管理
### 网络接口相关
- `ifconfig`：查看网络接口信息
- `ifup/ifdown`：开启或关闭接口
### 临时配置相关
- `route`命令：可以临时地设置内核路由表
- `hostname`命令：可以临时地修改主机名
- `sysctl`命令：可以临时地开启内核的包转发
- `ifconfig`命令：可以临时地设置网络接口的IP参数
### 网络检测的常用工具：
- `ifconfig` 检测网络接口配置
- `route` 检测路由配置
- `ping` 检测网络连通性
- `netstat` 查看网络状态
- `lsof` 查看指定IP 和/或 端口的进程的当前运行情况
- `host/dig/nslookup` 检测DNS解析
- `traceroute` 检测到目的主机所经过的路由器
- `tcpdump` 显示本机网络流量的状态
### 安装软件
- `yum`
- `rpm`
- `wget`
## cpu100%怎么排查
### 1、问题复现
### 2、第一查看程序运行日志
### 3、排查
- 执行“top”命令 查看CPU最高的进程pid
- 执行“top -Hp 进程号”命令 查看java进程下的所有线程占CPU的情况。
- 执行“printf "%x\n 10"命令 把进程号转为16进制，方便在堆栈中查找线程号
- 执行 “jstack 进程号 | grep 线程ID”
  - 可以查看线程的状态判断问题
    - NEW,未启动的。不会出现在Dump中。
    - RUNNABLE,在虚拟机内执行的。运行中状态，可能里面还能看到locked字样，表明它获得了某把锁。
    - BLOCKED,受阻塞并等待监视器锁。被某个锁(synchronizers)給block住了。
    - WATING,无限期等待另一个线程执行特定操作。等待某个condition或monitor发生，一般停留在park(), wait(), sleep(),join() 等语句里。
    - TIMED_WATING,有时限的等待另一个线程的特定操作。和WAITING的区别是wait() 等语句加上了时间限制 wait(timeout)。
    - TERMINATED,已退出的。
  - 注意deadlock
- jmap -dump pid 导出dump文件供一些分析工具分析