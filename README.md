# cai-dat-apache-lam-webserver
Cài đặt apache làm webserver

I. Giới thiệu
A. Quá trình phát triển
- Apache web Server đi vào thế giới Server từ giữa những năm 90. Một nhà lập trình đã nhận định: "Apache như là một viên đá quý của chương trình mã nguồn mở, chi phí cho nó thì hầu như không có, hoạt động tốt hơn những đối thủ cạnh tranh khác, do đó nó được sử dụng ngày càng rộng rãi hơn nhũng Web Servers thương mại khác".
- Apache thường đi kèm với bản phân phối Linux hoặc tải từ trang ww.apache.org để được dùng bản mới nhất.
- Apache thống trị thị trường web Server từ rất sớm.
B. Tiến trình giải quyết yêu cầu và đặc điểm Apache
- Web Server là sự kết hợp giữa phần cứng và phần mềm phục vụ cho những tài liệu HTTP khi client yêu cầu. Một web Server cơ bản là môt máy tính với hệ điều hành Linux, một file hệ thống đầy đủ khả năng hỗ trợ tốt cho ứng dựng Web Server, và một kết nối mạng (đó là đặc trưng cho Internet hoặc tổ chức Intranet). Khi làm việc với web server cần có sự cân nhắc về loại người dùng đảm bảo hệ thống chạy thực sự hiệu quả, như là:

	* Mục đích Web Server
	* Tiến trình request/response cho Client

+ Mục đích của Web Server có thể thay đổi. Từ đơn giản như mạng server nội bộ, đến phức tạp như e-commerce server. Nó rất quan trọng để xác định mục đích Server trước khi xây dựng và đưa vào hoạt động
+ Tiến trình request/response bắt đầu từ việc client yêu cầu, thường là từ trình duyệt Web, và sự trả lời từ Server, trả về thông tin cho Client
- Tiến trình hoạt động Web Server
+ Client sử dụng trình duyệt Web kết nối đến Server và đưa ra yêu cầu. Yêu cầu này sử dụng giao thức HTTP mà người dùng muốn Server cung cấp và nói cho Server biết phiển bảo nào HTTP dùng để trả lời. Web Server lắng nghe những yêu cầu trên mạng. Khi một yêu cầu được gửi đến, Web Server phân tích thành 3 thành phần:

	* Cách thức sử dụng là GET, POST hay HEAD. Phương pháp GET yêu cầu Uniform Resource Indicator (URI - Sự chỉ định tài nguyên đồng nhất) hoặc tài liệu từ Web Server. Phương pháp POST gửi dữ liệu điều khiển chỉ định bởi URI. Phương pháp HEAD chỉ yêu cầu headers từ Web server.
	* Tài nguyên đang được yêu cầu: Web Server đổi URI, xác định đói tương yêu cầu thành đường dẫn vật lý trên hệ thống file của Web Server
	* Phiên bản HTTP

+ Web server tiếp tục quy trình giải quyết yêu cầu bằng việc dùng Child Processes (tiến trình con) để hoàn thành yêu cầu, và gửi trả lời lại cho người dùng. Trong khoảng thời gian đó Web Server sẽ kiểm tra quyền hạn của Client. Trước khi hoàn tất yêu cầu, Web Server sẽ xác định loại MIME của đối tượng được yêu cầu và sắp đặt lại aliases
+ Yêu cầu Client đã được thực hiện. Trình duyệt Web sẽ cập nhập thông tin. Ví dụ một trang HTML, một file, một thông báo lỗi sẽ xuất hiện. Khi kết thúc yêu cầu Web Server sẽ cập nhập lại file log và ngắt kết nối đến Client.
- Đặc điểm của Web Server
+ Là phần mềm mã nguồn mở và hoàn toàn miễn phí. Hỗ trợ trên những hệ điều hành khác nhau.....
+ Apache là một Modular, dễ lựa chọn và có thể tích hợp với sản phẩm khác như IBM Websphere

II. Cài đặt và cấu hình

- Trước khi làm việc ở Ubuntu, nên tiến hành cập nhập gói phần mềm của Ubuntu lên phiên bản mới nhất với lệnh:

**apt-get update**
<img src="http://prntscr.com/8vi9rg" >

- Tên phần mềm Apache trên Ubuntu là apache2 nên sẽ cài đặt với lệnh sau:

**apt-get install apache2**
<img src="http://prntscr.com/8via5r" >

- Cài đặt trong thì truy cập vào địa chỉ Ip của máy chủ, sẽ thấy trang chào mừng của Apache
<img src=http://prntscr.com/8vib2b>

##Cấu trúc thư mục cấu hình Apache trên Ubuntu
/etc/apache2/conf-available/ : Thư mục này sẽ chứa các file thiết lập cấu hình sẵn của Apache trên Ubuntu, nhưng thiết lập trong đây sẽ chưa được áp dụng vì Ubuntu không load được thiết lập trong thư mục này.
/etc/apache2/conf-enabled/ : Thư mục chứa các file thiết lập cấu hình của Apache trên Ubuntu đang được bật. Hãy hiểu là nếu thưc mục này có một iên kết tượng trưng (symlink) qua một file module nào đó bên thư mục conf-available thì nó sẽ được bật.
/etc/apache2/mods-available/ : Thư mục chứa các file từng module của Apache trên Ubuntu nhưng chưa được bật.
/etc/apache2/mods-enabled/ : Thư mục chứa các file từng module của Apache trên Ubuntu đang được bật.
/etc/apache2/site-available/ : Thư mục chứa file cấu hình VirtualHost của Apache trên Ubuntu nhưng chưa được bật
/etc/apache2/site-enabled/ : Thư mục chứa file cấu hình VirtualHost của Apache trên Ubuntu đang được bật
/etc/apache2/apache.conf : File cấu hình Apache trên Ubuntu
/etc/apache2/envvars : File thiết lập các biến với giá trị có sẵn để sử dụng các file cấu hình.
/etc/apache2/magic : File thiết lập mod_mime_magic trên Apache.
/etc/apache2/ports.conf : File cấu hình cổng mạng của Apache (mặc định là Port 80)

