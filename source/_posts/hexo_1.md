---
title: hexo基本安装及配置
date: 2020-09-13 11:32:25
tags: 
- 杂谈
- Hexo
categories:
- 记录
---

# 前言

经过了快一星期的折腾，我的博客的各项功能也在陆续开通中，本文就来记录一下hexo + github pages心路历程及配置方法。

<!--more-->

> 可以通过右边的文章目录快速跳转哦！

# 安装hexo

## 需要准备的东西

1. github账号
2. git(本地)
3. node.js
4. npm
5. 个人域名(可选)

## 安装流程

### 申请[github](https://github.com/)账号

这里xxx填写你的github账户名称。如图：

![](https://cdn.jsdelivr.net/gh/haomingvince/ghcdn@master/hexo_pic/1.png)
![](https://cdn.jsdelivr.net/gh/haomingvince/ghcdn@master/hexo_pic/2.png)

### 创建一个新的仓库

命名为 xxx.github.io
![](https://cdn.jsdelivr.net/gh/haomingvince/ghcdn@master/hexo_pic/3.png)
![](https://cdn.jsdelivr.net/gh/haomingvince/ghcdn@master/hexo_pic/4.png)

### 电脑上安装 [git](https://git-scm.com/)

记得添加右键选单和加入PATH。具体git配置教程可以参考
[[Git & GitHub] Windows安装git和环境变量配置_Bluetata's Tech.Blog-CSDN博客](https://blog.csdn.net/dietime1943/article/details/71751007)

### 电脑上安装 [node.js](https://nodejs.org/en/download/)

记得加入PATH。此版本node.js集成了npm，可以再命令行中输入node -v 以及 npm -v 检查是否安装成功。
![](https://cdn.jsdelivr.net/gh/haomingvince/ghcdn@master/hexo_pic/5.png)

### 安装Hexo

使用命令行工具(cd xxxx) 进入你的博客文件夹，依次输入以下指令：  
安装hexo和hexo服务器模块

```sh
$ npm install -g hexo-cli
$ npm install hexo-server --save
```

初始化博客

```sh
$ hexo init blog
```

测试hexo是否安装成功：

```sh
$ hexo new test
$ hexo g
$ hexo s
```

其中hexo new test表示新建一篇名为test的博文，hexo g表示生成，是hexo generate的简写，hexo s在本地运行hexo服务器，是hexo server的简写。

成功后会有如下提示，进入 http://localhost:4000 即可看到刚刚生成的网页。
![](https://cdn.jsdelivr.net/gh/haomingvince/ghcdn@master/hexo_pic/6.png)

以下为配置完成后的样子，可能和你生成的页面不同，如果想配置和我一样的hexo可以继续阅读我的其他post。
![](https://cdn.jsdelivr.net/gh/haomingvince/ghcdn@master/hexo_pic/7.png)

### 配置到github pages

之前的操作只是在本地实现了我们的博客，如何推送到github pages呢？

首先，打开博客目录下的 _config.yml 文件

![](https://cdn.jsdelivr.net/gh/haomingvince/ghcdn@master/hexo_pic/8.png)

使用 ctrl+f 搜索deploy，并添加以下代码。注意！把xxx改为之前在github配置的名字即可。

```yml
deploy:
- type: git
  repo: https://github.com/xxx/xxx.github.io.git
  branch: master
```

接下来，安装hexo-deployer-git

```sh
$ npm install hexo-deployer-git --save
```

接下来就可以推送我们的网页到github啦！

```sh
$ hexo clean 
$ hexo g 
$ hexo d
```

其中hexo d表示deploy，是hexo deploy的简写，它会去config里面找到deploy栏目，然后根据你配置的deployer进行配置，十分方便！

### 访问网页

如果之前的步骤都是正确的话，那么恭喜你！你已经可以访问你的网页了！

比如我的网页： https://haomingvince.github.io

把haomingvince改成你的github用户名即可

### 绑定你自己的域名（可选）

如果你已经拥有你自己的域名的话那是最好，如果你想购买一个域名，可以去[腾讯云](https://dnspod.cloud.tencent.com/)，[阿里云](https://wanwang.aliyun.com/)，或者[godaddy](https://go.skimresources.com/?id=157360X1623833&xs=1&xcreo=500002&url=https://www.godaddy.com)购买。

由于我的域名是在godaddy购买的，接下来我会演示如何绑定你的github pages到godaddy，其他域名商操作应该也是雷同的。

登录你的godaddy后台，点击manage DNS
![](https://cdn.jsdelivr.net/gh/haomingvince/ghcdn@master/hexo_pic/9.png)

添加两条记录，一条CNAME，一条A记录，如图：
![](https://cdn.jsdelivr.net/gh/haomingvince/ghcdn@master/hexo_pic/10.png)
其中CNAME的value就填写你的github page的值，A的value可以通过ping xxx.github.io得到。

接下来，去到你的github page的settings界面，在Options->Github pages->custom domain添加你的域名：
![](https://cdn.jsdelivr.net/gh/haomingvince/ghcdn@master/hexo_pic/11.png)

最后一步，在你本地 /source 文件夹下添加一个名为CNAME的文件（注意，此文件没有后缀），里面添加你的域名即可。
![](https://cdn.jsdelivr.net/gh/haomingvince/ghcdn@master/hexo_pic/12.png)

再次执行deploy

```sh
$ hexo clean 
$ hexo g 
$ hexo d
```

稍等几分钟，你就可以用自己的域名访问你的网站啦！
![](https://cdn.jsdelivr.net/gh/haomingvince/ghcdn@master/hexo_pic/13.png)

# 小结

本文介绍了基本的hexo + github page的部署及实现，如果有任何问题，欢迎留言！

## Upcoming Next

Next 8.0 主题配置 （[已更新](https://haomingzhang.com/2020/09/13/hexo_2/)）

# Reference

[Vince's Blog](https://haomingzhang.com/)

[GitHub+Hexo 搭建个人网站详细教程 - 知乎](https://zhuanlan.zhihu.com/p/26625249)
