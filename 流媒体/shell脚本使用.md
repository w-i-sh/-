## 1、错误场景分析
同样的脚本在不同的主机上使用相同的命令不能执行。
```
nohup sh tool.sh rtc_live_servic 5 .   > /dev/null 2> /dev/null &
```
并且tool.sh脚本中规定了#!bin/bash


分析后发现是因为tool.sh脚本确实规定了使用bin/bash来执行脚本，但是如果使用sh tool.sh来执行的话会使用sh执行的shell来执行脚本，以前机器的sh默认指向的都是bin/bash shell但是有台机器的sh不是，它指向的是bin/dash，导致执行失败



查看sh指向的命令：`readlink -f $(which sh)`



结论：之后运行脚本可以直接使用./{脚本名}来执行，因为脚本中已经规定了#!bin/bash使用bash shell来执行脚本

## 2、bash和dash的区别
/usr/bin/dash和/bin/bash并不完全一样，它们是两种不同的shell 。[1] [2] [3] [4] [5]

[1]: https://blog.csdn.net/HandsomeHong/article/details/120120737
[2]: https://www.cnblogs.com/macrored/p/11548347.html
[3]: https://jishuzhan.net/article/1772078394528239617
[4]: https://cloud.baidu.com/article/2853345
[5]: https://blog.csdn.net/hshl1214/article/details/51122663

- Bash (Bourne Again SHell)是许多Linux平台的默认Shell。它提供了许多额外的功能和工具，包括命令编辑、历史记录、自动补全等。Bash支持的写法比dash多很多。

- Dash (Debian Almquist Shell)是Debian及其衍生发行版默认的Shell。Dash设计更注重轻量化和速度，它的执行速度比Bash快，因为它的代码更精简。Dash不支持一些Bash的高级特性，比如命令补全和作业控制。Dash主要是为了执行脚本而出现，而不是交互。

## 3、执行脚本的方式
在Shell中执行脚本有以下几种方式，它们之间的主要区别在于是否需要执行权限和是否会创建子进程：
    
- 使用绝对路径或相对路径执行：这种方式需要给脚本添加执行权限（使用chmod +x script.sh命令），并且会在当前shell中开启一个子shell来执行脚本内容。例如：
    chmod +x script.sh
    ./script.sh

- 使用sh或bash命令来执行：这种方式不需要手动给脚本添加执行权限，但是它会改变脚本默认解释器类型。例如：

    ```
    sh script.sh
    bash script.sh
    ```


- 使用.（点）命令来执行：这种方式不需要单独添加执行权限，它和source类似，权限继承于bash。例如：

    `. script.sh`


- 使用source命令来执行：这种方式也不需要单独添加执行权限，主要用于生效配置文件。例如：

    `source script.sh`

只有使用绝对路径或相对路径执行的方式需要给脚本添加执行权限。使用sh或bash命令来执行的方式会改变脚本默认解释器类型。

而使用.（点）命令和source命令来执行的方式则不会创建子进程，会直接在当前shell环境中执行。这意味着脚本中设置的环境变量会直接影响当前shell。

因此，当我们需要利用脚本设置当前环境变量时，应该采取后两种运行脚本的方式

## 常见shell类型及其特点
__1. Bourne shell (sh)__

UNIX 最初使用，且在每种 UNIX 上都可以使用。在 shell 编程方面相当优秀，但在处理与用户的交互方面做得不如其他几种shell。

__2\. C shell (csh)__

csh, the C shell, is a command interpreter with a syntax similar to the C programming language.一个语法上接近于C语言的shell。

__3. Korn shell (ksh)__

完全向上兼容 Bourne shell 并包含了 C shell 的很多特性。

__4. Bourne Again shell (bash)__

因为Linux 操作系统缺省的 shell。即 bash 是 Bourne shell 的扩展，与 Bourne shell 完全向后兼容。在 Bourne shell 的基础上增加、增强了很多特性。可以提供如命令补全、命令编辑和命令历史表等功能。包含了很多 C shell 和 Korn shell 中的优点，有灵活和强大的编程接口，同时又有很友好的用户界面。

__5. Debian Almquist Shell(dash)__

原来bash是GNU/Linux 操作系统中的 /bin/sh 的符号连接，但由于bash过于复杂，有人把 bash 从 NetBSD 移植到 Linux 并更名为 dash，且/bin/sh符号连接到dash。Dash Shell 比 Bash Shell 小的多（ubuntu16.04上，bash大概1M，dash只有150K），符合POSIX标准。Ubuntu 6.10开始默认是Dash。