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
f = open(file_name, access_mode, buffering)
{% endhighlight %}

Trong đó:

* `access_mode  ` : chế độ để mở file. Có một số chế độ sau:
    * `r  ` : chỉ đọc nội dung (mặc định)
    * `r+  ` : đọc và ghi
    * `rb  ` : đọc file ở chế độ nhị phân
    * `rb+  ` : đọc và ghi file ở chế độ nhị phân
    * `w  ` : tạo file mới để ghi (nếu file đã tồn tại thì bị ghi đè nội dung)
    * `w+  ` : tạo file mới để đọc và ghi (nếu file đã tồn tại thì bị ghi đè nội dung)
    * `wb  ` : tạo file mới để ghi ở chế độ nhị phần (nếu file đã tồn tại sẽ bị ghi đè nôi dung)
    * `wb+  ` : tọa file mới để đọc và ghi ở chế độ nhị phân (nếu file đã tồn tại sẽ bị ghi đè)
    * `a  ` : append - mở file và ghi thêm vào cuối file, nếu file chưa tồn tại thì tạo file mới
    * `a+  `: mở file để đọc và ghi thêm vào cuối file nội dung mới, nếu file chưa tồn tại thì tạo file mới
    * `ab  ` : mở file ở dạng nhị phân và ghi nội dung mới vào cuối file
    * `ab+  `: mở file ở dạng nhị phân để đọc và ghi file, nội dung sẽ được ghi thêm vào cuối file
* `buffering  ` : Nếu buffer = 0, nghĩa là sẽ không có trình đệm nào diễn ra, Nếu = 1, thì trình đệm dòng được thực hiện trong khi truy cập một File. Nếu > 1 thì hoạt động đệm được thực hiện với kích cỡ bộ đệm đã cho. Nếu < 0: bộ đệm mặc định

Ví dụ:

{% highlight python %}
f = open('hello.txt', 'r')
for line in f: # lấy dữ liệu theo từng dòng trong file
    print(line) # in từng dòng dữ liệu ra màn hình
{% endhighlight %}

Sau khi gọi hàm open() thành công thì sẽ trả về một object có các thuộc tính sau:

* `closed  ` : trả về `True` nếu đã đóng, `False` nếu chưa đóng
* `mode  ` : trả về chế độ khi mở file
* `name  ` : trả về tên của file

### 1.2 Đọc nội dung file:

Sau khi mở file thì chúng ta sẽ dùng các phương thức sau để đọc nội dung trong file

{% highlight python %}
f = open('data.txt', 'r')
data = f.read() # đọc toàn bộ nội dung trong file
data = f.read(1024) # đọc 1024 byte nội dung trong file
line = f.readline() # đọc dữ liệu theo từng dòng trên file
f.close() # đóng file sau khi đọc nội dung trong file xong
{% endhighlight %}

### 1.3 Ghi nội dung vào file:

Nếu file được mở ở chế độ ghi thì ta có thể dùng phương thức ```write() ``` để ghi nội dung vào file. ví dụ:

{% highlight python %}
f = open('data/write.txt', 'w') # mở file tên write.txt trong thư mục data
f.write('Tuan') # ghi nội dung vào file
f.write('\n') # xuống dòng
f.write('Tony') # ghi tiếp nội dung
f.close() # đóng file sau khi đã làm việc xong
{% endhighlight %}

### 1.4 Đọc nội dung từ 1 file và ghi vào một file khác

Dưới đây là cách thức chúng ta đọc nội dung trong 1 file và ghi vào một file khác:

{% highlight python %}
rFile = open('read.txt', 'r') # mở file cần đọc dữ liệu read.txt
wFile = open('write.txt', 'w') # mở file cần ghi dữ liệu write.txt
for line in rFile: # lấy dữ liệu trong rFile theo từng dòng
    print(line, file=wFile, end='') # phương thức ghi nội dung vào wFile, ghi xong xuống hàng
print("Done") # thông báo đã ghi xong
{% endhighlight %}

### 1.5 Buffering - làm việc với file có dung lượng lớn

