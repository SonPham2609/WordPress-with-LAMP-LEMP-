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
```
# apt install nginx
```
* Để kiểm tra tường lửa cấu hình UFW nào khả dụng, hãy chạy:
```
# ufw app list
```
![image](https://user-images.githubusercontent.com/91528234/196124811-81d07573-12aa-4ab0-9171-96556e80f33c.png)

