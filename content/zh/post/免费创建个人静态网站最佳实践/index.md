---
title: "免费创建个人静态网站最佳实践：hugo+github+netlify"  
subtitle: ""  
summary: "利用hugo+github+netlify创建个人静态网站最佳方式，专注写作而不是网页控件。"  
authors: [风不止]  
tags: ["hugo","academic","静态网站"]  
categories: [网站]  
date: 2020-05-25T15:56:11+08:00
lastmod: 2020-07-06T15:56:11+08:00
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



## 一、前言

关于搭建一个博客或个人网站的好处不用我多说，但创建网站的难度可能会让人望而却步。本人从网络上获得过很多帮助，学到很多。很早就萌发了自己建网站并分享知识的想法，但是又不想在简书这类的网站上写作。原谅我是个拖延控，有时间就写一点，很可能一篇文章写好久，也不喜欢在网上编辑。此外，知识需要积累形成框架，由于平时我所有的笔记都放在有道云笔记中，复制粘贴到简书有时候格式不对，又不想进行二次编辑。最重要的是不够Geek（装逼）。

其实中间有过一段时间，利用hexo、github和github page创建过静态网站。但是用得不太顺手，原因有很多，比如：老是花时间在怎么改网页主题上，而不是专注在写作上；markdown（md）文件中的图片迁移很麻烦，网上的图片老是会丢失；github page 在国内打开很慢而且SEO不容易搜索到。因此，一直耽误到现在，但一直贼心不死，想得到一个不太需要维护，可以专注写作，文档可以同步（在别的电脑上也可以编辑），又很geek的网站。我的想法是把所有笔记保存在有道云笔记中进行维护和整理，需要分享的话可以在本地用typora写md文档。此外，md文档中的图片用图床解决移动问题，然后托管到git自动渲染成网页。这样只要图床不挂，分享或上传到其它平台就很方便，因为只要复制md文档就行。为什么不直接用有道云笔记中的md呢？因为插入图片得是VIP才行，而导出来的md文档里所有图片的超链接是私人链接，移到别的地方根本没办法显示图片。最终我觉得搭网站最好的方式是：hugo+github+Netlify。适合我的笔记保存和写作的最佳方式是：有道云笔记+typora+picgo。如果觉得太麻烦了，不想把博客和有道云笔记等之类的笔记工具连接在一起，也不会传到其它平台上，可以直接用typora写作，利用hugo的page bundle绑定图片。