Khi đọc hay ghi những file có dung lượng lớn trong một lần thì có thể gây lỗi. Chúng ta dùng `buffer ` chia nhỏ dữ liệu để đọc và ghi trong nhiều lần  

{% highlight python %}
rFile = open('read.txt', 'r') # mở file nguồn
wFile = open('write.txt', 'w') # mở file đích

bufferSize = 25000 # set kích thước của buffer
data = rFile.read(bufferSize) # lấy dữ liệu có kích thước bằng bufferSize

i = 0
while len(data): # vòng lặp while kết thúc khi len(data) = 0, hết dữ liệu để đọc
    i += 1 # mỗi lần chạy tăng i lên 1
    wFile.write(data) # ghi data vừa lấy lên vào wFile
    print(i, "đã ghi {} bytes vào rFile".format(data)) # in ra màn hình quá trình đọc ghi để theo dõi
    data = rFile.read(bufferSize) # đọc tiếp bufferSize byte dữ liệu tiếp theo
print("Done") # thông báo đã ghi xong
{% endhighlight %}

### 1.6 Lấy vị trí dữ liệu trong file

Chúng ta sẽ sử dụng phương thức `tell() ` để lấy vị trí hiện tại của con trỏ đang ở trong file và sử dụng phương thức `seek(index) ` để tìm đến vị trí mong muốn. Trong đó `-index-` là vị trí muốn tìm đến

{% highlight python %}
fp = open('data.txt', 'r') # mở file

fpos = fp.tell() # lấy vị trí đang load dữ liệu trong file
print("Đọc tới vị trí :", fpos)
line = fp.readline() # lấy dữ liệu theo từng dòng
print(line, end='') # in dữ liệu lấy được ra màn hình, xuống dòng
fpos = fp.tell() # lấy vị trí hiện tại
print("Đang đọc tới vị trí: ", fpos) # in vị trí hiện tại ra màn hình

fp.seek(73) # tìm đến vị trí dữ liệu thứ 73
data = fp.read() # đọc toàn bộ dữ liệu từ vị trí thứ 73 cho đến cuối file

{% endhighlight %}

### 1.7 Đóng file

Sau khi làm việc xong với file thì chúng ta phải thực hiện đóng file bằng phương thức `close() `
ví dụ:

{% highlight python %}
fp.close()
{% endhighlight %}

### 1.8 Đổi tên file

Sử dụng phương thức `os.rename(ten_cu, ten_moi) ` để đổi tên file. Ví dụ sau sẽ đổi tên file từ abc thành def

{% highlight python %}
import os
os.rename('abc.txt', 'def.txt')
{% endhighlight %}

### 1.9 Xóa file:

Sử dụng phương thức `os.remove(file) ` để xóa 1 file ra khỏi hệ thống

{% highlight python %}
import os
os.remove('def.txt')
{% endhighlight %}

### 1.10 Lấy đường dẫn đầy đủ của file

sử dụng phương thức `os.getcwd() ` để lấy đường dẫn của file

{% highlight python %}
import os
file_path = os.getcwd() + abc.txt
{% endhighlight %}

## 2 Thư mục (Directory)

### 2.1 Tạo thư mục:

Sử dụng phương thức `os.mkdir(dir_name) ` để tạo thư mục

{% highlight python %}
import os
os.mkdir('project') # tạo thư mục project
{% endhighlight %}

### 2.2 Xóa thư mục:

Sử dụng phương thức `os.rmdir(dir_name) ` để xóa thư mục

{% highlight python %}
import os
os.rmdir('project') # xóa thư mục project
{% endhighlight %}

### 2.3 Lấy danh sách tập tin / thư mục:
Sử dụng phương thức `os.listdir(dir_name) ` để lấy danh sách các tập tin, thư mục bên trong thư mục dir_name. Kết quả sẽ trả về một mảng danh sách các tập tin, thư mục.

{% highlight python %}
import os
files = os.listdir('/root/downloads') # lấy danh sách tập tin bên trong thư mục downloads
print(files) # in danh sách files
{% endhighlight %}

### 2.4 Module `os `

