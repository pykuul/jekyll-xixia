---
layout: post
title:  "Học lập trình Python: Sử dụng pySerial để đọc dữ liệu từ cổng COM máy tính"
categories: Python
tags: Python pySerial
author: Richard Nguyen
description: Script to read serial data from COM port using pySerial.
---

Bài viết này mình sẽ hướng dẫn các bạn cách sử dụng package PySerial để đọc dữ liệu từ cổng COM của máy tính chạy hệ điều hành window. Cụ thể mình đọc số ID in trên thẻ proximity 125khz dùng đầu đọc thẻ RFID sử dụng cổng COM của hãng ITECH

Trước hết các bạn cần cài đặt gói package pySerial bằng lệnh sau đây:
* Window:  
`pip install pySerial`

* Linux:  
`sudo apt install pySerial` 

Để sử dụng thư viện pySerial các bạn phải import nó:  
    import serial
 
sau đó các bạn khởi tạo đối tượng Serial
{% highlight python %}
    ser = serial.Serial()
    ser.port = COM3 # các bạn phải kiểm tra xem đầu đọc thẻ đang kết nối tới cổng COM nào
    ser.baudrate = 9600
    # ser.bytesize = 8
    # ser.parity = 'N'
    # ser.stopbits = 1
    # ser.timeout = None
    # ser.xonxoff = 0
    # ser.rtscts = 0
{% endhighlight %}



### Full code
{% highlight python %}
    import serial
    import time

    ser = serial.Serial() # khởi tạo đối tượng Serial
    ser.close() # close COM trước để đảm bảo không bị Window khóa truy cập tới cổng COM 
    ser.port = "COM3" # card reader kết nối vào COM 3
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