关于利用hugo和Github建网站的博客很多，但是有些博客内容有些出入，可能是由于英文翻译或版本更新所造成的。这里建议大家直接看hugo的[英文官网](https://gohugo.io/getting-started/quick-start/)和[hugo in action](https://livebook.manning.com/book/hugo-in-action/about-this-meap/v-4/)，或者[官方翻译](https://s0gohugo0io.icopy.site)。此外，网上的博客可以进行参考。这篇博客主要针对搭建过程中可能遇到的问题进行记录，希望对大家有所帮助。  

## 二、原理

那么如何用静态网页创建网站呢？很多博客一上来就直接讲方法，怎么一步步运行，得到一个简陋的网页。但是不知其所以然，因此这里想先介绍一下基本原理，方便理解和后面的debug。

1. 首先你得在本地生成静态网页文件。这里推荐用hugo或hexo。
2. 然后把静态网页文件托管到github仓库。这里推荐使用git和gitlab工具。
3. 把远程的静态网页文件进行渲染，形成让大家可根据网址直接阅览的网页。可用github page和Netlify.
4. 找到有道云笔记的md文件，用typora进行编辑，并用图床解决图片容易丢失问题。

关于hugo和hexo，github和gitlab，github page和Netlify的差别网上有很多博客，这里就不赘述了。目前我觉得最好的方式是：hugo+github+Netlify。

## 三、快速入门

如果有相关静态网页生成的经历，可以直接忽略快速入门，直接到下一节：进阶。

### 1、本地生成静态网页文件

如果不想看英文的，可以参考[这篇](https://jdhao.github.io/2018/10/10/hexo_to_hugo/)和[这篇](https://mogeko.me/2018/018/)中文入门。

下面简要阐述过程：  

```
hugo new site hugo #建立站点以后，博客根目录下默认有这些文件和子目录：archetypes/  config.toml  content/     data/        layouts/     static/      themes/
cd hugo
git init
git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke # 安装主题
echo 'theme = "ananke"' >> config.toml
hugo new posts/my-first-post.md
hugo server 
```

这时出现类似下面的信息，说明生成静态网页成功。可以在浏览器上输入 http://localhost:1313/ 进行浏览。  

```
Building sites …
                   | EN
-------------------+-----
  Pages            | 11
  Paginator pages  |  0
  Non-page files   |  1
  Static files     | 39
  Processed images |  0
  Aliases          |  2
  Sitemaps         |  1
  Cleaned          |  0

Built in 37 ms
Watching for changes in E:\blogs\hugo\{archetypes,content,data,layouts,static,themes}
Watching for config changes in E:\blogs\hugo\config.toml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

如果出现下面的错误：  

```
hugo new posts/my-first-post.md
Error: "E:\blogs\quickstart\config.toml:3:1": unmarshal failed: Near line 3 (last key parsed ''): bare keys cannot contain '\x00'
```

这是因为E:\blogs\hugo\config.toml里面有一些NUL的间隔符，可能是由于echo的命令产生的。手动把它们删除就行了。


### 2、托管到github

把我们本地生成的静态网页托管到[github](https://github.com)上进行保存，而不用自己进行维护。  
首先在github上新建账号，并创建一个新的仓库，以仓库名为test为例。再下载安装[git](https://git-scm.com/) 。

```
cd .\public
git init
git add .
git commit -m "update"
git remote add origin https://github.com/你的git账户/test.git
git push origin master:master
```

这样就把东西上传到github上了。

为了方便发布网页，可以写成一个脚本，然后每次发布只要右键选择git bash here后运行./deploy.sh就可以。

```bash
#!/bin/bash

echo -e "\033[0;32mDeploying updates to GitHub...\033[0m"

# build the project
hugo
git add .

msg="rebuilding site `date`"

if [ $# -eq 1 ]
  then msg="$1"
fi

git commit -m "$msg"

# push source to github
git push origin master:master 
```





### 3、用Netlify渲染网页

最后我们用[Netlify](https://www.netlify.com)对托管到github上的静态网页进行渲染。很简单，可以看这篇[教程](https://kuleyu.github.io/hexolog/post/31808.html)。至此一个简陋的网页就建好了。记得改一下Netlify自动分配给你的域名，不过只能更改前缀。要求不高也还好了。  
下面简单描述一下操作步骤：
1. 用github的账号登陆[Netlify](https://www.netlify.com)。
2. 点击右上角的Create new site
3. 跳转到第一步，connect to git provider，选github
4. pick a repository，选择存放代码的仓库。
5. Build options and deploy。点击Deploying就ok了。
6. 等待一会配置，就会出现网址了。类似这样的https://priceless-morse-029791.netlify.app。
7. 复制粘贴网址就大功告成。


目前我们可以以网站形式来展示内容，但是初始化的见面一点也不cool啊。客官别急，请看下面进阶教程。




## 四、进阶

### 1、添加主题

首先我们可以到[hugo主题库](https://themes.gohugo.io)中找一个自己喜欢的主题。我比较喜欢的一个主题是academic，B站上还有人介绍[Academic视频](https://www.bilibili.com/video/BV1Tt411g7jx?p=2)。
由于大部分主题都已经有站点所需要的各种文件夹，所以不用自己再建站点。直接clone下来，把主题换成子模块的就行。快速入门的什么的可以忘记了^_^。

```
git clone https://github.com/sourcethemes/academic-kickstart.git My_Website
cd My_Website
git submodule update --init --recursive
```

### 2、修改网页布局

我们可以根据[academic文档](https://sourcethemes.com/academic/docs/)进行修改，变成你自己喜欢的样式。这个academic帮助文档讲得很清楚，这里就不赘述。

不过这里提一下添加评论系统，这应该是一个刚需。要不然没有互动在那孤芳自赏？

由于academic主题设置commento很方便，这里图方便直接用了：

1. 把config/_default/params.toml中的```engine = 0```改成```engine = 2```。  
2. ~~注册[commento](https://commento.io)账号，把你自己博客域名进行绑定即可。~~
commento后来发现是收费的，现改成valine。
3. valine的加载有点麻烦，可以参考[博客](https://www.smslit.top/2018/07/08/hugo-valine/)。  
此外，国外用的比较多的有Disqus，国内有valine和Gittalk。不过[Gitalk](https://github.com/gitalk/gitalk/)有点复杂，可参考这篇[博客](https://mogeko.me/2018/024/)进行安装。



## 五、写作

### 1、图片管理

在md文档中插入的图片是一个麻烦事。一般来说有三种解决方案。如下所示

#### 放置在static中

可以直接把图片放在static中，不过以后图片一多就麻烦了。如果后面想迁移什么的就太麻烦了。

#### 利用page bundle

可以在post下面新建文件夹，重命名为你想要的博客名后新建md文件。这个md文档名称一定得是**index.md**，然后我们就可在同一目录下放置图片。md可以使用相对位置进行引用。

其实如果不是为了在有道云笔记中同时显示md文件中的图片，这种方式是最方便的，而且免费。

#### 利用图床

这里利用picgo工具，把图片复制后，按一个快捷键就会自动上传到picgo内设置的图床上。  

[picgo教程](https://picgo.github.io/PicGo-Doc/zh/)支持8大图床。可以选免费的**smms**和github（虽然github慢了点），也可以氪金买云服务。

同时typora还支持picgo的插件，直接复制图片就可以实现上传到云端。不过配置可能会遇到些问题，可以参考这篇[博客排坑](https://www.jianshu.com/p/4cd14d4ceb1d)。

---

综上，图床是最方便的，但需要点时间配置各个软件。page bundle是最简单的，但是如果没法移动到其它平台。



### 2、更新博客的流程

日后更新博客时就只需要在本地的hugo\content\post文件夹中编辑新的md文件，然后```./deploy.sh```就会自动编译静态网页然后上传至github，同时Netlify会检测Github中库的动态，并及时更新发布的网站内容。  



### 3、在另一台电脑上写作

由于静态网页是托管到github，可以很方便地进行同步。直接用```git pull```把github拉下来就行，写完后```git push``` 到仓库就万事大吉了。

----

以上就是免费创建个人静态网站地最佳实践。全免费，渲染快捷且可以专注写作，不用费心维护。



## 六、域名

最后为了装一下，怎么也得换个个性化的域名啊。网上到处看了看，感觉比较复杂。因为在国内买域名还得备案，听说很麻烦。后来直接到name.com购买了域名。

### 域名解析

可以参考这篇[博客](https://www.cnblogs.com/codernie/p/9062104.html)。值得注意的是：在你的域名购买商处管理DNS的时候，要加两条DNS。一条是没有www，一条是有www。

![image-20200526113018470](https://i.loli.net/2020/05/26/3kwRGpLSuICDW8d.png)

## 七、Debug

- push error

```
git push academic master
remote: Permission to Feng-Zhang/academic-kickstart.git denied to xiaofeng007.
fatal: unable to access 'https://github.com/Feng-Zhang/academic-kickstart.git/': The requested URL returned error: 403
```

控制面板-用户帐户-凭据管理器-找到git:https://github.com-编辑  
对这个凭据进行编辑，把要远程的账号和密码加上。 

![image-20200526130114714](https://i.loli.net/2020/05/26/Ox6Gdy9sVJzlm71.png)