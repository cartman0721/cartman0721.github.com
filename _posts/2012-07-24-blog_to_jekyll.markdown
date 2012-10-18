---
layout: post
title: blog 迁至Jekyll
---

今天把blog从nodejs迁到了jkeyll，原因是每个月写不了几篇文章，每次给vps续费的时候都要小小的挣扎下，有时候还会生出罪恶感来。。jekyll 把文章寄托在github上，安全可靠，与vps完全撇清关系，而且保留我最爱的markdown的书写方式。

jekyll原生的几个模版都被我嫌太复杂，我需要一个简洁到可以装逼的模版，不需要分页，不许要category，甚至都不需要tag。我现在的模版就是这样一个简介到极致的模版，是从原来的博客里把样式抠过来的，当然有些抠的方式不是很高明，但样子上总体让我满意。

还有个未解决的问题是由于汉字的编码是三个字符，首页在truncate的时候容易出现乱码（当天刚刚truncate到汉字的一半的时候）。

###test code

	intro: function intro(markdown) {
	    var html = Markdown.encode(markdown);
	    return html.substr(0, html.indexOf("</p>"));
	  },
	  
	  
###test image

本地的

![sss]({{site.img_url}}/img.jpg)

第三方的

![book](http://img1.douban.com/lpic/s10393872.jpg)
