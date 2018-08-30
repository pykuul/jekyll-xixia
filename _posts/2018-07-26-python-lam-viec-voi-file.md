---
layout: post
title:  "Python: Làm việc với file và thư mục"
categories: Python
tags: Python
author: Richard Nguyen
description: python - làm việc với file và thư mục trong python.
---

Nội dung bài này sẽ hướng dẫn các thao tác cơ bản liên quan đến tâp tin và thư mục

## 1. Tập tin (File):

### 1.1 Mở file: 

Trước khi làm việc với bất cứ file nào thì các bạn cần phải mở file

\- **Cú pháp:**  
{% highlight python %}
file = open(file_name, access_mode, buffer)
{% endhighlight %}

Trong đó:

* ```access_mode ``` : chế độ để mở file. Có một số chế độ sau:
    * ```r ``` : chỉ đọc nội dung (mặc định)
    * `r+` : đọc và ghi
    * `rb` : đọc file ở chế độ nhị phân
    * `rb+` : đọc và ghi file ở chế độ nhị phân
    * `w` : tạo file mới để ghi (nếu file đã tồn tại thì bị ghi đè nội dung)
    * `w+` : tạo file mới để đọc và ghi (nếu file đã tồn tại thì bị ghi đè nội dung)
    * `wb` : tạo file mới để ghi ở chế độ nhị phần (nếu file đã tồn tại sẽ bị ghi đè nôi dung)
    * `wb+` : tọa file mới để đọc và ghi ở chế độ nhị phân (nếu file đã tồn tại sẽ bị ghi đè)
    * `a` : append - mở file và ghi thêm vào cuối file, nếu file chưa tồn tại thì tạo file mới
    * `a+`: mở file để đọc và ghi thêm vào cuối file nội dung mới, nếu file chưa tồn tại thì tạo file mới
    * `ab` : mở file ở dạng nhị phân và ghi nội dung mới vào cuối file
    * `ab+`: mở file ở dạng nhị phân để đọc và ghi file, nội dung sẽ được ghi thêm vào cuối file
* ```buffer``` : Nếu buffer = 0, nghĩa là sẽ không có trình đệm nào diễn ra, Nếu = 1, thì trình đệm dòng được thực hiện trong khi truy cập một File. Nếu > 1 thì hoạt động đệm được thực hiện với kích cỡ bộ đệm đã cho. Nếu < 0: bộ đệm mặc định

Ví dụ:

{% highlight python %}
file = open('hello.txt', 'r')
{% endhighlight %}

Sau khi gọi hàm open() thành công thì sẽ trả về một object có các thuộc tính sau:

* ```closed ``` : trả về `True` nếu đã đóng, `False` nếu chưa đóng
* ```mode ``` : trả về chế độ khi mở file
* ```name ``` : trả về tên của file

### 1.2 Đọc nội dung file:

Sau khi mở file thì chúng ta sẽ dùng các phương thức sau để đọc nội dung trong file

{% highlight python %}
file = open('data.txt', 'r')
data = file.read() # đọc toàn bộ nội dung trong file
data = file.read(1024) # đọc 1024 byte nội dung trong file
line = file.readline() # đọc dữ liệu theo từng dòng trên file
{% endhighlight %}

### 1.3 Ghi nội dung vào file:

Nếu file được mở ở chế độ ghi thì ta có thể dùng phương thức ```write() ``` để ghi nội dung vào file. ví dụ:

{% highlight python %}
file = open('log.txt', 'a+')
file.write('added new user')
{% endhighlight %}