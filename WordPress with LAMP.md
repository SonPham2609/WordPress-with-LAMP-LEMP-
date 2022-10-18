# LAMP là gì
 LAMP là chữ viết tắt thường được dùng để chỉ sự sử dụng các phần mềm Linux, Apache, MySQL và ngôn ngữ văn lệnh PHP hay Perl hay Python để tạo nên một môi trường máy chủ Web có khả năng chứa và phân phối các trang Web động. Bốn phần mềm nói trên tạo thành một gói phần mềm LAMP.
 # WordPress với LAMP
 * Yêu cầu:

   * Với mục đích của hướng dẫn này, chúng tôi sẽ sử dụng VPS Ubuntu. Lưu trữ VPS Ubuntu của chúng tôi đã được cài đặt sẵn với một ngăn xếp LAMP hoạt động đầy đủ. Tuy nhiên, chúng tôi vẫn sẽ đi qua tất cả các bước cần thiết và hướng dẫn bạn cách tự cài đặt và định cấu hình ngăn xếp LAMP, trong trường hợp bạn đang thực hiện việc này trên một máy chủ sạch.

    * Cũng cần có quyền root SSH đầy đủ hoặc người dùng có đặc quyền sudo. Tất cả các VPS của chúng tôi đều có quyền truy cập root đầy đủ mà không phải trả thêm phí.

    * Tên miền hợp lệ để truy cập trang web WordPress (172.16.222.130)
## Kết nối với máy chủ của bạn và cập nhật hệ thống của bạn
* Trước khi bắt đầu, hãy kết nối với VPS của bạn qua SSH với tư cách là người dùng gốc (hoặc bằng tài khoản quản trị viên) và cập nhật phần mềm hệ thống của bạn lên phiên bản mới nhất hiện có.

* Để kết nối với máy chủ của bạn qua SSH với tư cách là người dùng gốc, hãy sử dụng lệnh sau:
```ssh root@IP_ADDRESS ```
* Mình sẽ dùng `root` với tên `ptson` với địa chỉ `IP_ADDRESS` là `172.16.222.130`
![image](https://user-images.githubusercontent.com/91528234/196365577-8f1470b8-ce85-4e0b-a39a-2e1ed35602a8.png)

* Sau khi đăng nhập, hãy đảm bảo rằng máy chủ của bạn được cập nhật bằng cách chạy các lệnh sau với quyền root:
``` 
# apt update
# apt upgrade 
```
## Cài đặt LAMP
1. Cài đặt Máy chủ Web Apache

* Apache là một máy chủ web nhanh và an toàn và là một trong những máy chủ web phổ biến và được sử dụng rộng rãi nhất trên thế giới. Tính dễ sử dụng của nó làm cho nó rất hấp dẫn khi bắt đầu với máy chủ web và lưu trữ máy chủ web.

* Để cài đặt máy chủ web Apache, hãy chạy lệnh sau:
```
# apt install apache2
```
* Khi quá trình cài đặt hoàn tất, hãy kích hoạt dịch vụ Apache để tự động khởi động khi khởi động hệ thống. Bạn có thể làm điều đó bằng lệnh sau:
```
# systemctl enable apache2
```
* Để xác minh rằng Apache đang chạy, hãy thực hiện lệnh sau:
```
# systemctl status apache2
```
![image](https://user-images.githubusercontent.com/91528234/196366489-10b00c41-46b9-4b76-89e7-0324ef941903.png)
* Bạn cũng có thể mở trình duyệt web và nhập địa chỉ IP máy chủ của mình và thu được page mặc địch của apache như sau:
![image](https://user-images.githubusercontent.com/91528234/196366835-b582859b-8687-41bd-81d3-a7e5a3c60fbb.png)
## Cài đặt MySQL 
* Bước tiếp theo là cài đặt máy chủ cơ sở dữ liệu MySQL sẽ được sử dụng để lưu trữ dữ liệu trên trang WordPress của bạn.

* Để cài đặt máy chủ cơ sở dữ liệu MySQL, hãy nhập lệnh sau:
```
# apt install mysql-server
```
* Trong quá trình cài đặt, bạn sẽ được yêu cầu nhập mật khẩu cho người dùng gốc MySQL. Đảm bảo nhập mật khẩu mạnh.

* Để cải thiện hơn nữa tính bảo mật của cài đặt MySQL của chúng tôi, cũng như thiết lập mật khẩu cho người dùng gốc MySQL của chúng tôi, chúng tôi cần chạy tập lệnh mysql_secure_installation và làm theo hướng dẫn trên màn hình. Chạy lệnh dưới đây để định cấu hình hệ thống của bạn:
```
# mysql_secure_installation
```
* Nếu chương trình yêu cầu bạn nhập mật khẩu gốc MySQL hiện tại, chỉ cần nhấn phím [Enter] một lần, vì không có mật khẩu nào được đặt theo mặc định khi cài đặt MySQL.

* Một số câu hỏi khác sẽ được hiển thị trên màn hình - bạn nên trả lời CÓ cho tất cả chúng bằng cách nhập ký tự ‘Y’:
![image](https://user-images.githubusercontent.com/91528234/196368110-2d06b199-d453-4b61-9f12-eb2277cda27f.png)
* Bạn cũng sẽ cần kích hoạt MySQL để bắt đầu khởi động với điều này:
```
# systemctl enable mysql
```
## Cài đặt PHP
* Bước cuối cùng của quá trình thiết lập ngăn xếp LAMP của chúng tôi là cài đặt PHP. WordPress là một CMS dựa trên PHP, vì vậy chúng tôi cần PHP để xử lý nội dung động của trang WordPress của chúng tôi.

* Ubuntu 20.04 đi kèm với PHP 7.4 theo mặc định. Chúng tôi cũng sẽ cần một số mô-đun bổ sung để cho phép PHP kết nối và giao tiếp với các phiên bản Apache và MySQL của chúng tôi. Để cài đặt PHP cùng với các mô-đun MySQL và Apache được yêu cầu, hãy chạy lệnh sau:
```
# apt install php libapache2-mod-php php-mysql
```
* Để xác minh rằng PHP 7.4 đã được cài đặt thành công, hãy chạy lệnh sau:
```
php -v
```
* Bạn sẽ nhận được kết quả sau trên màn hình của mình:
![image](https://user-images.githubusercontent.com/91528234/196369617-4aeb2061-479e-45b4-ad67-f2744bb57e58.png)
## Cài đặt WordPress

* Bây giờ chúng ta đã thiết lập xong môi trường LAMP, bây giờ chúng ta có thể tiến hành cài đặt WordPress. Trước tiên, chúng tôi sẽ tải xuống và đặt các tệp cài đặt WordPress trong thư mục gốc của tài liệu máy chủ web mặc định, / var / www / html.

* Bạn có thể di chuyển đến thư mục này bằng lệnh sau:
```
cd /var/www/html
```
* Bây giờ chúng ta có thể tải xuống bản cài đặt WordPress mới nhất bằng lệnh sau:

```
# wget -c http://wordpress.org/latest.tar.gz
```
* Sau đó, giải nén các tệp bằng:
```
#tar -xzvf mới nhất.tar.gz
```
* Các tệp WordPress được giải nén bây giờ sẽ được đặt trong thư mục wordpress tại vị trí sau trên máy chủ của bạn / var / www / html / wordpress

