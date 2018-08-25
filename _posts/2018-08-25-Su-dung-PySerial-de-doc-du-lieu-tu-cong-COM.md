---
layout: post
title:  "Sử dung PySerial để đọc dữ liệu từ cổng COM máy tính"
categories: Python
tags: Python PySerial
author: Richard Nguyen
description: Script to read data from COM port using PySerial.
---

Bài viết này mình sẽ hướng dẫn các bạn cách sử dụng package PySerial để đọc dữ liệu từ cổng COM của máy tính chạy hệ điều hành window. Cụ thể mình đọc card-ID sử dụng đầu đọc thẻ RFID sử dụng cổng COM của hãng ITECH

### Full code
{% highlight python %}
    import serial
    import time

    ser = serial.Serial() # khởi tạo đối tượng Serial
    ser.close() # close COM trước để đảm bảo không bị Window khóa truy cập tới cổng COM 
    ser.port = "COM 3" # card reader kết nối vào COM 3
    ser.baudrate = 9600

    try:
        ser.open() # khởi tạo kết nối tới COM 3
        ser.flushInput() # làm sạch buffer ngõ vào của cổng COM
        time.sleep(1) # Chờ 1 giây
        data_raw = ser.read(ser.inWaiting()) # đọc toàn bộ dữ liệu từ buffer
        if len(data_raw) > 9: # kiểm tra xem có đọc đủ dữ liệu cần thiết không
            print("Card_id: {}".format(str(data_raw[1:9].decode('utf-8'))))
        else:
            print("Chưa đọc được dữ liệu")
    except serial.SerialException as error:
        print(error)
{% endhighlight %}