##Thư mục gốc chứa dữ liệu website của Apache trên Ubuntu
Mặc định, Apache trên Ubuntu sẽ sử dụng thư mục  /var/www/html để chứa dữ liệu website gốc (load bằng IP hoặc hostname). Khi vào đây sẽ thấy một file index.html. đó chính là giao diện Apache Welcome đã thấy ở trên.

##Thêm VirtualHost (thêm domain) vào Apache trên Ubuntu
Cách thêm VirtualHost của Apache trên Ubuntu sẽ khác so với CentOS
Trước tiên, chúng ta cũng cần tạo cho nó một thư mục chứa dữ liệu cho domain cần thêm vào
**mkdir -p /home/hunter.com/public_html**
**mkdir -p /home/hunter.com/log**

Sau đó chúng ta cần copy file /etc/apache2/sites-available/000-default.conf ra một file mới file chứa cấu hình của domain cần thêm vào (hunter.com)
Lưu ý: Có thể file cấu hình mặc định của bạn không phải tên là default mà là “000-default.conf” nên tốt nhất bạn nên vào thư mục /etc/apache2/sites-available/ để xem rồi copy cho đúng.
Bây giờ hãy mở file /etc/apache2/sites-available/thachpham.dev.conf lên và sửa nội dung trong đó cho nó gọn hơn như thế này:

<VirtualHost *:80>
        ServerName thachpham.dev
        ServerAlias www.thachpham.dev
        ServerAdmin contact@thachpham.com
 
        DocumentRoot /home/thachpham.dev/public_html
 
        <Directory /home/thachpham.dev/public_html>
                Options FollowSymLinks
                AllowOverride All
                Order allow,deny
                Allow from all
                Require all granted
        </Directory>
 
        # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
        # error, crit, alert, emerg.
        # It is also possible to configure the loglevel for particular
        # modules, e.g.
        LogLevel error
 
        ErrorLog /home/thachpham.dev/log/error.log
        CustomLog /home/thachpham.dev/log/access.log combined
 
        # For most configuration files from conf-available/, which are
        # enabled or disabled at a global level, it is possible to
        # include a line for only one particular virtual host. For example the
        # following line enables the CGI configuration for this host only
        # after it has been globally disabled with "a2disconf".
        #Include conf-available/serve-cgi-bin.conf
</VirtualHost>
 
# vim: syntax=apache ts=4 sw=4 sts=4 sr noet
Nhớ thay:

	* SererName – Domain website cần thêm vào.
	* ServerAlias – Sử dụng một tên domain khác thay thế, hay còn gọi là Parked Domain nếu bạn đã từng sử dụng qua cPanel đó.
	* DocumentRoot – Đường dẫn tới thư mục chứa dữ liệu website của domain này mà ta đã tạo ở trên.
	* ErrorLog – Đường dẫn tới thư mục log đã tạo ở trên cho domain này.
	* CustomLog – Tương tự ErrorLog nhưng sẽ lưu log lại các lượt truy cập với file là access.log.

Sau đó chúng ta gõ lệnh sau để nó tự động tạo ra một symlink của file này vào thư mục sites-enabled để bật nó lên.
01
a2ensite thachpham.dev
Hãy nhớ rằng, thachpham.dev.conf là tên file cấu hình trong thư mục sites-available đã bỏ đuôi .conf.
Kết quả trả về:

root@vps103534:~# a2ensite thachpham.dev
Enabling site thachpham.dev.
To activate the new configuration, you need to run:
service apache2 reload
Gõ lệnh sau để khởi động lại Apache.
01
service apache2 restart
Bây giờ nếu bạn truy cập domain vừa thêm vào nó sẽ hiển thị ra lỗi 403 do thư mục của domain chứa có tập tin index để nó load. Hãy tạo ra một file index.html với nội dung sau và upload vào thư mục public_html của domain vừa thêm.

<html>
<head></head>
<body><h1>Tao VirtualHost Thanh Cong! </h1></body>
</html>
Kết quả:

Nếu bị lỗi 500
Nếu bạn vào website mà bị lỗi 500 (dễ gặp ở Ubuntu 10.04 32-bits), hãy mở lại file cấu hình virtualhost của bạn và xóa đoạn này đi:

Order allow,deny
Allow from all
Require all granted
I.4) Bật module mod_rewriteNếu bạn sử dụng WordPress sau này hay các website khác có sử dụng mod_rewrite để ghi lại đường dẫn thì phải bật module này lên. Ở phần thêm VirtualHost, chúng ta đã thêm AllowOverride All vào thiết lập thư mục gốc của domain rồi, nhưng chúng ta cũng cần bật module rewrite lên nữa. Hãy gõ lệnh sau:

a2enmod rewrite
Và khởi động lại Apache

service apache2 restart

