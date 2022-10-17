# LAMP là gì
 LAMP là chữ viết tắt thường được dùng để chỉ sự sử dụng các phần mềm Linux, Apache, MySQL và ngôn ngữ văn lệnh PHP hay Perl hay Python để tạo nên một môi trường máy chủ Web có khả năng chứa và phân phối các trang Web động. Bốn phần mềm nói trên tạo thành một gói phần mềm LAMP.
 # WordPress với LAMP
 Yêu cầu:

Với mục đích của hướng dẫn này, chúng tôi sẽ sử dụng VPS Ubuntu. Lưu trữ VPS Ubuntu của chúng tôi đã được cài đặt sẵn với một ngăn xếp LAMP hoạt động đầy đủ. Tuy nhiên, chúng tôi vẫn sẽ đi qua tất cả các bước cần thiết và hướng dẫn bạn cách tự cài đặt và định cấu hình ngăn xếp LAMP, trong trường hợp bạn đang thực hiện việc này trên một máy chủ sạch.

Cũng cần có quyền root SSH đầy đủ hoặc người dùng có đặc quyền sudo. Tất cả các VPS của chúng tôi đều có quyền truy cập root đầy đủ mà không phải trả thêm phí.

Tên miền hợp lệ để truy cập trang web WordPress (172.16.222.129)
## Kết nối với máy chủ của bạn và cập nhật hệ thống của bạn
* Trước khi bắt đầu, hãy kết nối với VPS của bạn qua SSH với tư cách là người dùng gốc (hoặc bằng tài khoản quản trị viên) và cập nhật phần mềm hệ thống của bạn lên phiên bản mới nhất hiện có.

* Để kết nối với máy chủ của bạn qua SSH với tư cách là người dùng gốc, hãy sử dụng lệnh sau:
```ssh root@IP_ADDRESS ```
* Mình sẽ dùng `root` với tên `ptson` với địa chỉ `IP_ADDRESS` là `172.16.222.129`e
![image](https://user-images.githubusercontent.com/91528234/196119251-a70b839e-9a4a-45bb-b95a-a433e4a37a12.png)
* Sau khi đăng nhập, hãy đảm bảo rằng máy chủ của bạn được cập nhật bằng cách chạy các lệnh sau:
``` 
sudo apt update
sudo apt upgrade 
```
## Cài đặt LAMP
1. Cài đặt Máy chủ Web Apache

Apache là một máy chủ web nhanh và an toàn và là một trong những máy chủ web phổ biến và được sử dụng rộng rãi nhất trên thế giới. Tính dễ sử dụng của nó làm cho nó rất hấp dẫn khi bắt đầu với máy chủ web và lưu trữ máy chủ web.

Để cài đặt máy chủ web Apache, hãy chạy lệnh sau:
