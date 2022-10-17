# LEMP là gì
LEMP server là một server chạy Linux, Nginx (đọc là Engine x), MySql và PHP (hoặc Perl/Python). Nó tương tự như LAMP server ngoại trừ việc web server nền tảng được giám sát bằng Nginx thay vì Apache.
# Cài đặt WordPress với LEMP
## Điều kiện 

* VPS Ubuntu 20.04 

* Quyền truy cập vào tài khoản người dùng root (hoặc quyền truy cập vào tài khoản quản trị viên có đặc quyền root)
## Đăng nhập vào máy chủ và cập nhật gói Hệ điều hành máy chủ
* Đầu tiên, đăng nhập vào máy chủ Ubuntu 20.04 của bạn thông qua SSH với tư cách là người dùng gốc:
```
ssh root@IP_Address 
```
* người dùng gốc mình dùng `ptson` và `IP_Address` là `172.16.222.129`
![image](https://user-images.githubusercontent.com/91528234/196124967-0ff2a1bc-85b9-4c9a-a752-61f6878a5acb.png)

* Trước khi bắt đầu, bạn phải đảm bảo rằng tất cả các gói hệ điều hành Ubuntu được cài đặt trên máy chủ đều được cập nhật. Bạn có thể thực hiện việc này bằng cách chạy các lệnh sau:
```
apt update 
apt upgrade
```
## Cài LEMP Server
### Cài Nginx 
```
# apt install nginx
```
* Để kiểm tra tường lửa cấu hình UFW nào khả dụng, hãy chạy:
```
# ufw app list
```
![image](https://user-images.githubusercontent.com/91528234/196124811-81d07573-12aa-4ab0-9171-96556e80f33c.png)
* Bạn nên bật cấu hình hạn chế nhất vẫn cho phép lưu lượng truy cập mà bạn cần. Vì bạn chưa định cấu hình SSL cho máy chủ của mình trong hướng dẫn này, bạn sẽ chỉ cần cho phép lưu lượng HTTP thông thường trên cổng 80.
* Kích hoạt tính năng này bằng cách nhập:
```
# ufw allow 'Nginx HTTP'
```
![image](https://user-images.githubusercontent.com/91528234/196125686-d2c7d722-a983-4f10-b844-59113954ffd9.png)
* Bạn có thể xác minh sự thay đổi bằng cách chạy:
```
# ufw status
```
![image](https://user-images.githubusercontent.com/91528234/196126124-45d2af64-63f8-4b1b-96f4-a905c8f36475.png)
* Với quy tắc tường lửa mới được thêm vào, bạn có thể kiểm tra xem máy chủ có hoạt động hay không bằng cách truy cập vào tên miền hoặc địa chỉ IP công cộng của máy chủ trong trình duyệt web của bạn.
* Nhập địa chỉ mà bạn nhận được vào trình duyệt web của mình và địa chỉ đó sẽ đưa bạn đến trang đích mặc định của Nginx:
```
http://server_domain_or_IP
```
![image](https://user-images.githubusercontent.com/91528234/196126468-6f1785b7-4ff0-4d29-8b62-952eafd3e435.png)
### Cài đặt MySQL
* Bây giờ bạn đã có một máy chủ web và đang chạy, bạn cần cài đặt hệ thống cơ sở dữ liệu để có thể lưu trữ và quản lý dữ liệu cho trang web của mình. MySQL là một hệ quản trị cơ sở dữ liệu phổ biến được sử dụng trong môi trường PHP.

* Một lần nữa, hãy sử dụng apt để mua và cài đặt phần mềm này:
```
# apt install mysql-server
```
* Khi quá trình cài đặt hoàn tất, bạn nên chạy một tập lệnh bảo mật được cài đặt sẵn với MySQL. Tập lệnh này sẽ xóa một số cài đặt mặc định không an toàn và khóa quyền truy cập vào hệ thống cơ sở dữ liệu của bạn. Bắt đầu tập lệnh tương tác bằng cách chạy:
```
mysql_secure_installation
```
* cài đặt mặt khẩu và bấm Y cho đến khi như sau:
![image](https://user-images.githubusercontent.com/91528234/196129691-04043cef-e600-4fb6-a8a7-ded823cb5076.png)
### Cài đặt PHP
* Bạn đã cài đặt Nginx để phân phát nội dung của mình và đã cài đặt MySQL để lưu trữ và quản lý dữ liệu của bạn. Bây giờ bạn có thể cài đặt PHP để xử lý mã và tạo nội dung động cho máy chủ web.

* Trong khi Apache nhúng trình thông dịch PHP trong mỗi yêu cầu, Nginx yêu cầu một chương trình bên ngoài để xử lý quá trình xử lý PHP và hoạt động như một cầu nối giữa chính trình thông dịch PHP và máy chủ web. Điều này cho phép hiệu suất tổng thể tốt hơn trong hầu hết các trang web dựa trên PHP, nhưng nó yêu cầu cấu hình bổ sung. Bạn sẽ cần cài đặt php-fpm, viết tắt của “PHP fastCGI process manager” và yêu cầu Nginx chuyển các yêu cầu PHP đến phần mềm này để xử lý. Ngoài ra, bạn sẽ cần php-mysqlmột mô-đun PHP cho phép PHP giao tiếp với cơ sở dữ liệu dựa trên MySQL. Các gói PHP cốt lõi sẽ tự động được cài đặt dưới dạng các gói phụ thuộc.

* Để cài đặt php-fpm và php-mysql các gói, hãy chạy:
```
apt install php-fpm php-mysql
```
Trên Ubuntu 20.04, Nginx có một khối máy chủ được bật theo mặc định và được định cấu hình để cung cấp tài liệu ra khỏi một thư mục tại /var/www/html. Mặc dù điều này hoạt động tốt cho một trang web nhưng có thể trở nên khó quản lý nếu bạn đang lưu trữ nhiều trang web. Thay vì sửa đổi /var/www/html, chúng tôi sẽ tạo cấu trúc thư mục bên trong /var/www cho trang web your_domain , giữ nguyên /var/www/html vị trí này làm thư mục mặc định được phục vụ nếu yêu cầu của khách hàng không khớp với bất kỳ trang web nào khác.


