---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "商业网盘推荐和私有网盘构建"
subtitle: ""
summary: "推荐好用的同步网盘，及构建私有网盘策略"
authors: [章峰]
tags: ["网络","网盘","同步","私有"]
categories: ["网络"]
date: 2022-05-13
lastmod: 2022-05-13
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


## 备份网盘和同步网盘
我们经常听到“网盘”这一名词，我们以为“网盘”顾名思义是网络U盘/网络硬盘，将资料备份储存的网上空间，然而这只是“备份”的含义。严格来说，网盘的功能可以分为“备份”和“同步”，大部分人通常会将“备份”与“同步”混为一谈。

我们经常使用的百度网盘就是侧重备份，同步功能也有但比较弱。而同步网盘不仅具备网盘功能，其最大的特点为“同步”而非“备份”。同步网盘的意思即，在电脑A里安装软件后，在同步文件夹内的任何文件只要有更新或修改，会被自动上传到云端（不需手动上传），当电脑B也安装此软件时，在电脑A上自动上传到云端的文件会被自动下载到电脑B的同步文件夹中。移动设备亦然。这样在办公室没做完的文件可以直接被同步，在家里无缝链接地接着做。而不用U盘拷贝来拷贝去，有时还得比较哪些文件更新了，哪些没动。

## 商用网盘推荐
那么现在有哪些好用的网盘推荐呢？

### 备份网盘
备份网盘最重要的参数应该是**存储容量**。最开始备份盘都是1T，2T的免费送，但是市场证明免费的策略行不通，现在大部分都挂了。记得原来使用的360网盘，实在恶心，直接关闭，还不让你把数据下载回来，最后好像交了99块钱买了VIP服务才把数据下载下来。

现在还坚挺的不多，目前国内用的比较多还是[百度网盘](https://pan.baidu.com/)。虽然被吐槽各种限速和收费，但是大浪淘沙下来还是非常坚挺。2T的存储空间还是够用的。其它的软件，请看[10款好用的在线网盘服务推荐](https://www.v1tx.com/post/best-cloud-storage-services/)。

推荐：[百度网盘](https://pan.baidu.com/)  
体验感：全平台通用，用户非常广，分享的资源丰富。但是下载速度太慢。

### 同步网盘
同步盘比较流行的有：[坚果云](https://www.jianguoyun.com/)，[百度网盘](https://pan.baidu.com/)，OneDrive，Dropbox 和 Google Drive。

具体软件间的差异可以看[各大同步网盘的比较](https://sspai.com/post/40457)。由于某些原因，国外的网盘在国内都不是很好用，上传下载速度太慢。近几年百度网盘也有同步功能，但是限制流量，只有1G的空间。综合比较还是坚果云好用。

推荐：[坚果云](https://www.jianguoyun.com/)  
体验感：全平台通用，界面简洁，使用方便，还有增量同步功能，不限制容量。缺点是限制流量，免费版只有1G的上传流量和3G的下载流量。

## 自建网盘
如果你经历过：限速下载，限制分享，关闭服务，无故删除数据等，你可能会非常想有一个自己的私人网盘，我的数据我做主。相比商业网盘，私人网盘的优点是：安全性更高，没有任何限制。缺点是：需要自己维护，懂一些linux命令。当然两者都需要一些费用。

当然要实现这一目标，需要具备以下两点：
1. 首先得有一个服务器，用于构建环境及存储。
2. 还需要有一个公网IP，要不然只有在局域网才能登陆网盘。

作为一个不太懂计算机网络的人，目前有两种方式实现，推荐第一种：
1. 使用轻量服务器，网上购买阿里云等其它云服务，价格便宜，使用方便。
2. 在家里用一台电脑当服务器，但是得请网络商申请一个公网IP，24小时开机。

### 1 cloudreve 构建
[Cloudreve](https://github.com/cloudreve/Cloudreve)是一个开源的，在github上有10K的star。安装简单易懂，有人做了[阿里云搭建cloudreve视频](https://www.bilibili.com/video/BV1Ap4y1x7uE?spm_id_from=333.337.search-card.all.click)可以参考。

1. 安装
```
# 解压程序包
tar -zxvf cloudreve_VERSION_OS_ARCH.tar.gz

# 赋予执行权限
chmod +x ./cloudreve

# 启动 Cloudreve
./cloudreve
```
2. 网页
通过http://IP:5212/ 来访问。

优点：安装方便，界面简洁，国人开发有中文文档说明，下载和上传速度非常快。  
缺点：体验使用的人较少，说明文档不多，没有同步功能，没有客户端，只支持windows和linux两种平台。

### 2 nextcloud 构建
[nextcloud官网](https://nextcloud.com/)有安装教程，但是是英文的，网上也有一些[nextcloud 中文教程](https://wzfou.com/nextcloud-pan/#ftoc-heading-2)。

优点：全平台支持，上传速度快，有自动同步功能，插件多功能丰富。  
缺点：英文说明文档，不能上传文件夹，同步文件没有虚拟功能，全部同步占用空间。

### 3 seafile 构建
Seafile和Syncthing 二者均开源，但Seafile教程和应用更多一些。
1. Seafile 适合用在自建服务器上（如 VPS、NAS），类似的还有 ownCloud 和 NextCloud；
2. Syncthing 类似之前的 BitTorrent Sync （现在叫 Resilio），同步的各个设备可以认为是平等的，适合在个人多台电脑之间同步。

[Seafile官网](https://www.seafile.com/home/)上找到[安装教程](https://www.seafile.com/download/)，也有[seaFile 同步盘搭建视频教程](https://www.bilibili.com/video/BV13r4y187cL?spm_id_from=333.880.my_history.page.click)。

#### 3.1 seafile 服务器安装
[服务器安装](https://cloud.seafile.com/published/seafile-manual-cn/overview/components.md)，推荐用docker安装开源版seafile
1. 安装 docker-compose
```
apt-get update
apt-get install docker-compose -y
```
2. 下载并修改 docker-compose.yml
下载到本地进行修改，再上传到服务器

3. 启动 Seafile 服务
```
docker-compose up -d
```
需要等待几分钟，等容器首次启动时的初始化操作完成后，您就可以在浏览器上访问http://IP:端口号来打开主页。

#### 3.2 客户端
支持全平台，直接下载安装，界面简洁，方便上手。

优点：全平台支持，有自动同步功能，上传速度快，官方是中文说明文档
缺点：暂未发现

### 4 用git进行同步
将服务器当做远端仓库，从本地A端推送上去。另一台电脑B端clone下来。
实践下来发现，如果数据超过100M的话，家庭宽带上行速度太慢，push不上。此外，git对大文件不太友好，也限制了同步的功能。



## 小结
- 如果图方便，备份盘选择百度网盘，同步盘选择坚果云。
- 如果看重文件安全及稳定，想自己在服务器上搭建私人网盘，推荐用seafile搭建。

## 参考资料

[如何搭建自己的私有云盘](https://zhuanlan.zhihu.com/p/44103820)  
[对比9大开源网盘程序，自建网盘指南](https://www.bilibili.com/video/BV1mF41137Vc?spm_id_from=333.880.my_history.page.click)