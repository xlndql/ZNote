[(127条消息) 前端-工作中 npm install 安装依赖报错常见总结_西京刀客的博客-CSDN博客_npminstall安装包常见错误](https://docker.blog.csdn.net/article/details/120564807?spm=1001.2014.3001.5506)

前端-npm install 安装依赖报错解决

先清除缓存

```
npm cache clean --force
```

删除项目中的node_modules文件夹

安装淘宝镜像cnpm，用cnpm来安装依赖

```
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

最后再执行

```
cnpm install
```

报错The package-lock.json file was created with an old version of npm

问题背景：

npm install 报：

```
The package-lock.json file was created with an old version of npm
```

问题分析：

你使用npm太新了

解决方法：

```
npm i npm@6 -g 
npm -v
```