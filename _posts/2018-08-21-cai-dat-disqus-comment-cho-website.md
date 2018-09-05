---
layout: post
title:  "Tạo Blog với Github và Jekyll: Thêm công cụ comment của Disqus vào blog"
categories: Github
tags: Github Blog GitBlog GitPages sitemap sitemap.xml
author: Richard Nguyen
description: them cong cu comment disqus cho website hay blog tao boi Jekyll va github.
---

Bài viết này tôi sẽ hướng dẫn các bạn cách thêm công cụ comment của disqus vào blog được tạo bởi Jekyll

* Đầu tiên các bạn tạo tài khoản Disqus tại đây: [https://disqus.com/](https://disqus.com/) 
* Sau đó các bạn tạo ra một Disqus shortname cho website Jekyll. Các tham khảo theo hướng dẫn sau: [https://help.disqus.com/installation/whats-a-shortname](https://help.disqus.com/installation/whats-a-shortname) 
* Bước tiếp theo là các bạn cấu hình các thông số cho website Jekyll. Thực hiện các bước như sau:

1. Mở file `_config.yml ` sau đó add thêm đoạn code bên dưới vào cuối file:

```ruby
# Add Disqus comments
disqus:
	shortname: my_disqus_shortname # my_disqus_shortname là cái shortname các bạn đã lấy được bước 2
```
2. Tạo một file tên là `disqus_comments.html` trong thư mục `_includes ` trên website của bạn. Sau đó thêm đoạn code bên dưới vào file và lưu file lại.

```java
{% raw %}
{% if page.comments != false and jekyll.environment == "production" %}

  <div id="disqus_thread"></div>
  <script>
    var disqus_config = function () {
      this.page.url = '{{ page.url | absolute_url }}';
      this.page.identifier = '{{ page.url | absolute_url }}';
    };
    (function() {
      var d = document, s = d.createElement('script');
      s.src = 'https://{{ site.disqus.shortname }}.disqus.com/embed.js';
      s.setAttribute('data-timestamp', +new Date());
      (d.head || d.body).appendChild(s);
    })();
  </script>
  <noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript" rel="nofollow">comments powered by Disqus.</a></noscript>
{% endif %}
{% endraw %}
```

3. Mở file `post.html` trong thư mục `_layouts`. thêm vào phần đầu post (YAML front-matter) `comments: true` như sau:

```ruby
---
layout: post
comments: true # gán false nếu bạn muốn disable Disqus
---
```

Đồng thời thêm đoạn code sau vào trước thẻ `</article>`:

```ruby
{% if site.disqus.shortname %}
  {% include disqus-comments.html %}
{% endif %}
```

các bạn lưu file post.html. Commit toàn bộ các thay đổi vừa rồi cho website của bạn.  


**Nguồn tham khảo:** [https://desiredpersona.com/disqus-comments-jekyll/](https://desiredpersona.com/disqus-comments-jekyll/)