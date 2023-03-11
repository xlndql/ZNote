>本篇用来记录我安装配置obsidian的过程

因为在知乎上看到这个obsidian的功能十分强大，且轻量便捷，于是打算自己配置一下，用obsidian来作为之后自己的笔记软件，代替臃肿复杂的**有道云笔记**、难以用手机进行多端同步的**vscode**以及格式复杂不通用的OneNote。

等配置完obsidian后我打算将自己配置的github+hexo个人博客网站作为我生活学习到一定阶段时来发布学习总结和感悟的平台（*平常对于一些刷题的思路和项目上的想法也能整理到博客上*），而obsidian则是用来作为我日常的笔记软件（*毕竟用hexo里直接写md文件还得运行本地博客才能看见结果，而直接提交到github上又需要几分钟才能同步，而且网速也很感人...*）

总而言之，我的博客平台用来做一些比较专业的、大规模的学习整理，而obsidian则是用来作为日常笔记，所有废话可能有点多（*比如现在*）。

言归正传，下面是我搭建obsidian的过程记录。

# Windows端

## 1.下载obsidian

当然是直接去官网下载：[Obsidian官方下载](https://obsidian.md/)

## 2.在git托管平台创建新仓库

略，github和gitee随便选一个创建仓库就行

## 3.配置本地仓库

```shell
touch README.md 
git init 
git add README.md 
git commit -m "first commit" 
git branch -M main 
git remote add origin "仓库地址" 
git push -u origin main
```

## 4.配置obsidian-git插件

这里很重要，国内的obsidian可能打不开第三方插件的插件市场，所以需要下载一个[obsidian-proxy-github](https://github.com/juqkai/obsidian-proxy-github)插件，并解压到笔记本目录下的.obsidian/plugins/目录中（没有plugins就自己创建），然后在obsidian的第三方插件中打开这个插件，就可以进入插件市场了。

之后搜索obsidian-git就可以下载了，但是我在插件市场下载的obsidian-git无法开启，缺少了一个main.js文件，所以我还是去了github上的[obsidian-git](https://github.com/denolehov/obsidian-git/tags)下载压缩包后解压到plugins目录下才加载成功的（下载最后一个download而不是前面的zip）。

安装完开启obsidian-git插件后填写插件设置下面的提交姓名和邮箱，并自己调整一下自动提交的设置就可以了。

# Android端

## 1.下载obsidian

官方下载地址我没有找到，找到了第三方的下载地址：[obsidian-Android](https://mobile.softpedia.com/apk/obsidian)

##