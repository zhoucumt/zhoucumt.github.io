---
title: 本博客搭建方法
date: 2016-09-07 10:54:26
tags:
---

搭建这样一个博客还是很容易的，在网上随便找一篇教程，按照上面的步骤，都基本能搞定。但搭建的过程中，随着hexo版本的更新，之前教程没出现的问题，现在可能就出现了，所以踩了一些坑(比如在git版本控制中hexo init会干掉版本控制)，趁着还记得，赶快记录下来。
## 环境
mac系统，hexo + github。也就是利用github的博客功能，但是需要自己搭建。

## 前提
电脑已安装node环境，已安装git,已有github帐号，并有相应的git知识。

## 步骤
*1.创建仓库*

仓库名称为github帐号名称后面加上github.io,比如,我的github帐号为zhoucumt,那么仓库名称就是zhoucumt.github.io

*2.新建一个hexo分支*

由于在github上建立上述仓库后，默认创建了一个master分支，所以我们还需要创建另一个hexo分支，用于存放博客的源文件。直接在github网站上创建就可以了

*3.设置hexo分支为默认分支*

方法如图：
![image](/Users/baidu/Pictures/snip/settings.png)
然后在下图中，选择hexo之后update就可以了
![image](/Users/baidu/Pictures/snip/default.png)

*4.clone到本地*

``` bash
git clone git@github.com:zhoucumt/zhoucumt.github.io.git
```

成功之后，默认就处于hexo分支了。如果失败，则检测一下有没有add SSH KEYS，这里不再叙述这个，github网上也有方法，很简单。


*5.安装hexo*

``` bash
npm install hexo -g
```

*6.初始化*

完成第4步后，电脑中有了zhoucumt.github.io这个文件夹，cd进去，执行以下命令：

``` bash
hexo init
```

``` bash
npm install
```

``` bash
npm install hexo-deployer-git
```

**注意：**这个时候，坑就来了，因为你会发现这个时候版本控制信息居然不见了，你需要做如下处理
``` bash
git init
```

这个时候又回出现master分支了，但是hexo分支在命令行中还是没，需要我们重新再建一次。
``` bash
git branch hexo
```

但是，你会发现这个时候还是不能新建分支，此时你需要提交主干中的代码才可以，git add. git commit -m 'init' 这个时候再新建分支就没问题了

*7.配置_config.yml*

打开_config.yml文件，在文件最底部添加如下代码：
![image](/Users/baidu/Pictures/snip/config.png)

*8.依次执行git add .、git commit -m “…”、git push origin hexo提交网站相关的文件；*

*9.执行hexo generate -d生成网站并部署到GitHub上*


## hexo常用命令：新建一篇博文
*1.新建*

在zhoucumt.github.io（具体文件夹名称以你自己的github帐号不同而不同）
``` bash
hexo new 'how-to-create-blog'
```
注：可以看到此时source/_post中生成了how-to-create-blog.md,然后你就可以编辑你的博客了

*2.启动本地服务器*

``` bash
hexo server
```
浏览器输入http://localhost:4000,这个时候应该就可以看到生成的初始静态页面了（hexo低版本可能不能出现）

*3.生成编译后的静态文件*

``` bash
hexo generate
```
注：可以看到此时生成了public这个文件夹

*4.发布到github*

``` bash
hexo deploy
```
访问[link](https://zhoucumt.github.io/)就可以看到发布的博客文章了。



