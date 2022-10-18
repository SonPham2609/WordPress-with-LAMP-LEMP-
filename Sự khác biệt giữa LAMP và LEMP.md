# Tìm hiểu Lamp Stack là gì ?
## LAMP stack là gì?
* LAMP stack là nền tảng của các hosting website sử dụng chủ yếu Linux. LAMP là viết tắt của Linux, Apache, MySQL và PHP, là giải pháp máy chủ linh hoạt, được kết hợp từ 4 lớp giải pháp phần mềm riêng lẻ.

* Các thành phần này, được sắp xếp theo các lớp hỗ trợ lẫn nhau,.tạo thành các stack phần mềm. Các website và ứng dụng web chạy trên nền tảng của các stack cơ bản này.

    *  Linux: là lớp đầu tiên trong stack. Hệ điều hành này.là cơ sở nền tảng cho các lớp phần mềm khác.
    *   Apache: Lớp thứ hai bao gồm phần mềm web server,.thường là Apache Web (HTTP) Server. Lớp này nằm trên lớp Linux. Web server chịu trách nhiệm chuyển đổi các web browser.sang các website chính xác của chúng. Apache đã (và vẫn) là ứng dụng web server phổ biến nhất.trên public Internet hiện nay. Trên thực tế, Apache được ghi nhận là đóng một vai trò quan.trọng trong sự phát triển ban đầu của World Wide Web.
    * MySQL: Lớp thứ ba là nơi cơ sở dữ liệu database được lưu trữ. MySQL lưu trữ các chi tiết có thể được truy vấn bằng script để xây dựng một website. MySQL thường nằm trên Linux và cùng với Apache / lớp 2. Trong cấu hình highend, MySQL có thể được off load xuống 1 máy chủ lưu trữ riêng biệt.
     * PHP: là lớp trên cùng của stack. Lớp script bao gồm PHP và / hoặc các ngôn ngữ lập trình.web tương tự khác. Các website và ứng dụng web chạy trong lớp này.
Hầu hết các Developer nên biết về LAMP stack truyền thống.vì nó đã được sử dụng làm web từ rất lâu rồi. Tất cả các công nghệ backend như PHP. và Mysql đều rất phổ biến và được hỗ trợ bởi các nhà cung cấp hosting lớn. Do đó, ưu điểm lớn nhất của LAMP stack.là bảo mật và sự hỗ trợ rộng rãi. Các CMS phổ biến nhất như WordPress, Joomla, Drupal.. đều được phát triển trên nền PHP và Mysql.

* Cả Apache, PHP và Mysql đều có mã nguồn mở, đó là lý do tại sao Linux là lớp nền tảng cho môi trường này. Đây cũng là môi trường đơn giản nhất để các developer làm web trực tuyến.

