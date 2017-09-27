---
title: '如何使用Bootstrap创建有逼格的web界面'
layout: post
tags:
    - bootstrap 
    - simple
    - css
    - web
---
我和大家一样，打算在知乎上找一个有“格调”的jekyll的模板，嗯，找到这个帖子[知乎——有哪些简洁明快的 Jekyll 模板？](https://www.zhihu.com/question/20223939)。看到了一些同学的推荐，[cellier](http://cellier.me/blog/)这个博客样式。真的漂亮！但没有找到cellier同学的博客源码，于是我使用Bootstrap来实现了一把。使用Bootstrap没有其它理由，纯是因为我只听过她。好吧，谁叫我是个后端程序员呢！

现在这个主题已经做成一个基于jekyll模板进行开源，这里是地址：[github-simplist-jekyll-template](https://github.com/Zuofan/jekyll-blog-template)，希望各位喜欢。
<!--more-->

<div class="table-contents">table of contents@TOC</div>
# 概述
如果要看原主人的BLOG，请点击[cellier](http://cellier.me/blog/)。如果我的做法冒犯到原作者，请联系我告诉我怎么做！

我主要模仿了主界面的文章列表、Blog的文章页面。

文章列表页面，我主要使用了futura-pt字体，没有使用Hypatia-Sans-Pro-ExtraLight字体，主要是因为如果有标签是中文的话，其显示效果有别于英文。 下图是主界面的文章列表：

Blog的文章页面会依据是否有图，调整样式，我觉得有些拖沓，不够简洁，所以去除了。主题内容显示，我使用了[typo.css](https://github.com/sofish/)，来利于中文排版，增强阅读效果。

移动端。我使用Bootstrap的机制来支持响应式，修改了显示的样式，以求和此主题相切合。使用CSS3动画和jQuery（嗯，只有一句话而已），实现了菜单显示的动画。

添加archive、about页面样式。

增加了社交图标。因为我只要几个社交图标即可，所以不准备使用整个`font-awesome`的所有图标库。但发现好像多此一举了，方法虽然降低了下载文件的体积，但仍然需要下载文件，而我本意是直接将svg的图标直接复制到css文件上，就没有下载文件的问题了，但为了兼容性，又走回老路了。

注意：在每一篇文章中需要加上文章简介，否则jekyll会默认选取第一段作为文章简介。为了更好地控制列表显示文章的效果，所以我使用了定制文章简介的方式：在简介后加上`<!--more-->`进行标识，`<!--more-->`和`_config.xml`中的`excerpt_separator`值相对应。你可以查看本篇文章的源码。

## 主界面的文章列表的样式
主要修改Bootstrap默认的页头样式，看一下页头修改的前后对比图片。

修改之前的：
![css-simple-index-header-old]({{ site.siteurl }}/media/files/2017/css-simple-index-header-old.png)

修改之后的：
![css-simple-index-header-new]({{ site.siteurl }}/media/files/2017/css-simple-index-header-new.png)

嗯，看起来，好像修改之前的比修改之后的好看，这主要是因为截图的分辨率的问题。

### 页头

1. 修改链接样式
		
        a { color: #1f1f1f;font-family: "futura-pt", "proxima-nova","Helvetica Neue",Helvetica,Arial,sans-serif;}
        a:focus, a:hover{text-decoration: none;color:inherit;}
        
        .navbar-default {background-color:#ffffff;border:none;}
          
        .navbar-default .navbar-nav > .active > a, 
        .navbar-default .navbar-nav > .active > a:hover,
        .navbar-default .navbar-nav > .active > a:focus {
            background-color: #fff;
            color: #000;
        }
        
        .navbar-default  a {
            font-size: 14px;
            text-transform: uppercase;
            text-decoration: none;
            letter-spacing: 1px;
            font-weight: 400;
            font-style: normal;
            line-height: 1em;
            color: #515252;
        }
        
        .navbar-default  .navbar-brand > a {
            font-weight: 600;
            font-size: 20px;
            letter-spacing: 2px;
            letter-spacing: 1.4px;
            font-style: normal;
            color: #000;
        }
        
        .navbar-default .navbar-nav > li > a:hover,
        .navbar-default .navbar-nav > li > a:focus {
            background-color: #fff;
            color: #000;
        }
        
2. 修改移动端的页头样式

	修改之前的：

	![css-simple-index-header-mobile-old]({{ site.siteurl }}/media/files/2017/css-simple-index-header-mobile-old.png)

	修改之后的：
	
	![css-simple-index-header-mobile-new]({{ site.siteurl }}/media/files/2017/css-simple-index-header-mobile-new.png)

	下面是移动端的修改样式：

        .navbar-default .navbar-toggle:hover, 
        .navbar-default .navbar-toggle:focus {
            background-color: white; 
        }
        
        .navbar-default .navbar-toggle {border:none;}
        
        .navbar-default button:active,
        .navbar-default button:focus {
            border-style: none;
            outline:none;
        }
        
        .navbar-default .navbar-toggle:hover,
        .navbar-default .navbar-toggle:focus {
          background-color: transparent;
        }
        
        .navbar-default .navbar-toggle .icon-bar {
            background-color: #515252;
            border: 1px solid transparent;
        }

	为移动端的菜单添加CSS3动画，并响应用户的点击动作

        //html-code
        <button type="button" class="navbar-toggle cross-rotate" data-toggle="collapse" data-target=".navbar-collapse">
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
        </button>
        
        //css-code
        .cross-rotate {
            -webkit-transition-duration: 1s;
            -moz-transition-duration: 1s;
            -o-transition-duration: 1s;
             transition-duration: 1s;
            -webkit-transition-property: -webkit-transform;
            -moz-transition-property: -moz-transform;
            -o-transition-property: -o-transform;
             transition-property: transform;
        }
        
        .cross-rotate.active {
            -webkit-transform: rotate(90deg);
            -ms-transform: rotate(90deg);
             transform: rotate(90deg);
        }
        
        //javascript-code
        <script src="/media/js/jquery.js" type="text/javascript"></script>
        <script src="/media/js/bootstrap.js" type="text/javascript"></script>
        <script type="text/javascript">
          $('.cross-rotate').on('click', function(){
            $(this).toggleClass('active');
        });

### 文章列表
文章列表主要在3个地方应用CSS规则，如下图所示：
![css-simple-index-content]({{ site.siteurl }}/media/files/2017/css-simple-index-content.png)

下面我们看一下具体的CSS规则，主要分为article-header、article-body、article-footer。

        article   *, .article *,#tag_cloud {
         font-family: "futura-pt", "proxima-nova","Helvetica Neue",Helvetica,Arial,sans-serif;
        }
        
        //article-header
        .article .article-header {
            text-align:center;
            margin:.6em 0 1em;
            font-size: 1.5em;
        }
        .article .article-header .header-title {
              margin: .15em 0 .25em;
          }
          .article .article-header .header-category a,
          .article .article-header .header-dateline {
            color: rgba(31,31,31,.5);font-family: "futura-pt";
          }
        
        
        //article-body
        .article  .article-body,
        .article  .article-summary{
            font: 300 1.5em/1.8 "futura-pt", "proxima-nova","Helvetica Neue",Helvetica,Arial,sans-serif;
          }
        .article  .article-body img {
            display:block;
        }
        
        //article-footer
        .article > .article-footer  {
          margin: 1em 0 2em;
        }
         .article > .article-footer a {
            color: rgba(31,31,31, .5);
            text-decoration: none;
            font-size: 1.5em;
            line-height: 1.8em;
          }
        .article > .article-footer a:before {
            content: "Read More";
        }
         .article > .article-footer a:after {
            content: " \279D";
            font: normal .9em sans-serif;
            color:rgba(31, 31, 31, .45);
        }

## Blog的文章页面样式

用的就是主界面的文章样式。

## Archive列表样式

        ul.listing { margin-top: 1em; }
        ul.listing li {
            font-size: 1.4em;
            list-style-type: none;
            padding: 0; 
        }
        
        ul.listing li.listing-item a, 
        ul.listing li.listing-item header #header h1 a, 
        header #header h1 ul.listing li.listing-item a {
              padding: .2em 0 .2em 2em; 
        }
        
        ul.listing li.listing-item time {
              color: #999; 
        }
        ul.listing li.listing-item:hover {
              background-color: #f9f9f9; 
        }
        ul.listing li.listing-seperator {
              font-family: telexregular, Hiragino Sans GB, Microsoft YaHei, sans-serif; 
        }
        ul.listing li.listing-seperator:before {
                content: "⭠ ";
                color: #ccc; 
        }

