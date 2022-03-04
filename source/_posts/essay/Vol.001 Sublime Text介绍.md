---
title: Sublime Text介绍
date: 2016-09-09 18:00:00
categories:
  - essay
tags:
  - sublime text
---
# 一、Sublime Text 介绍

### Sublime Text 特色

- 跨平台（Windows、Linux、Mac OS X）
- 支持众多编程语言，支持语法上色，可通过下载外挂支持更多编程语言
- 支持多行编辑啥的好用的小功能
- 支持主题~主题~~主题~~~折腾控福音Σ(ﾟ∀ﾟﾉ)ﾉ
- 最重要的是，插件众多！

# 二、一切的开始——Package Control

Package Control类似于ST上的APP Store，安装使用都比较简单

1. 复制以下代码：
   ```shell
   import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())
   ```
2. crtl+~开启console，粘贴+enter
3. ctrl+shift+p就可以打开辣~Σ(ﾟ∀ﾟﾉ)ﾉ

氮素！我发现Package Control被墙了！万恶的GFW！！！ヽ(●-`Д´-)ノ

大家装插件的话全局翻墙吧。。。இ௰இ

# 三、自用插件简单介绍

如图

![image1](/images/essay/001/image1.png)

其实有很多装了没用上。。。

我逐个介绍ヽ(•̀ω•́ )ゝ

# 四、强烈推荐的插件&使用方法

Emmet：主要用来提高编写HTML的效率，也可以用来写CSS，个人后者用的不多。

Emmet LiveStyle：能够做到ST、Chrome修改同步，即ST修改实时在Chrome上显示，Chrome控制台修改实时在ST上同步。

缺点是配置安装什么的比较麻烦，似乎需要科学上网。。。ヾ(｡｀Д´｡)

# 五、总结

挑喜欢的用吧~