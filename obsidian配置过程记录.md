>本篇用来记录我安装配置obsidian的过程

因为在知乎上看到这个obsidian的功能十分强大，且轻量便捷，于是打算自己配置一下，用obsidian来作为之后自己的笔记软件，代替臃肿复杂的**有道云笔记**、难以用手机进行多端同步的**vscode**以及格式复杂不通用的OneNote。

等配置完obsidian后我打算将自己配置的github+hexo个人博客网站作为我生活学习到一定阶段时来发布学习总结和感悟的平台（*平常对于一些刷题的思路和项目上的想法也能整理到博客上*），而obsidian则是用来作为我日常的笔记软件（*毕竟用hexo里直接写md文件还得运行本地博客才能看见结果，而直接提交到github上又需要几分钟才能同步，而且网速也很感人...*）

总而言之，我的博客平台用来做一些比较专业的、大规模的学习整理，而obsidian则是用来作为日常笔记，所有废话可能有点多（*比如现在*）。

言归正传，下面是我搭建obsidian的过程记录。

# 1.下载obsidian

当然是直接去官网下载：[Obsidian官方下载](https://obsidian.md/)

# 2.在git托管平台创建新仓库

略，github和gitee随便选一个创建仓库就行

# 3.配置本地仓库

```shell
touch README.md 
git init 
git add README.md 
git commit -m "first commit" 
git branch -M main 
git remote add origin "仓库地址" 
git push -u origin main
```

# 4.配置obsidian-git插件

这里很重要，国内的obsidian可能打不开第三方插件的插件市场，所以需要下载一个[obsidian-proxy-github](https://github.com/juqkai/obsidian-proxy-github)插件，并解压到笔记本目录下的.obsidian/plugins/目录中（没有plugins就自己创建），然后在obsidian的第三方法