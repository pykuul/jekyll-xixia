---
layout: post
title:  "Tạo Blog với Github: Tạo Sitemap tự động cho website sử dụng Jekyll"
categories: Github
tags: Github Blog GitBlog GitPages sitemap sitemap.xml
author: Richard Nguyen
description: automatically create sitemap.xml for wibsite or blog created by github page and Jekyll.
---
sitemap.xml là gì?
==================

sitemap được xem như tấm bản đồ của wibsite. Nó là một tập tin văn bản có chứa toàn bộ các url trên trang web của bạn. Toàn bộ công việc của Sitemap là hướng dẫn cho các bộ máy tìm kiếm thu thập thông tin của trang web hiệu quả đồng thời cập nhật các thay đổi trên trang web của bạn

Do vậy việc có một Sitemap và submit lên các công cụ tìm kiếm như Google, sẽ giúp các công cụ tìm kiếm index trang web nhanh hơn. Bài viết này mình hướng dẫn các bạn tạo ra sitemap tự động cho các website hay blog được tạo từ Jekyll và Github pages

Mở file `_config.yml` tại thư mục gốc chứa website trên repository, thêm vào các dòng lệnh sau:
{% highlight ruby %}
gems: 
  - jekyll-sitemap
{% endhighlight %}

Các bạn commit để lưu các thay đổi. Hệ thống sẽ tự động tạo ra file sitemap.xml cho website của bạn.

kiểm tra sitemap: pykuul.github.com/sitemap.xml

![sitemap]({{ site.baseurl }}/assets/images/site-map.png)