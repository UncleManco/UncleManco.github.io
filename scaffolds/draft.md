---
title: 打造自己的独立博客GithubPages+Hexo+Next | Next主题深度优化
date: 2018-07-02 21:12:20
categories: "Hexo"
tags:
  - 教程  
---
{% qnimg 0.jpg alt:远方的路 走走停停 'class:class1 class2'alt: %}





优秀的githuber已经把你可能要用到的优化插件集成在hexo的主题中。



### 开通gitment评论

>Gitment 是一款基于 GitHub Issues 的评论系统。支持在前端直接引入，不需要任何后端代码。可以在页面进行登录、查看、评论、点赞等操作，同时有完整的 Markdown / GFM 和代码高亮支持。尤为适合各种基于 GitHub Pages 的静态博客或项目页面。

进入Next主题的配置文件themes\next\_config.yml中，查找[gitment]: https://github.com/imsun/gitment 就可以找到相关的配置项，如下：

题外话，这里提供了两个评论的插件，一个是Valine一个是gitment。我是先试了Valine，但是没有成功，最后用了gitment。

~~~ bash
gitment:
  enable: true
  mint: true # RECOMMEND, A mint on Gitment, to support count, language and proxy_gateway
  count: true # Show comments count in post meta area
  lazy: false # Comments lazy loading with a button
  cleanly: false # Hide 'Powered by ...' on footer, and more
  language: # Force language, or auto switch by theme
  github_user: #github的账号名
  github_repo: #github中博客的仓库
  client_id: 
  client_secret: 
  proxy_gateway: # Address of api proxy, See: https://github.com/aimingoo/intersect
  redirect_protocol: # Protocol of redirect_uri with force_redirect_protocol when mint enabled
~~~

这时候，你只需要去 [OAuth Application]: https://github.com/settings/applications/new 注册一个新的OAuth Application，如下图：

{% qnimg hexo_gitment1.png %}

注册即生成 client_id 和 client_secret，填入到配置项中，同时补上github_user和github_repo，把enable设置为true。搞定！重新部署后就可以看到文章后面有评论框，但每篇文章的评论都需要你点击初始化，登录github授权后就可以搞定。


### 开通访问统计、博客字数统计等统计功能

如果你找到旧一点的教程，他们会让你在代码里加入第三方统计插件，如不蒜子，而这些在新版本的主题里面。咱优秀的githuber已经帮我们加进来，同样的，只需要在主题配置文件里开启即可。

进入配置文件themes\next\_config.yml中搜索busuanzi，找到配置项目如下：
~~~ bash
busuanzi_count:
  # count values only if the other configs are false
  enable: true
  # custom uv span for the whole site
  site_uv: true
  site_uv_header: <i class="fa fa-user"></i>访客数
  site_uv_footer:
  # custom pv span for the whole site
  site_pv: true
  site_pv_header: <i class="fa fa-eye"></i>访问量
  site_pv_footer:
  # custom pv span for one page only
  page_pv: true
  page_pv_header: <i class="fa fa-file-o"></i> 阅读量
  page_pv_footer:
~~~

这里会将你博客主站的累积访客数、访问量，以及每篇文章的阅读量加上去。如果你还想展示博客文章总字数、每篇文章的字数统计、预估阅读时长，继续搜wordcount，配置如下：

~~~ bash
post_wordcount:
  item_text: true
  wordcount: true
  min2read: true
  totalcount: true
  separated_meta: true
~~~

开通以后只有图标和统计字数，如果你跟我一样都是小白，还需要去到themes\next\layout\_macro\post.swig，找到它们的html，在后面加入中文显示，如下：
<i class="fa fa-file-word-o"></i> 文章字数
<i class="fa fa-clock-o"></i> 预估阅读时长
