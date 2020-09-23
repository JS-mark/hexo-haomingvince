---
title: hexo + next8.0开启Valine评论系统及添加留言板功能
date: 2020-09-21 07:18:06
tags: 
- 杂谈
- Hexo
categories:
- 记录
---

# 前言

经过前三轮的折腾，你已经拥有一个自己定义的静态页面了，是时候给它添加一个留言板功能了。next主题自带了多种留言功能的插件，比如畅言，disqus，disqusjs，gitalk，livere，valine。 valine是其中相对简洁并且限制较少的一款轻量型博客评论系统。本文将教你如何开启并美化valine评论系统。如果你还没有配置你自己的博客，可以参考我的[前几篇文章](https://haomingzhang.com/tags/Hexo/)。

<!--more-->

> 可以通过右边的文章目录快速跳转哦！

# 开启valine评论系统

## 1. 注册 Leancloud 账号

在leancloud官网注册一个账号，海外同学推荐使用leancloud国际版，国内同学可以使用华东或华北节点。本文将使用国际版作为演示，国内版有些许不同，同学们可以自行查阅网上的资料。

![](https://cdn.jsdelivr.net/gh/haomingvince/ghcdn@master/hexo_pic/14.png)

注册完成后进入app控制面板->创建应用->创建开发版应用。

![](https://cdn.jsdelivr.net/gh/haomingvince/ghcdn@master/hexo_pic/15.png)

接下来我们配置一下我们的leancloud。点击设置->安全中心->Web 安全域名，输入你的域名来保证其他人就算获取了你的appid也没办法操作你的数据库。

![](https://cdn.jsdelivr.net/gh/haomingvince/ghcdn@master/hexo_pic/16.png)

接下来点击应用keys获取你的appid和appkey。

![](https://cdn.jsdelivr.net/gh/haomingvince/ghcdn@master/hexo_pic/17.png)

## 2. 在next主题中配置valine

打开 _config.next.yml，找到comments栏目并开启valine。

```yml
comments:
  active: valine
```

往下滑动进入valine设置栏，开启valine并填入你的appid和appkey。

```yml
valine:
  enable: true
  appId:  # Your leancloud application appid
  appKey:  # Your leancloud application appkey
  placeholder: "输入你的评论\n昵称为必填项目，输入QQ号可以直接获取用户名和头像，并且省去了填写邮箱的麻烦！\n虽然email不是必选，但是填写了email可以收到推送通知哦！" # Comment box placeholder
  avatar: "" # Gravatar style
  meta: [nick, mail] # Custom comment header
  pageSize: 10 # Pagination size
  lang: # Language, available values: en, zh-cn
  visitor: true # Article reading statistic
  comment_count: true # If false, comment count will only be displayed in post page, not in home page
  recordIP: true # Whether to record the commenter IP
  serverURLs: # When the custom domain name is enabled, fill it in here (it will be detected automatically by default, no need to fill in)
  enableQQ: true # Whether to enable the Nickname box to automatically get QQ Nickname and QQ Avatar
  requiredFields: [nick] # Set required fields: [nick] | [nick, mail]
```

这里稍微解释一下各个参数的用途。  
placeholder是在用户未输入任何参数时默认显示的值；  
avatar是默认用户头像，参考[link](https://valine.js.org/avatar.html)；  
meta是可以选择的用户信息栏；  
enableQQ可以自动匹配用户在nick栏目的输入，若是QQ，直接拉取用户的QQ头像和昵称作为评论使用，推荐开启（目前有个bug，若用户QQ昵称小于三个字符，可能出现拉取失败，等待大佬更新）；  
其他的配置可以参考[link](https://valine.js.org/configuration.html)。

> 至此你的评论系统已经开启。

## 3. 在菜单栏添加留言板

添加一个新的page

```sh
$ hexo new page guestbook
```

进入 source/guestbook/index.md。加入你想显示的内容，如：

```md
---
title: 留言板
date: 2020-09-13 13:34:29
---
# 欢迎来到我的博客！

> 欢迎在这里留言！任何问题都可以在这里留言，我会及时回复的，添加email可以获得更快的回复速度，在nickname栏目输入QQ号可以直接获取你的QQ头像。
```

进入 _config.next.yml， 找到menu栏目，添加留言板功能：

```yml
menu:
  guestbook: /guestbook/ || fa fa-book
```

图标支持font awesome，可以按自己喜好修改。

如果有多语言支持需求，可以更改 themes/next/languages 下对应语言的翻译。

en.yml:

```yml
menu:
  guestbook: guestbook
```

zh-CN.yml:

```yml
menu:
  guestbook: 留言板
```

## 4. 重新生成页面即可

```sh
$ hexo clean
$ hexo g -d
```

# 小结

valine比较简洁、配置简单且免费，非常推荐作为个人博客的评论系统来使用。网上有很多魔改版本的valine可以实现更多功能，有需要的同学可以自行查阅哦！如果有任何关于本篇文章的问题欢迎留言。

## Upcoming next

更改Valine评论表情

# Reference

[我的页面设置](https://github.com/haomingvince/hexo-haomingvince/)