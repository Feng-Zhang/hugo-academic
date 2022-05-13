---
title: "Anaconda使用教程"
subtitle: ""
summary: "较为全面地介绍Anaconda的使用方法，并以RNA-seq环境和R环境的安装进行举例"
authors: [章峰]
tags: ["生信","anaconda","conda","r-base","RNA-seq"]
categories: ["语言","workflow","conda"]
date: 2021-10-21
lastmod: 2021-10-28
featured: false
draft: false


# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: "Smart"
  preview_only: false

---

{{< toc  >}}

# Anaconda使用教程
## 参考资料
[中文博客推荐](https://zhuanlan.zhihu.com/p/32925500)  
[anaconda 官网教程](https://docs.anaconda.com/anaconda/navigator/tutorials/index.html)

## 一、什么是Anaconda？
### 1. 简介
Anaconda（官方网站）就是可以便捷获取包且对包能够进行管理，同时对环境可以统一管理的发行版本。Anaconda包含了conda、Python在内的超过180个科学包及其依赖项。

Anaconda可以创建不同的虚拟环境，以实现环境间的隔离，这样在不同环境中可以使用软件或依赖库的不同版本，避免不同版本间的冲突。

### 2. 特点
Anaconda具有如下特点：
- 开源
- 安装过程简单
- 高性能使用Python和R语言
- 免费的社区支持
- 适用于多平台：Windows, macOS, Linux


如果日常工作或学习并不必要使用1,000多个库，那么可以考虑安装[Miniconda](https://docs.conda.io/en/latest/miniconda.html)，这里不过多介绍Miniconda的安装及使用。

## 二、安装及镜像
### 1. 下载Anaconda
Anaconda官网下载地址：  https://www.anaconda.com/products/individual#linux  
Anaconda中国镜像下载： https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/  
miniconda下载地址： https://docs.conda.io/en/latest/miniconda.html#latest-miniconda-installer-links  

### 2. 安装Anaconda  
```
bash Anaconda3-2021.05-Linux-x86_64.sh  
# specify a different location below  
>>> /home/zhangfeng/bin/anaconda3  
```
注意指定安装目录时，不能进行修改。如果有错字，使用删除键也不行。    


### 3. 设置镜像
显示镜像：`conda config --show-source` 

默认有以下载通道：
```
channels:
  - conda-forge
  - bioconda
  - r
  - defaults
show_channel_urls: true
```
即从国外的服务器下载不同软件包。`- r`表示通过r通道下载软件，即指从 https://conda.anaconda.org/r/网站下载  
conda-forge是指从 https://conda.anaconda.org/conda-forge/网站下载  

默认下载网址为[Anaconda的官方服务器](https://conda.anaconda.org/)，安装包时下载速度很慢，所以设置国内镜像很重要。清华大学的[TUNA镜像源](https://mirror.tuna.tsinghua.edu.cn/help/anaconda/)有Anaconda仓库的镜像，我们将其加入conda的配置即可，即修改`~/.condarc`文件内容。conda会从.condarc中下载通道按顺序搜索软件包。  
defaults ：默认下载通道。如果不指定通道则从defaults通道下载。  
channel_alias：修改指向defaults的网址，我们可以用 https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/镜像代替。

修改后的.condarc文件：
```
channel_alias: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/pro
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2
  - conda-forge
  - bioconda
  - defaults
ssl_verify: true
show_channel_urls: true
channel_priority: disabled
```

conda-forge和bioconda通道里的软件包比较新，推荐使用。


### 4. 安装软件包注意事项  
安装一个包不成功的话，可能的原因有：
1. 在本平台（windows）上没有这个包，或没有相应的硬件支持。
2. 有依赖的包没有安装，可以网上查询一下可能的依赖包，先安装这个依赖包。
3. 如果之前安装好的，但由于其它软件的变动，可能导致无法使用。可以先卸载后再重新安装。
4. 有些包在conda和pip中的版本是不兼容的，因此应该尽量用conda来安装。如果在conda中没有这个版本，再用pip来安装。


## 三、conda常用命令


### 常用命令
```
conda create -n learn python=3  // 创建一个名为learn的环境并指定python版本为3(最新版本)
conda activate learn //激活learn环境
conda env list // 列出conda管理的所有环境
conda list // 列出当前环境的所有包
conda search --full-name <package_full_name> //搜索包
conda install requests //安装requests包
conda install -n root conda=4.6 // 将conda降回原来版本
conda remove requests //卸载requets包
conda remove -n learn --all // 删除learn环境及下属所有包
conda update requests 更新requests包
conda env export > environment.yaml  // 导出当前环境的包信息
conda env create -f environment.yaml  // 用配置文件创建新的虚拟环境
```

### 1. 验证conda已被安装
```
conda --version
```
终端上将会以 conda 版本号的形式显示当前安装conda的版本号。如： conda 3.11.0

### 2. 更新conda至最新版本
```
conda update anaconda #更新anaconda  
conda update conda
conda update --all #更新所有包  
```
执行命令后，conda将会对版本进行比较并列出可以升级的版本。同时，也会告知用户其他相关包也会升级到相应版本。当较新的版本可以用于升级时，终端会显示 Proceed ([y]/n)? ，此时输入 y 即可进行升级。  

### 3. 查看conda帮助信息
```
conda --help
conda -h
```

### 4. 卸载conda
```
rm -rf ~/anaconda3
```
直接删除Anaconda的安装目录即可。

### 5. 配置
anaconda默认会开机启动，为了避免这种情况，我们需要在`~/.condarc`文件中进行设置。
```
conda config --set auto_activate_base false
```

### 6. 路径及重命名
```
conda env list #可列出conda管理的所有环境
```

conda不能对环境进行重命名，如果直接将环境所在目录重命名的话：
```
mv /home/zhangfeng/bin/anaconda3/envs/test /home/zhangfeng/bin/anaconda3/envs/test1 #
```
使用软件会报错，因为会用到以前的test下的库。只能删除这个环境，重新建一个新环境。

## 四、管理环境
### 1. 创建新环境
```
conda create --name <env_name> <package_names>
```

- <env_name> 即创建的环境名。建议以英文命名，且不加空格，名称两边不加尖括号“<>”。
- <package_names> 即安装在环境中的包名。名称两边不加尖括号“<>”。
- 如果要安装指定的版本号，则只需要在包名后面以 = 和版本号的形式执行。如： `conda create --name python2 python=2.7` ，即创建一个名为“python2”的环境，环境中安装版本为2.7的python。
- 如果要在新创建的环境中创建多个包，则直接在 <package_names> 后以空格隔开，添加多个包名即可。如： `conda create -n python3 python=3.5 numpy pandas `，即创建一个名为“python3”的环境，环境中安装版本为3.5的python，同时也安装了numpy和pandas。
- --name 同样可以替换为 -n 。
- 默认情况下，新创建的环境将会被保存在 /Users/<user_name>/anaconda3/env 目录下，其中<user_name> 为当前用户的用户名。


### 2. 切换环境
```
conda activate <env_name>
```

- 如果创建环境后安装Python时没有指定Python的版本，那么将会安装与Anaconda版本相同的Python版本，即如果安装Anaconda第2版，则会自动安装Python 2.x；如果安装Anaconda第3版，则会自动安装Python 3.x。
- 当成功切换环境之后，在该行行首将以“(env_name)”或“[env_name]”开头。其中，“env_name”为切换到的环境名。如：在执行`conda activate python2`，即切换至名为“python2”的环境，则行首将会以(python2)开头。


### 3. 退出环境
```
source deactivate
```
- 当执行退出当前环境后，原本行首以“(env_name)”或“[env_name]”开头的字符将不再显示。

### 4. 显示已创建环境
```
conda info --envs
conda info -e
conda env list
```
结果中星号“*”所在行即为当前所在环境。Linux系统中默认创建的环境名为“base”。

### 5. 复制环境
```
conda create --name <new_env_name> --clone <copied_env_name>
```
- <copied_env_name>即为被复制/克隆环境名。环境名两边不加尖括号“<>”。
- <new_env_name>即为复制之后新环境的名称。环境名两边不加尖括号“<>”。
- `conda create --name py2 --clone python2`，即为克隆名为“python2”的环境，克隆后的新环境名为“py2”。此时，环境中将同时存在“python2”和“py2”环境，且两个环境的配置相同。

### 6. 删除环境
```
conda remove --name <env_name> --all
```
- <env_name> 为被删除环境的名称。环境名两边不加尖括号“<>”。




## 五、管理软件包
### 1. 查找可供安装的包版本

#### 1.1 精确查找
```
conda search --full-name <package_full_name>
```
- --full-name 为精确查找的参数。
- <package_full_name>是被查找包的全名。包名两边不加尖括号“<>”。
- 例如： `conda search --full-name python` 即查找全名为“python”的包有哪些版本可供安装。


#### 1.2 模糊查找
```
conda search <text>
```
- <text> 是查找含有此字段的包名。此字段两边不加尖括号“<>”。
- 例如： `conda search py` 即查找含有“py”字段的包，有哪些版本可供安装。


### 2. 获取当前环境中已安装的包信息
```
conda list
```
执行上述命令后将在终端显示当前环境已安装包的包名及其版本号。


### 3. 安装包
#### 3.1 在指定环境中安装包
```
conda install --name <env_name> <package_name>  
```

- <env_name> 即将包安装的指定环境名。环境名两边不加尖括号“<>”。
- <package_name> 即要安装的包名。包名两边不加尖括号“<>”。
- 例如： `conda install --name python2 pandas` 即在名为“python2”的环境中安装pandas包。


#### 3.2 在当前环境中安装包  
```
conda install <package_name>
```

- <package_name> 即要安装的包名。包名两边不加尖括号“<>”。
- 执行命令后在当前环境中安装包。如`
conda install gdal=2.4.3 `


#### 3.3 使用pip安装包
```
pip3 install see
```
当使用 conda install 无法进行安装时，可以使用pip进行安装。例如：see包。

pip 用法：
- 安裝：pip install PackageName
- 更新：pip install -U PackageName 
- 移除：pip uninstall PackageName
- 搜索：pip search PackageName
- 帮助：pip help
- 从github安装: pip install git+https://github.com/jkbr/httpie.git


#### 3.4 从http://Anaconda.org安装包
当使用 conda install 无法进行安装时，可以考虑从 http://Anaconda.org 中获取安装包的命令，并进行安装。

1. 在浏览器中输入： http://anaconda.org
2. 在SEARCH PACKAGES搜索框中输入要安装的包名，然后点击右边“放大镜”标志进行检索。
3. 搜索结果中有数以千计的包可供选择，此时点击“Downloads”可根据下载量进行排序，最上面的为下载最多的包。
4. 选择满足需求的包或下载量最多的包，点击包名。
5. “To install this package with conda run one of the following:”下方有安装命令，选择其中一个并粘贴在终端中执行。
6. 完成安装。

### 4. 卸载软件包
#### 4.1 卸载其它环境中的包
```
conda remove --name <env_name> <package_name>
```
- <env_name> 即卸载包所在指定环境的名称。环境名两边不加尖括号“<>”。
- <package_name>即要卸载包的名称。包名两边不加尖括号“<>”。
- 例如：`conda remove --name python2 pandas` 即卸载名为“python2”中的pandas包。


#### 4.2 卸载当前环境中的包
```
conda remove <package_name>
```
- <package_name>即要卸载包的名称。包名两边不加尖括号“<>”。
- 执行命令后即在当前环境中卸载指定包。
- 例如： `conda remove pandas` 即在当前环境中卸载pandas包。


### 5. 更新包

#### 5.1 更新所有包
```
conda update --all
conda upgrade --all
```
建议：在安装Anaconda之后执行上述命令更新Anaconda中的所有包至最新版本，便于使用。


#### 5.2 更新指定包
```
conda update <package_name>
conda upgrade <package_name>
```
- <package_name>为指定更新的包名。包名两边不加尖括号“<>”。
- 更新多个指定包，则包名以空格隔开，向后排列。
- 如： `conda update pandas numpy matplotlib` 即更新pandas、numpy、matplotlib包。

---

## 六、debug
- conda install 一直在Solving environment卡死
1. 可能是通道的原因，换一个通道 `conda update conda -c conda-forge`试试.
2. 删除安装缓存。`conda info`找到缓存地址，在package cache行。然后进行删除：
```
rm /home/disk2/xs/anaconda3/pkgs
rm /home/disk2/xs/.conda/pkgs
```

## 七、案例 

### 创建R环境并安装R软件及R包

```
conda create -n R # 创建一个R的环境
conda activate R #激活R环境
conda install -c conda-forge r-base #不能同时加 r-essentials，会导致环境冲突
conda update -c conda-forge r-base # 如果没有安装最新版本，用此命令尝试更新
conda install -c conda-forge r-packagename #安装r包
```
- 注意R包的名称前要加`r-`，如需要安装ggplot2，命令为`conda install -c conda-forge r-ggplot2`
- 有些r包有时就是安装不了。这时候可以直接进入R命令行，直接在R里面装。  


### 创建rnaseq环境
```
conda create -n rnaseq python=3
conda install -c bioconda fastqc multiqc trim-galore 
conda install -c bioconda samtools stringtie STAR

# 验证相关软件是否安装
fastqc --version
multiqc --version
trim_galore --version
samtools --version
stringtie --version
STAR --version
```
