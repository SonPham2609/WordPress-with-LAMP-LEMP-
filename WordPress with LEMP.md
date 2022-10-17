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
# mysql_secure_installation
```
* cài đặt mặt khẩu và bấm Y cho đến khi như sau:
![image](https://user-images.githubusercontent.com/91528234/196129691-04043cef-e600-4fb6-a8a7-ded823cb5076.png)
* Chạy mysql với lệnh sau:
```
mysql -u root -p
```
* Để tạo cơ sở dữ liệu mới cho cài đặt WordPress của chúng tôi, hãy chạy các lệnh sau:
```
CREATE DATABASE wordpress_db;
CREATE USER wordpress_user@localhost IDENTIFIED BY '12345678';
GRANT ALL PRIVILEGES ON wordpress_db.* TO wordpress_user@localhost;
FLUSH PRIVILEGES;
exit;
```
![image](https://user-images.githubusercontent.com/91528234/196132041-91095dd7-7ad1-45f2-a411-89328d9c1295.png)


### Cài đặt PHP
* Bạn đã cài đặt Nginx để phân phát nội dung của mình và đã cài đặt MySQL để lưu trữ và quản lý dữ liệu của bạn. Bây giờ bạn có thể cài đặt PHP để xử lý mã và tạo nội dung động cho máy chủ web.

* Trong khi Apache nhúng trình thông dịch PHP trong mỗi yêu cầu, Nginx yêu cầu một chương trình bên ngoài để xử lý quá trình xử lý PHP và hoạt động như một cầu nối giữa chính trình thông dịch PHP và máy chủ web. Điều này cho phép hiệu suất tổng thể tốt hơn trong hầu hết các trang web dựa trên PHP, nhưng nó yêu cầu cấu hình bổ sung. Bạn sẽ cần cài đặt php-fpm, viết tắt của “PHP fastCGI process manager” và yêu cầu Nginx chuyển các yêu cầu PHP đến phần mềm này để xử lý. Ngoài ra, bạn sẽ cần php-mysqlmột mô-đun PHP cho phép PHP giao tiếp với cơ sở dữ liệu dựa trên MySQL. Các gói PHP cốt lõi sẽ tự động được cài đặt dưới dạng các gói phụ thuộc.

* Để cài đặt php-fpm và php-mysql các gói, hãy chạy:
```
# apt install php-fpm php-mysql
```
Trên Ubuntu 20.04, Nginx có một khối máy chủ được bật theo mặc định và được định cấu hình để cung cấp tài liệu ra khỏi một thư mục tại /var/www/html. Mặc dù điều này hoạt động tốt cho một trang web nhưng có thể trở nên khó quản lý nếu bạn đang lưu trữ nhiều trang web. Thay vì sửa đổi /var/www/html, chúng tôi sẽ tạo cấu trúc thư mục bên trong /var/www cho trang web your_domain , giữ nguyên /var/www/html vị trí này làm thư mục mặc định được phục vụ nếu yêu cầu của khách hàng không khớp với bất kỳ trang web nào khác.
### Cài đặt WordPress
* Đầu tiên, thay đổi thư mục thành thư mục gốc của web mặc định Nginx và tải xuống phiên bản WordPress mới nhất bằng lệnh sau:
```
# cd /var/www/html
# wget http://wordpress.org/latest.tar.gz
```
* Sau khi quá trình tải xuống hoàn tất, hãy giải nén tệp đã tải xuống bằng lệnh sau:
```
# tar -xzvf latest.tar.gz
```
Tiếp theo, thay đổi thư mục thành wordpress :
```
cd wordpress

```
* Tiếp theo, chỉnh sửa tệp cấu hình và xác định cài đặt cơ sở dữ liệu của bạn:

```
vim wp-config-sample.php
```
* Thay đổi các dòng sau:
```
define( 'DB_NAME', 'wordpress_db' );
define( 'DB_USER', 'wordpress_user' );
define( 'DB_PASSWORD', '12345678' );
```
```
define('AUTH_KEY',         '?HXr7 _M-^@n&iNi1%/|RCm@#,:jt T^YSPm.x_tPI|4[JX;nnu$RTX|~P|D-G*D');
define('SECURE_AUTH_KEY',  '-&IT?.[gVA1+,kF8TJl7=VUAC[kqJST| =; _t=c6!-E;xd~+%vTAu0A{1Zu+*qS');
define('LOGGED_IN_KEY',    'jztpP84Sj<3895!wXYS#9;t#:y.;SQ[:T+Z1aa_7A^,>C923(a8KLw#D5T*<x7/U');
define('NONCE_KEY',        ' k1?wuak`)/Xi5X$_}Xp(BJn$6I~ %h^NT^LdmKS9&-o7w:g`z.V`Smw%MtDZ$U>');
define('AUTH_SALT',        '$$q/.VhXgvt8//V5#ZV`?!`skW;: 3eRcy{a&:t|QSwXDi- aE| ?`(T^vn{@As/');
define('SECURE_AUTH_SALT', '2o/DZ<ciFOd,|_aP0~7=7aKzgB}-b.&Q^nZo>80`_ t)RBnQ4{@Lxi|4~Cja/uSq');
define('LOGGED_IN_SALT',   ':]OuwX,C#^4/b5=U`?MY8zm04+D+>3*TEb(_ 5#+yYkTIR$FbsM;(-[%7$jS6^.j');
define('NONCE_SALT',       '5!c6yjB%*n?x-2}QM%.% ^wCYT1ZOB+emNh1)sI=QQ]PLwhdSwhGTW+AmHu2]o!Q');
```
### Định cấu hình Nginx cho WordPress
* Tiếp theo, bạn sẽ cần tạo tệp cấu hình máy chủ ảo Nginx để lưu trữ trang web WordPress của mình.
```
# vim /etc/nginx/conf.d/wp.conf
```
* Thêm các dòng sau:
```
server {
        listen 80;
        root /var/www/html/wordpress;
        index  index.php index.html index.htm;
        server_name yourdomain.com;

        error_log /var/log/nginx/yourdomain.com_error.log;
        access_log /var/log/nginx/yourdomain.com_access.log;

        client_max_body_size 100M;
        location / {
                try_files $uri $uri/ /index.php?$args;
        }
        location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_pass unix:/run/php/php7.4-fpm.sock;
                fastcgi_param   SCRIPT_FILENAME $document_root$fastcgi_script_name;
        }
}
```
Tiếp theo, khởi động lại dịch vụ Nginx để áp dụng các thay đổi cấu hình:
```
# systemctl restart nginx
```

