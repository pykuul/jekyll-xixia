---
layout: post
title:  "Cách gõ code html và bootstrap nhanh"
categories: html
tags: html bootstrap
author: Richard Nguyen
description: cách gõ code html và bootstrap nhanh.
---

### Bài viết này tôi giới thiệu các bạn một cách để viết code html và bootstrap nhanh bằng SublineText

* Để gõ code html nhanh thì ta cài đặt gói Emmet vào sublineText
* Để gõ Bootstrap nhanh thì cài đặt gói package: Bootstrap 3 Snippets vào Sublinetext

### 1. gõ code html và css nhanh:

* khởi tạo tài liệu html 5: `html:5 ` --> nhấn tab

* **html elements**: nhập tên bất kỳ và nhấn tab sẽ tự động tạo html tag. Ví dụ: `div --> <div></div> ` nhập `foo --> <foo></foo> `

* **Child**: sử dụng dấu `> ` để tạo các element con (viết liền không khoảng trắng)> ví dụ: `div>ul>li ` sẽ tạo ra đoạn code html như sau:  
{% highlight html %}
<div>
	<ul>
		<li></li>
	</ul>
</div>
{% endhighlight %}

* **Sibling**: sử dụng dấu `+ ` để tạo các element ngang hàng. ví dụ: `div+p+bq ` sẽ tạo ra đoạn code html sau:
{% highlight html %}
<div></div>
<p></p>
<blockquote></blockquote>
{% endhighlight %}

* **Multiple**: Sử dụng dấu `* ` để tảo ra nhiều element cùng lúc. ví dụ `ul>li*5 ` sẽ tạo ra đoạn code sau:
{% highlight html %}
<ul>
	<li></li>
	<li></li>
	<li></li>
	<li></li>
	<li></li>
</ul>
{% endhighlight %}

* **id và class**: sử dụng `. ` để tạo class và dấu `# ` để tạo id cho các element. ví dụ: `div#header+div.page+div#footer.class1.class2.class3 ` sẽ tự động tạo ra đoạn code html như sau:
{% highlight html %}
<div id="header"></div>
<div class="page"></div>
<div id="footer" class="class1 class2 class3"></div>
{% endhighlight %}

* **Item numbering**: sử dụng dấu `$ ` để tự động đánh số cho các item của element. ví dụ `ul>li.item$*5` sẽ tự động tạo ra đoạn code sau:
{% highlight html %}
<ul>
	<li class="item1"></li>
	<li class="item2"></li>
	<li class="item3"></li>
	<li class="item4"></li>
	<li class="item5"></li>
</ul>
{% endhighlight %}

* **Text**: sử dụng dấu `{text here} ` để thêm text cho element. Ví dụ đoạn code sau: `#page>div.logo+ul#navigation>li*5>a{item $}` sẽ tự động tạo ra đoạn code html sau
{% highlight html %}
<div id="page">
    <div class="logo"></div>
    <ul id="navigation">
    	<li><a href="">Item 1</a></li>
    	<li><a href="">Item 2</a></li>
    	<li><a href="">Item 3</a></li>
    	<li><a href="">Item 4</a></li>
    	li><a href="">Item 5</a></li>
    </ul>
</div>{% endhighlight %}

Hay đoạn code sau: `a>{Click}+b{here} ` sẽ tự động tạo ra đoạn code html như sau:
{% highlight html %}
<a href="">click<b>here</b></a>
{% endhighlight %}

**Tài liệu tham khảo cho cách gõ Emmet**:[https://docs.emmet.io/abbreviations/syntax/](https://docs.emmet.io/abbreviations/syntax/)

### 2. Cách gõ website bootstrap nhanh:

* khởi tạo tài liệu html 5: ` html:5 ` --> tab
* Sử dụng gói bootstrap cdn: ` bs3-cdn ` -->tab vào trong thẻ `<header> ` của tài liệu html
* tạo nav-bar : ` bs3-navbar ` --> ta  (gõ thêm ctr + space để xem thêm suggestion)
* tạo jumbotron quảng cáo: ` bs3-ju ` -->tab
* tạo class container: ` .container ` -->tab 
* bên trong container tạo 1 class row: ` .row ` -->tab
* bên trong row tạo 1 col chiều ngang 4 cột: ` .col-md-4 ` -->tab
* bên trong col này tạo 1 list danh sách: ` bs3-list-group ` --> tab
* tạo 1 col thứ 2 chiều ngang 8 cột: ` .col-md-8 ` --> tab
* trong col này tạo 1 panel-heading: ` bs3-panel-heading ` --> tab
* tạo footer: ` footer ` --> tab
* trong footer tạo đoạn text căn giữa: ` p.text-centre ` --> tab

