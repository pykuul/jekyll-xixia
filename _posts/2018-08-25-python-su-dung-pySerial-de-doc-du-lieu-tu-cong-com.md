---
layout: post
title:  "Python: Sử dụng pySerial để đọc dữ liệu từ cổng COM máy tính"
categories: Python
tags: Python pySerial
author: Richard Nguyen
description: python - doc du lieu tu cong com serial su dung pySerial.
---

Bài viết này mình sẽ hướng dẫn các bạn cách sử dụng package pySerial để đọc dữ liệu từ cổng COM của máy tính chạy hệ điều hành window. Cụ thể mình đọc số ID in trên thẻ proximity 125khz dùng đầu đọc thẻ RFID sử dụng cổng COM của hãng ITECH

Đầu tiên các bạn cần phải cài đặt gói package pySerial bằng lệnh sau đây:
* Window:  
`pip install pySerial`

* Linux:  
`sudo apt install pySerial` 

Để sử dụng thư viện pySerial các bạn phải import nó:
{% highlight python %}
    import serial
{% endhighlight %}

sau đó các bạn khởi tạo đối tượng Serial
{% highlight python %}
    ser = serial.Serial()
    # cài đặt thông số cho cổng COM
    ser.port = "COM3" # window
    # ser.port = '/dev/ttyUSB0' # Linux
    ser.baudrate = 9600
    ser.bytesize = 8
    ser.parity = 'N'
    ser.stopbits = 1
    ser.timeout = None
    ser.xonxoff = 0
    ser.rtscts = 0
    # Khởi tạo kết nối tới cổng COM
    ser.open() 
{% endhighlight %}

Có nhiều phương thức để đọc dữ liệu:
{% highlight python %}
    data = ser.read() # đọc 1 byte
    data = ser.read(10) # đọc 10 bytes
    line = ser.readline() # đọc nguyên dòng
    line = ser.read(ser.inWaiting()) # đọc dữ liệu từ bộ nhớ buffer ngõ vào
{% endhighlight %}

Các bạn cũng có thể thực hiện lệnh send dữ liệu ra cổng COM bằng lệnh write:
{% highlight python %}
    ser.write(b'hello') # b'hello' dùng để chuyển chuỗi hello sang bytes
{% endhighlight %}

sau khi các bạn ghi hoặc đọc dữ liệu xong các bạn nên đóng cổng COM lại
{% highlight python %}
    ser.close()
{% endhighlight %}   

### Full code
{% highlight python %}
    import serial
    import time

    ser = serial.Serial() # khởi tạo đối tượng Serial
    # đóng cổng COM trước để đảm bảo không bị Window khóa truy cập tới cổng COM 
    ser.close()
    # cài đặt thông số cho cổng COM: 
    ser.port = "COM3" # thiết bị đang kết nối vào COM3
    ser.baudrate = 9600

    try:
        ser.open() # khởi tạo kết nối tới COM 3
        ser.flushInput() # làm sạch buffer ngõ vào của cổng COM
        time.sleep(1) # Chờ 1 giây

        # đọc toàn bộ dữ liệu từ bộ nhớ buffer
        data_raw = ser.read(ser.inWaiting()) 
        # dữ liệu đọc được sẽ có dạng như sau: b'\x0207054805\x03\x06'
        # trong đó \x02 là SOL(Start of line), \x03 là EOL (End of line)
        # dữ liệu cần lấy là phần ở giữa SOL và EOL: 07054805 (8 ký tự)

        # tách dữ liệu cần lấy
        if len(data_raw) > 9: # kiểm tra xem có đọc đủ dữ liệu cần thiết chưa
            print("Card_id: {}".format(str(data_raw[1:9].decode('utf-8'))))
        else:
            print("Chưa đọc được dữ liệu")
        ser.close() # đóng cổng COM
    except serial.SerialException as error:
        print(error)
{% endhighlight %}   

**Tài liệu tham khảo:** [https://pythonhosted.org/pyserial/](https://pythonhosted.org/pyserial/)