![image](https://www.semtek.com.vn/wp-content/uploads/2021/01/lamp-stack-la-gi-1-768x480.png)


## LEMP stack là gì?
* Các thành phần cấu thành LEMP stack cũng gần tương tự với LAMP, chỉ khác là Apache sẽ được thay thế bởi nginx. Nginx được đọc là “engine-x”, giải thích cho chữ E trong “LEPM”, nginx cũng là một ứng dụng HTTP proxy nhưng không có được danh tiếng ấn tượng như Apache, tuy nhiên, nó có ưu điểm là cho phép xử lý tốc độ tải cao hơn đối với các HTTP request.

* Nginx giờ đây, đã đạt được sự thu hút đáng kể đối với người dùng khi nó bắt đầu được nhiều người sử dụng từ năm 2008 và hiện trở thành ứng dụng web server tiếng tăm thứ 2 sau Apache khi đề cập các active site theo báo cáo của Netcraft.

![image](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcST12roMOjK-Ns_P1Aid7C5gVLoTdAAnyPfZoUIOXurvP7wZ152DDCFXylxNlvKMcWAVPk&usqp=CAU)

## Sự khác biệt giữa LEMP và LAMP Stack là gì ?
* Sự khác biệt giữa LEMP và LAMP Stack là gì ? Như đã nói, khác biệt cơ bản giữa LAMP và LEMP stack là ở 2 thành phần Apache và Nginx. Vậy việc sử dụng nginx và Apache sẽ tạo ra những khác biệt gì? Chúng ta sẽ cùng so sánh riêng 2 phần mềm này để thấy được rõ hơn sự khác biệt:

### Apache
* Apache đã được sử dụng từ lâu (từ những năm 1995), có rất nhiều các module được viết và cả người dùng tham gia vào mở rộng hệ chức năng cho Apache.
* Phương pháp process/thread-oriented – sẽ bắt đầu chậm lại khi xuất hiện tải nặng, cần tạo ra các quy trình mới dẫn đến tiêu thụ nhiều RAM hơn, bên cạnh đó, cũng tạo ra các thread mới cạnh tranh các tài nguyên CPU và RAM;
* Giới hạn phải được thiết lập để đảm bảo rằng tài nguyên không bị quá tải, khi đạt đến giới hạn, các kết nối bổ sung sẽ bị từ chối;
* Yếu tố hạn chế trong điều chỉnh Apache: bộ nhớ và thế vị cho các dead-locked threads cạnh tranh cho cùng một CPU và bộ nhớ.
### Nginx
* Ứng dụng web server mã nguồn mở được viết để giải quyết các vấn đề về hiệu suất và khả năng mở rộng có liên quan đến Apache.
* Phương pháp Event-driven, không đồng bộ và không bị chặn, không tạo các process mới cho mỗi request từ web.
* Đặt số lượng cho các worker process và mỗi worker có thể xử lý hàng nghìn kết nối đồng thời
* Các module sẽ được chèn vào trong thời gian biên dịch, có trình biên dịch mã PHP bên trong (không cần đến module PHP).
Để kết luận thì nginx nhanh hơn và có khả năng xử lý tải cao.hơn nhiều so với Apache khi sử dụng cùng một bộ phần cứng. Tuy nhiên, Apache vẫn là tốt hơn nhiều khi nói đến chức.năng và tính sẵn sàng của các module cần thiết để làm việc với các ứng dụng máy chủ back-end.và chạy các ngôn ngữ kịch bản lệnh. Vậy nên việc lựa chọn sẽ phụ thuộc phần lớn vào những gì bạn.muốn chạy trên web server của mình. Việc chạy cả Apache và nginx trên cùng một máy chủ vẫn.có khả năng thực hiện được, và nó sẽ giúp người dùng có được.lợi ích tốt nhất từ cả 2 phương pháp. Ví dụ, bạn có thể chạy nginx như reverse proxy.trong khi để Apache chạy trong back-end.

### Phân quyền tệp và thư mục
Sử dụng máy chủ Linux việc phân quyền tệp và thư mục rất quan trọng. Ví dụ trong trường hợp người dùng upload files lên hệ thống mà bạn chưa phân quyền.thư mục thì lúc này việc đọc và ghi file lên máy chủ sẽ xảy ra lỗi. Và máy chủ web sẽ trả về lỗi 500.

Phân quyền trong Linux có 3 quyền hạn cơ bản của một user/group nào.đó trên một file/folder nào đó bao gồm:

* r (read) – quyền đọc file/folder.
* w (write) – quyền ghi/sửa nội dung file/folder.
* x (execute) – quyền thực thi (truy cập) thư mục. Đối với thư mục thì bạn cần phải có quyền execute thì mới dùng lệnh cd để truy cập vào được.
### Log và xem log error
Tùy thuộc vào config hệ thống mà các file log sẽ nằm ở vị trí tương ứng. Ví dụ webite của bạn hiển thị một màn hình trắng tinh và không có bất cứ thông báo.nào từ màn hình debug. Lúc này bạn cần xem log hệ thống xem sao nhé.

### Cấu hình cơ sở dữ liệu (Database)
Để mở rộng hay backup một hệ thống cũng như để đảm bảo một cơ sở dữ liệu toàn vẹn, không bị mất mát trước những sự cố. Việc hiểu biết nơi, cách cấu hình cơ sở dữ liệu cũng khá quan trọng bạn có thể tìm hiểu thêm về cấu hình Mysql Replication.

### Cài đặt package
Linux không cung cấp đầy đủ các package cho anh em developer, nó chỉ làm môi trường thôi, còn lại bạn cần package nào thì tải cái đó. Để tải package cần thiết ta có thể dùng lệnh apt hoặc là yum.

### Chỉnh sửa file trực tiếp trên máy chủ
Nhiều lúc bạn sẽ gặp phải lỗi và phải hot fix trực tiếp trên server, hoặc config web server. Việc này đòi hỏi bạn phải biết cách sử dụng trình soạn thảo của Linux thông qua câu lệnh vi ít nhất bạn có thể mở file và chỉnh sửa file. Lúc này bạn sẽ cần một list các câu lệnh Linux thông dụng để làm việc cho tiện, search thêm Google mỗi khi cần dùng nhé.

## Tham khảo thêm tại
https://bizflycloud.vn/tin-tuc/tong-quan-ve-lamp-lemp-stack-phan-biet-va-huong-dan-cai-dat-tren-server-20180820105455562.htm
