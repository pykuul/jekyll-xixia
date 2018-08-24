---
layout: post
title:  "Tạo Sitemap tự động cho website tạo bởi Jekyll và Github"
categories: Github Blog
tags: Github Blog
author: Richard Nguyen
description: 2 sites, one help to generate ASCII texts for you, another have lots of ASCII pics.
---
##Tạo Sitemap
Việc có một Sitemap và submit lên các công cụ tìm kiếm như Google sẽ giúp các công cụ tìm kiếm index trang của các bạn nhanh hơn. Để tạo file sitemap tự động các bạn làm như sau:

Các bạn mở file `_config.yml` tại thư mục gốc website của bạn, thêm vào các dòng lệnh sau:
{% highlight ruby %}
gems: 
  - jekyll-sitemap
{% endhighlight %}
Các bạn commit thay đổi. Hệ thống sẽ tự dộng tạo ra file sitemap.xml cho website của bạn.