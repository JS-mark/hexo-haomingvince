---
title: 为hexo next8.0主题添加一个可以切换的黑色/夜间模式
date: 2020-09-16 20:58:30
tags: 
- 杂谈
- Hexo
categories:
- 记录
---

# 前言

虽然next 8.0 主题已经支持原生黑色模式，只需要在 _config.next.yml 文件中，将相应开关打开即可。

```yml
darkmode: true
```

但是这个黑色模式是不可以切换的，本文将介绍如何实现一个按钮来切换黑/白模式。如果你还没有自己的博客，可以参考我的前两篇文章：[hexo基本安装及配置](https://haomingzhang.com/hexo_1/)，[hexo主题安装以及next8.0主题美化](https://haomingzhang.com/hexo_2/)。

<!--more-->

# 具体步骤

## 1. 添加darkmode.js到你的next主题中

你可以下载 [Darkmode.js](https://github.com/sandoche/Darkmode.js) 或者直接添加他的cdn到你的vendors文件。（注：next8.0之前的版本没有接下来所提到的需要的文件，可以参考[这篇文章](https://dog.wtf/tech/hexo-dark-mode-note/)来配置你的黑色模式）

我的方法是直接在 themes/next/_vendors.yml 中添加 darkmode的 cdn：

```yml
darkmode_js:
  name: darkmode-js
  version: 1.5.7
  file: lib/darkmode-js.min.js
```
直接加在文件末尾即可。

## 2. 在你的 _config.next.yml 添加darkmode_js的相关开关：

```yml
vendors:
  #darkmode_js: https://cdn.jsdelivr.net/npm/darkmode-js/lib/darkmode-js.min.js
  darkmode_js:

# darkmode.js
darkmode_js: 
  enable: true
```
注意缩进！第一个darkmode_js是在vendors栏目下，第二个darkmode_js是一个单独的栏目。

## 3. 开启darkmode_js

打开 themes/next/layout/_scripts/vendors.njk，配置以下代码：

```yml
{%- if theme.canvas_ribbon.enable %}
  <script size="{{ theme.canvas_ribbon.size }}" alpha="{{ theme.canvas_ribbon.alpha }}" zIndex="{{ theme.canvas_ribbon.zIndex }}" src="{{ theme.vendors.canvas_ribbon }}"></script>
{%- endif %}

{# Customize darkmode.js - Declaration #}
{%- if theme.darkmode_js.enable %}
  <script src="{{ theme.vendors.darkmode_js }}"></script>
{%- endif %}

{%- for name in js_vendors() %}
  <script src="{{ url_for(theme.vendors[name]) }}"></script>
{%- endfor %}

{# Customize darkmode.js - Invokation #}
{%- if theme.darkmode_js.enable %}
<script>
var options = {
  bottom: '64px', // default: '32px'
  right: 'unset', // default: '32px'
  left: '32px', // default: 'unset'
  time: '0.5s', // default: '0.3s'
  mixColor: '#fff', // default: '#fff'
  backgroundColor: '#fff',  // default: '#fff'
  buttonColorDark: '#100f2c',  // default: '#100f2c'
  buttonColorLight: '#fff', // default: '#fff'
  saveInCookies: true, // default: true,
  label: '🌓', // default: ''
  autoMatchOsTheme: true // default: true
}
const darkmode = new Darkmode(options);
darkmode.showWidget();
</script>
{%- endif %}
```

因为此版本的动画特效已经精简为只有canvas_ribbon，更改后的配置文件就如上所示，其他可以根据情况自行更改。

## 4. 重新生成即可开启，点击按钮即可切换黑白模式

```sh
$ hexo clean
$ hexo g -d
```

# 小结

因为next团队在8.0版本更改了比较多的代码，网上既有的教程并不适用于8.0版本，如果有这个按钮需要的话，可以按照本文配置哦！可以参考我的配置（Reference栏）来进行修改，如果有任何问题欢迎留言。

最后效果
![](https://cdn.jsdelivr.net/gh/haomingvince/ghcdn@master/hexo_pic/darkmode.gif)

## Upcoming next

为你的博客添加留言板功能（[已更新](https://haomingzhang.com/hexo_4/)）

# Reference

[我的页面设置](https://github.com/haomingvince/hexo-haomingvince/)

[sandoche/Darkmode.js: 🌓 Add a dark-mode / night-mode to your website in a few seconds](https://github.com/sandoche/Darkmode.js)

[Hexo（Next 主题）实现可切换的 Dark Mode (暗色背景 / 夜间模式) | 雪泥鴻爪](https://dog.wtf/tech/hexo-dark-mode-note/)