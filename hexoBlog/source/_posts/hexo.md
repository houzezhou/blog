---
title: hexo 搭建
date: 2019-09-29
tags: 博客
categories: 博客
---

hexo 博客搭建
<!-- more -->


### 一、安装hexo


``` bash
npm install -g hexo-cli
```


### 二、建站

###### 1、新建文件夹

``` bash
hexo init <folder>
cd <folder>
npm install
```

###### 2、_config.yml 配置网站

More info: [Server](http://www.cnblogs.com/xiaoxuetu/p/hexo-guide.html)

###### 3、进入博客根目录，执行命令

``` bash
hexo new hello-hexo
```
完成后会在 source/_posts目录下多出一个文件 hello-hexo.md，可以编辑它，按照markdown的语法

###### 4、生成静态页面

``` bash
hexo g //会生成public目录，里面有生成的静态文件
```
###### 5、启动本地服务

``` bash
hexo s // 默认是 http://localhost:4000/
```

### 三、部署到github

##### 1、安装自动部署到github的插件

```
npm install hexo-deployer-git --save
```

##### 2、_config.yml中配置

```
# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: https://17it.github.io
root: /
        
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: https://github.com/17it/17it.github.io.git
  branch: master
```

##### 3、生成静态文件

```
hexo g
```


##### 4、发布

```
hexo deploy // 发布到github
```

#### 参考链接

搭建：[Server](https://17it.github.io/2019/07/18/Linux-CentOS-7.2.x%E4%B8%8A%E4%BB%8E0%E5%BC%80%E5%A7%8B%E6%90%AD%E5%BB%BA%E8%87%AA%E5%B7%B1%E7%9A%84hexo%E5%8D%9A%E5%AE%A2/)

主题：[Server](http://theme-next.iissnan.com/getting-started.html)

部署: [Server](https://www.cnblogs.com/xiaoxuetu/p/hexo-issue.html)
