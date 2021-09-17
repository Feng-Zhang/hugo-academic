---
title: " 在win10中使用ubuntu子系统WSL如何安装g++"  
subtitle: ""  
summary: "windows下使用linux (WSL)系统时如何正确安装g++"  
authors: [风不止]  
tags: ["win10","ubuntu","g++ install","安装"]  
categories: [windows]  
date: 2020-09-15T15:56:11+08:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Placement options: 1 = Full column width, 2 = Out-set, 3 = Screen-width
# Focal point options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
image:
  placement: 1
  caption: ''
  focal_point: "Smart"
  preview_only: false
  
---

{{% toc %}}

## 前言

　　偷偷告诉你一个秘密，一般人我不会说的，那就是WSL实在是太好用了。

　　Windows系统是全世界用户最多的，一直以来我也是用这个系统。不过有一个缺点就是没有terminal，虽然有dos操作，不过和Linux的bash相比实在弱爆了。但是我又不想放弃windows系统，这成为我心里的一个疙瘩。

　　目前来说，主要有3种方法可以在windows下实现linux的bash操作。

- 第1种就是安装虚拟机。也就是说在你的电脑里再安装一个系统，具体实现流程可参考[这篇博客](https://blog.csdn.net/xm_csdn/article/details/64438178)。缺点就是比较笨重，耗内存，最不能忍的是和你的电脑并不共享文件，相当于另一个电脑。
- 第2种方法是使用docker。自己制作一个镜像，上传到docker hub上。貌似就可以随时随地使用了，如果有更新还可以自主更新。不过这个得有docker基础，学会还不是一时半会的事。
- 于是找到第3种方法使用windows subsystem for linux（WSL）。windows自带这个可选功能，可以实现bash所有操作。这个相当于在你电脑上安装了轻巧型ubuntu系统，可以直接对磁盘上的文件进行操作。

## 安装

　　怎么安装这里就不细说了，网上教程一大堆。可以参考[一直学的博客](https://zhuanlan.zhihu.com/p/76032647)，写的很详细了。

## 使用

　　　折腾半天终于把WSL 安装好，当你兴冲冲打开ubuntu的terminal想安装一个软件时，会报下面这个错误。

```
Reading package lists... Done
Building dependency tree
Reading state information... Done
E: Unable to locate package build-essentials
```

不过[一直学的博客](https://zhuanlan.zhihu.com/p/76032647)也谈到这个问题，这是因为软件源不行，得换国内的软件源。参考网上的说法，觉得中科大的软件源比较好用。于是成功按照步骤进行更换。没问题…个鬼啊，这是个巨坑。后面安装R软件包的时候会详细描述。



### 安装R软件

　　本人是做生信的，R软件是必不可少的工具之一。可以直接用`sudo apt install r-base`来安装，不过默认的 Ubuntu 软件源中的 R 软件包经常都是过时的，我们得从[CRAN](https://cran.r-project.org/)软件源中安装 R。可以按下面的方式进行安装：

```shell
# 01.安装必要的软件包，添加一个新的软件源：
sudo apt install dirmngr gnupg apt-transport-https ca-certificates software-properties-common
# 02.将 CRAN 软件源 添加到你的系统源列表：
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
sudo add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/'

# 03.输入下面的命令，安装 R：
sudo apt install r-base

# 04.安装过程会持续几分钟完成。一旦完成，打印 R 的版本，验证它是否安装成功：
R --version
```

如果你发现出现下面的结果，现在是2020-09月，说明R版本是官网上最新的就没问题了。

```
R version 4.0.2 (2020-06-22) -- "Taking Off Again"
Copyright (C) 2020 The R Foundation for Statistical Computing
Platform: x86_64-pc-linux-gnu (64-bit)

R is free software and comes with ABSOLUTELY NO WARRANTY.
You are welcome to redistribute it under the terms of the
GNU General Public License versions 2 or 3.
For more information about these matters see
https://www.gnu.org/licenses/.
```



### 安装R软件包

　　由于运行R程序需要`httr`包，直接在bash上输入`R`打开R的交互窗口后，我们可以用下面的代码进行安装：

```R
# 由于R官网的软件包默认是放在国外服务器上的，对国内用户下载不友好，我们可以换清华的软件源。
options(BioC_mirror="http://mirrors.tuna.tsinghua.edu.cn/bioconductor/")##指定BioC_mirror镜像是清华镜像
options("repos" = c(CRAN="http://mirrors.tuna.tsinghua.edu.cn/CRAN/")) ##指定install.packages安装镜像是清华镜像
install.packages("httr")
```

之后会遇到这个错误：

```
* installing *source* package ‘sys’ ...
** package ‘sys’ successfully unpacked and MD5 sums checked
** using staged installation
** libs
gcc -std=gnu99 -I"/usr/share/R/include" -DNDEBUG      -fpic  -g -O2 -fdebug-prefix-map=/build/r-base-5iUtQS/r-base-4.0.2=. -fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2 -g  -c exec.c -o exec.o
In file included from exec.c:6:0:
/usr/share/R/include/Rinternals.h:39:11: fatal error: stdio.h: No such file or directory
 # include <stdio.h>
           ^~~~~~~~~
compilation terminated.
/usr/lib/R/etc/Makeconf:167: recipe for target 'exec.o' failed
make: *** [exec.o] Error 1
ERROR: compilation failed for package ‘sys’
* removing ‘/home/zhangfeng/R/x86_64-pc-linux-gnu-library/4.0/sys’
* installing *source* package ‘curl’ ...
** package ‘curl’ successfully unpacked and MD5 sums checked
** using staged installation
Using PKG_CFLAGS=
Using PKG_LIBS=-lcurl
------------------------- ANTICONF ERROR ---------------------------
Configuration failed because libcurl was not found. Try installing:
 * deb: libcurl4-openssl-dev (Debian, Ubuntu, etc)
 * rpm: libcurl-devel (Fedora, CentOS, RHEL)
 * csw: libcurl_dev (Solaris)
If libcurl is already installed, check that 'pkg-config' is in your
PATH and PKG_CONFIG_PATH contains a libcurl.pc file. If pkg-config
is unavailable you can set INCLUDE_DIR and LIB_DIR manually via:
R CMD INSTALL --configure-vars='INCLUDE_DIR=... LIB_DIR=...'
--------------------------------------------------------------------
ERROR: configuration failed for package ‘curl’
* removing ‘/home/zhangfeng/R/x86_64-pc-linux-gnu-library/4.0/curl’
* installing *source* package ‘jsonlite’ ...
** package ‘jsonlite’ successfully unpacked and MD5 sums checked
** using staged installation
** libs
gcc -std=gnu99 -I"/usr/share/R/include" -DNDEBUG -Iyajl/api    -fvisibility=hidden  -fpic  -g -O2 -fdebug-prefix-map=/build/r-base-5iUtQS/r-base-4.0.2=. -fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2 -g  -c base64.c -o base64.o
base64.c:6:10: fatal error: stdlib.h: No such file or directory
 #include <stdlib.h>
          ^~~~~~~~~~
compilation terminated.
/usr/lib/R/etc/Makeconf:167: recipe for target 'base64.o' failed
make: *** [base64.o] Error 1
ERROR: compilation failed for package ‘jsonlite’
* removing ‘/home/zhangfeng/R/x86_64-pc-linux-gnu-library/4.0/jsonlite’
* installing *source* package ‘mime’ ...
** package ‘mime’ successfully unpacked and MD5 sums checked
** using staged installation
** libs
gcc -std=gnu99 -I"/usr/share/R/include" -DNDEBUG      -fpic  -g -O2 -fdebug-prefix-map=/build/r-base-5iUtQS/r-base-4.0.2=. -fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2 -g  -c init.c -o init.o
In file included from init.c:1:0:
/usr/share/R/include/R.h:55:11: fatal error: stdlib.h: No such file or directory
 # include <stdlib.h> /* Not used by R itself, but widely assumed in packages */
           ^~~~~~~~~~
compilation terminated.
/usr/lib/R/etc/Makeconf:167: recipe for target 'init.o' failed
make: *** [init.o] Error 1
ERROR: compilation failed for package ‘mime’
* removing ‘/home/zhangfeng/R/x86_64-pc-linux-gnu-library/4.0/mime’
ERROR: dependency ‘sys’ is not available for package ‘askpass’
* removing ‘/home/zhangfeng/R/x86_64-pc-linux-gnu-library/4.0/askpass’
ERROR: dependency ‘askpass’ is not available for package ‘openssl’
* removing ‘/home/zhangfeng/R/x86_64-pc-linux-gnu-library/4.0/openssl’
ERROR: dependencies ‘curl’, ‘jsonlite’, ‘mime’, ‘openssl’ are not available for package ‘httr’
* removing ‘/home/zhangfeng/R/x86_64-pc-linux-gnu-library/4.0/httr’

The downloaded source packages are in
        ‘/tmp/RtmpG9wQX4/downloaded_packages’
Warning messages:
1: In install.packages("httr") :
  installation of package ‘sys’ had non-zero exit status
2: In install.packages("httr") :
  installation of package ‘curl’ had non-zero exit status
3: In install.packages("httr") :
  installation of package ‘jsonlite’ had non-zero exit status
4: In install.packages("httr") :
  installation of package ‘mime’ had non-zero exit status
5: In install.packages("httr") :
  installation of package ‘askpass’ had non-zero exit status
6: In install.packages("httr") :
  installation of package ‘openssl’ had non-zero exit status
7: In install.packages("httr") :
  installation of package ‘httr’ had non-zero exit status
```

仔细看错误信息，这应该是g++没有安装。`q()`关闭R交互窗口，返回bash。我们查看一下g++的情况：`g++ --version` 。bash会给出下面的信息```g++: command not found```。这说明g++是没安装的。`sudo apt-get install g++`安装起走，但是结果却出人意料：

```
Reading package lists... Done
Building dependency tree
Reading state information... Done
Some packages could not be installed. This may mean that you have
requested an impossible situation or if you are using the unstable
distribution that some required packages have not yet been created
or been moved out of Incoming.
The following information may help to resolve the situation:

The following packages have unmet dependencies:
 g++ : Depends: g++-7 (>= 7.4.0-1~) but it is not going to be installed
E: Unable to correct problems, you have held broken packages.
```

这里就是踩坑的开始。在google上看了n多帖子，尝试了很多方法，发现都行不通。比如说安装build-essentials，更新软件什么的，都不行。具体可以看这个[帖子](https://askubuntu.com/questions/223237/unable-to-correct-problems-you-have-held-broken-packages/1274779#1274779)，谈论的比较多。不过怎么尝试就是安装不了。后来无意中看[CediOsman的博客](https://blog.csdn.net/zhangjiahao14/article/details/80554616)，里面谈到更换ubuntu的软件源时，得根据版本号来。由于我们安装的版本是` Ubuntu 20.04.1 LTS`，比较新。网上的ubuntu的软件源得修改一下才能用，不修改很多的软件都安装不了。因此可以按下面的步骤来安装：

1. 查看新版本信息

```
$ lsb_release -a
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 20.04.1 LTS
Release:        20.04
Codename:       focal
```

　　这个codename也就是系统代号是很重要的。

2. 重新更换中科院的源

　　由于网上很多软件源都是用于系统代号为`bionic`的ubuntu系统，所以这里一定要改成`focal`。打开sources.list，`sudo vim /etc/apt/sources.list`将原来的东西清空，把下面的源地址粘贴上去：

```
# 默认注释了源码仓库，如有需要可自行取消注释
deb https://mirrors.ustc.edu.cn/ubuntu/ focal main restricted universe multiverse
# deb-src https://mirrors.ustc.edu.cn/ubuntu/ focal main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
# deb-src https://mirrors.ustc.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
# deb-src https://mirrors.ustc.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ focal-security main restricted universe multiverse
# deb-src https://mirrors.ustc.edu.cn/ubuntu/ focal-security main restricted universe multiverse

```

3. 更新ubuntu的源及相关软件

```shell
sudo apt-get update
sudo apt-get update
```

　　没有报错的话，证明软件源更新成功。

4. 安装g++

```
sudo apt-get install g++
sudo apt-get install r-base-dev #最好把这个安上，可以解决很多
```

　　看到ｇ++软件没有报错，安装成功，瞬间就觉得前面的折腾值了。

5. 安装R软件包

　　直接`install.packages("httr")`安装httr也会报错，除了`g++`还需要安装一些底层库。不过由于`g++`这最基本的编译器已经安装好，后面就很简单，就是几句代码的事。

```shell
#curl是httr的依赖库，不安装libcurl4-openssl-dev也会报错。
sudo apt-get install libcurl4-openssl-dev 
# openssl也是httr依赖库，不安装libcurl4-openssl-dev也会报错。
sudo apt-get install  libssl-dev
```

　　然后进入R交互窗口安装`httr`包，直接`install.packages("httr")`安装。看到下面的信息表示已经成功安装。

```
*** installing help indices
** building package indices
** installing vignettes
** testing if installed package can be loaded from temporary location
** testing if installed package can be loaded from final location
** testing if installed package keeps a record of temporary installation path
* DONE (httr)

The downloaded source packages are in
        ‘/tmp/Rtmp993tUS/downloaded_packages’
```

　　Finally，搞定WSL的基本配置，可以愉快地使用`bash`了。

