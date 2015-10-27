# Cài đặt apache làm webserver

#I. Giới thiệu

##A. Quá trình phát triển

- Apache web Server đi vào thế giới Server từ giữa những năm 90. Một nhà lập trình đã nhận định: "Apache như là một viên đá quý của chương trình mã nguồn mở, chi phí cho nó thì hầu như không có, hoạt động tốt hơn những đối thủ cạnh tranh khác, do đó nó được sử dụng ngày càng rộng rãi hơn nhũng Web Servers thương mại khác".

- Apache thường đi kèm với bản phân phối Linux hoặc tải từ trang ww.apache.org để được dùng bản mới nhất.

- Apache thống trị thị trường web Server từ rất sớm.

##B. Tiến trình giải quyết yêu cầu và đặc điểm Apache

- Web Server là sự kết hợp giữa phần cứng và phần mềm phục vụ cho những tài liệu HTTP khi client yêu cầu. Một web Server cơ bản là môt máy tính với hệ điều hành Linux, một file hệ thống đầy đủ khả năng hỗ trợ tốt cho ứng dựng Web Server, và một kết nối mạng (đó là đặc trưng cho Internet hoặc tổ chức Intranet). Khi làm việc với web server cần có sự cân nhắc về loại người dùng đảm bảo hệ thống chạy thực sự hiệu quả, như là:

+ Mục đích của Web Server có thể thay đổi. Từ đơn giản như mạng server nội bộ, đến phức tạp như e-commerce server. Nó rất quan trọng để xác định mục đích Server trước khi xây dựng và đưa vào hoạt động

+ Tiến trình request/response bắt đầu từ việc client yêu cầu, thường là từ trình duyệt Web, và sự trả lời từ Server, trả về thông tin cho Client

- Tiến trình hoạt động Web Server

+ Client sử dụng trình duyệt Web kết nối đến Server và đưa ra yêu cầu. Yêu cầu này sử dụng giao thức HTTP mà người dùng muốn Server cung cấp và nói cho Server biết phiển bảo nào HTTP dùng để trả lời. Web Server lắng nghe những yêu cầu trên mạng. Khi một yêu cầu được gửi đến, Web Server phân tích thành 3 thành phần:
<ul>
<li>Cách thức sử dụng là GET, POST hay HEAD. Phương pháp GET yêu cầu Uniform Resource Indicator (URI - Sự chỉ định tài nguyên đồng nhất) hoặc tài liệu từ Web Server. Phương pháp POST gửi dữ liệu điều khiển chỉ định bởi URI. Phương pháp HEAD chỉ yêu cầu headers từ Web server.</li>
<li>Tài nguyên đang được yêu cầu: Web Server đổi URI, xác định đói tương yêu cầu thành đường dẫn vật lý trên hệ thống file của Web Server</li>
<li>Phiên bản HTTP</li>
</ul>
+ Web server tiếp tục quy trình giải quyết yêu cầu bằng việc dùng Child Processes (tiến trình con) để hoàn thành yêu cầu, và gửi trả lời lại cho người dùng. Trong khoảng thời gian đó Web Server sẽ kiểm tra quyền hạn của Client. Trước khi hoàn tất yêu cầu, Web Server sẽ xác định loại MIME của đối tượng được yêu cầu và sắp đặt lại aliases

+ Yêu cầu Client đã được thực hiện. Trình duyệt Web sẽ cập nhập thông tin. Ví dụ một trang HTML, một file, một thông báo lỗi sẽ xuất hiện. Khi kết thúc yêu cầu Web Server sẽ cập nhập lại file log và ngắt kết nối đến Client.

- Đặc điểm của Web Server
<ul>
<li>Là phần mềm mã nguồn mở và hoàn toàn miễn phí. Hỗ trợ trên những hệ điều hành khác nhau.....</li>
<li>Apache là một Modular, dễ lựa chọn và có thể tích hợp với sản phẩm khác như IBM Websphere</li>
</ul>

#II. Cài đặt và cấu hình

- Trước khi làm việc ở Ubuntu, nên tiến hành cập nhập gói phần mềm của Ubuntu lên phiên bản mới nhất với lệnh:

**apt-get update**
<img src="http://prntscr.com/8vi9rg" >

- Tên phần mềm Apache trên Ubuntu là apache2 nên sẽ cài đặt với lệnh sau:

**apt-get install apache2**
<img src="http://prntscr.com/8via5r" >

- Cài đặt trong thì truy cập vào địa chỉ Ip của máy chủ, sẽ thấy trang chào mừng của Apache
<img src=http://prntscr.com/8vib2b>

###Cấu trúc thư mục cấu hình Apache trên Ubuntu

- **/etc/apache2/conf-available/** : Thư mục này sẽ chứa các file thiết lập cấu hình sẵn của Apache trên Ubuntu, nhưng thiết lập trong đây sẽ chưa được áp dụng vì Ubuntu không load được thiết lập trong thư mục này.

- **/etc/apache2/conf-enabled/** : Thư mục chứa các file thiết lập cấu hình của Apache trên Ubuntu đang được bật. Hãy hiểu là nếu thưc mục này có một iên kết tượng trưng (symlink) qua một file module nào đó bên thư mục conf-available thì nó sẽ được bật.
- **/etc/apache2/mods-available/** : Thư mục chứa các file từng module của Apache trên Ubuntu nhưng chưa được bật.
- **/etc/apache2/mods-enabled/** : Thư mục chứa các file từng module của Apache trên Ubuntu đang được bật.
- **/etc/apache2/site-available/** : Thư mục chứa file cấu hình VirtualHost của Apache trên Ubuntu nhưng chưa được bật
- **/etc/apache2/site-enabled/** : Thư mục chứa file cấu hình VirtualHost của Apache trên Ubuntu đang được bật
- **/etc/apache2/apache.conf** : File cấu hình Apache trên Ubuntu
- **/etc/apache2/envvars** : File thiết lập các biến với giá trị có sẵn để sử dụng các file cấu hình.
- **/etc/apache2/magic** : File thiết lập mod_mime_magic trên Apache.
- **/etc/apache2/ports.conf** : File cấu hình cổng mạng của Apache (mặc định là Port 80)

##Thư mục gốc chứa dữ liệu website của Apache trên Ubuntu

- Mặc định, Apache trên Ubuntu sẽ sử dụng thư mục  /var/www/html để chứa dữ liệu website gốc (load bằng IP hoặc hostname). Khi vào đây sẽ thấy một file index.html. đó chính là giao diện Apache Welcome đã thấy ở trên.

##Thêm VirtualHost (thêm domain) vào Apache trên Ubuntu

- Cách thêm VirtualHost của Apache trên Ubuntu sẽ khác so với CentOS. Trước tiên, chúng ta cũng cần tạo cho nó một thư mục chứa dữ liệu cho domain cần thêm vào

	**#mkdir /var/www/html/hunter**

- Sau đó chúng ta cần copy file /etc/apache2/sites-available/000-default.conf ra một file mới file chứa cấu hình của domain cần thêm vào (hunter.com)

	**#cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/hunter.dev.conf**
	

Bây giờ hãy mở file /etc/apache2/sites-available/hunter.dev.conf lên và sửa nội dung trong đó:

<img src="http://prntscr.com/8vrh70">	

	* SererName – Domain website cần thêm vào.
	* ServerAlias – Sử dụng một tên domain khác thay thế, hay còn gọi là Parked Domain nếu bạn đã từng sử dụng qua cPanel đó.
	* DocumentRoot – Đường dẫn tới thư mục chứa dữ liệu website của domain này mà ta đã tạo ở trên.
	* ErrorLog – Đường dẫn tới thư mục log đã tạo ở trên cho domain này.
	* CustomLog – Tương tự ErrorLog nhưng sẽ lưu log lại các lượt truy cập với file là access.log.

Sau đó chúng ta gõ lệnh sau để nó tự động tạo ra một symlink của file này vào thư mục sites-enabled để bật nó lên.

	**a2ensite hunter.dev**

Tạo file index.html trong tập tin /var/www/html/hunter/

<img src="http://prntscr.com/8vriit">

Khởi động lại Apache.

	**#service apache2 restart**

Vì chưa có DNS dựng sẵn nên ta sẽ sửa luôn trong file host của chính máy chủ ở tập tin /etc/hosts

<img src="http://prntscr.com/8vrjq0">

Sau khi hoàn tất gõ vào trình duyệt hunter.dev. Hiện ra như hình dưới là đã cài Virtual Host thành công

<img src="http://prntscr.com/8vrlvm">




#III. Mô hình Apache core

##1.. Apache core:

- **http_protocol.c:** chứa các procedure để giao tiếp với clinet thông qua giao thức http. Mọi thứ trao đổi với clinet do thằng này đảm nhiệm.
- **http_main.c:** khởi động server, tạo vòng lặp chính để đợi + chấp nhận các kết nối, và quản lý toàn bộ timeout.
- **http_request.c:** quản lý tiến trình xử lý bản tin request, đảm bảo chuyển các bản tin điều khiển tới các modul phù hợp theo đúng thứ tự + quản lý lỗi xảy ra trên server.
- **http_core.c:** triển khai các chức năng cơ bản nhất trên Apache.
- **alloc.c:** kiểm soát việc phân chia tài nguyên và lưu trữ các thông tin về sự phân chia đó.
- **http_config.c:** xử lý file cấu hình và hỗ trợ virtual host + liệt kê các modul sử dụng trong apache.

##2. Request processing – luồng request, cách xử lý một request từ phía client.

- Cách xử lý được thực hiện theo trình tự sau:
<ul>
<li>1, Phân giải địa chỉ.</li>
<li>2, Kiểm tra truy cập và cấp quyền truy cập đến những tài nguyên cần thiết.</li>
<li>3, Xác định MIME (Multipurpose Internet Mail Extensions) của đối tượng truy vấn. Tức là thông tin về kiểu định dạng của tài nguyên trên server được gọi tên trong gói HTTP Request.</li>
<li>4, Chỉnh sửa lại một số thông tin ( ví dụ thay đổi Alisa thành một đường dẫn thực – định nghĩa trong modul alisa thuộc phần mod_alisa).</li>
<li>5, Gửi lại dữ liệu cho clinet.</li>
<li>6, Ghi lại log.</li>
</ul>

##3. Communicating between modules – giao tiếp giữa các module

- Các modules không giao tiếp trực tiếp với nhau mà thông qua core.

##4. Handler

- Handler là một hành động được Apache định nghĩa riêng cho từng loại file nhất định. Mặc định, tùy loại file mà sẽ được xử lý theo các cách khác nhau.

- Handler có thể được cấu hình dựa trên phần mở rộng của file hoặc theo từng thư mục

- Mặc định, có 7 loại handler:
<ul>
<li>Send-as-is: dùng trong module mod_asis, dùng để gửi trả gói tin cho clinet mà không sử dụng đầy đủ HTTP header.</li>
<li>Cgi-script: coi file là một cgi-script (tương ứng modul: mod_cgi).</li>
<li>Imap-file sử dụng chung với mod_imagemap.</li>
<li>Server-info: lấy thông tin về cấu hình của server.</li>
<li>Server-status: lấy thông tin về trạng thái của server.</li>
<li>Type – map: sử dụng cùng với module mod_negotiation.</li>
<li>Default-handler: gửi file sử dụng default_handler().</li>
</ul>


Nếu muốn có một modul tham gia vào xử lý, thiết lập thêm r->handler, và phải thêm vào trước khi trình xử lý invoke_handler được yêu cầu.

##5. Modules

- Các module được cài đặt sẵn trong quá trinh buil Apache, hoặc có thể add thêm.

- Mặc định sẵn sẽ có các modules như sau – các modul này sẽ hoạt động lần lượt theo request của người dùng (6 bước, xem lại ở mục 2 – request processing)

###5.1 chuyển đổi giữa các URI thành filename trên server:

- **Mod_userdir**: chuyển thư mục home cho từng user

- **Mod_rewrite**: điều chỉnh lại đường dẫn URL

###5.2 Giai đoạn Xác thực/ Phân quyền:

- **Mod_ahth, mod_auth_anon, mod_auth_db, mod_ahth_dbm**: các kiểu xác thực người dùng

- **Mod_access**: kiểm soát truy cập theo từng host

###5.3, Xác định MIME của đối tượng được truy vấn:

- **Mod_mime**: xác định loại file bằng cách dựa vào phần mở rộng

- **Mod_mime_magic**: xác định loại file bằng cách sử dụng magic number

###5.4, chỉnh sửa đường dẫn:

- **Mod_alias**: thay thế alias bằng đường dẫn thực trên server

- **Mod_env**: thay đổi các tham số hệ thống dựa trên thông tin trong file cấu hình

- **Mod_spelling**: tự động sửa lỗi trông URL

###5.5, gửi trả lại cho clinet

- **Mod_actions**: các scrip cho từng loại file sẽ được thực thi

- **Mod_asis**: gửi file nguyên dạng

- **Mod_autoindex**:

- **Mod_cgi**: gọi scrip CGI và trả lại kết quả

- **Mod_include**:

- **Mod_dir**: xử lý về thư mục

- **Mod_imap**: xử lý về image-map file

###5.6, Ghi log:

- **Mod_log_**: các modul log khác nhau

####Gồm 3 thành phần chính:
<ul>
<li>1, Global Evironment: các thông số để cấu hình điều khiển hoạt động của toàn bộ ApacheServer</li>
<li>2, Các directive định nghĩa các thông số của “main” hay “default” server</li>
<li>3, Các tham số riêng cho từng virtual host</li>
</ul>

##6. Apache configuration File

###6.1 Config/ Global enviroment:

####1, ServerToken & ServerSignature

	ServerSignature Off
	ServerTokens Prod

- Giảm nguy cơ bị lộ thông tin về phiên bản Apache đang chạy trên server.

####2, Server Root

- Cấu hình thư mục lưu trữ chính của Apache

####3, PidFile

- Thông số này lưu trữ đường dẫn đến file httpd.pid, là file lưu trữ process ID của Apache mỗi khi khởi chạy. Mặc định, file này nằm ở /etc/httpd/run/httpd.pid và trong đó chỉ có 1 con số (ví dụ: 1231)

####4, Timeout

- Thời gian tim out cho hệt hống, giá trị mặc định

####5, KeepAlive

- KeepAlive là một hình thức có thể giúp tăng tốc độ tải trang khi không mở kết nối cho từng request một. Tuy nhiên, khi bị tấn công Ddos, thì nên tắt chắc năng này để giảm thiểu ảnh hưởng tới hệ thống. Nhưng với CDN thì có lẽ nên bật vì số lượng Edge rõ lắm. Thông số KeepAlive cho phép kiểu kết nối này được bật hay không.


####6, Listen

- Cấu hình địa chỉ IP và port để Apache nhận các gói request

####7, LoadModul

- Gọi modul nào sẽ khởi động cùng hệ thống

####8, Include

- Cấu hình thư mục chứa file config
	
###6.2 Config/ Main Server Configuration	

####1, ServerAdmin

- Cấu hình địa chỉ email của người quản trị, sẽ hiển thị trên một số trang (như trang báo lỗi 404)

####2, UseCanonicalName

- Thông thường, khi sử dụng Name-based Virutal Host thì nên set là off – không hỉu

####3, DocumentRoot

- Thư mục lưu trữ các đường dẫn chứa mã nguồn của website, các requet từ clinet sẽ chỉ truy xuất thông tin từ thư mục này.

Windows: c:/wampp/www
Centos: /var/www/html/

####4, DirectoryIndex

- Chỉ định file mặc định được trả về cho clinet khi có request tới một thư mục nào đó, thông thường các file như index.html, index.php sẽ được sử dụng.

DirectoryIndex index.htm index.html index.html.var

####5, AccessFileName

- Chỉ định file bổ sung các cấu hình riêng cho từng thư mục nhất định. Thông thường sẽ là file “.htaccess” – file này trong mỗi virutalhost sẽ có, nói lên việc truy cập, blah blah…

####6, TypesConfig

- Chỉ đường dẫn tới file mime.types. File này sẽ giúp cho Apache tra cứu phần mở rộng của file để xác định MIME type trong 

HTTP Header 
DefaultType  text/plain

- Mặc định, MIME type cho các file apache không xác định được sẽ là kiểu file text

####7, HostnameLookups

- Cấu hình ghi log tên hostname của clinet hay chỉ đại chỉ IP của clinet (thường mặc định để off)

####8, ErrorLog

- Cấu hình đường lưu trữ Error của hệ thống

####9, LogLevel

- Mức độ ghi log. Giống như syslog, log trong Apache cũng được ghi thành 7 mức độ khác nhau từ cao xuống thấp là:
Emergency
Alert
Critical
Error
Warning
Notification
Information
Debug

####10, Log

Dùng cái này để chạy nhiều site trên cùng một server.
Có 2 loại cấu hình
IP-based VirtualHost: trỏ từng website vào các địa chỉ IP (trên server có nhiều hơn 1IP)
Name-based Virtual Host: thông tin hostname được lưu trong phần Header của bản tin HTTP Request. Khi nhận các bản tin Request này, thì apache sẽ chuyển đến các virtual host tương ứng (cần 1 IP thôi)
Các vitual host được thực hiện trong file httpd.conf hoặc file httpd-vhost.conf. Với các thành phần cụ thể như sau:
Đường dẫn tới thư mục lưu trữ web
Server name
Đường dẫn tới log

###6.3 Một số trường – cấu hình apache server

Các thông số trong http.conf
Server Root: chỉ dẫn vị trí cài đặt Apache
Cú pháp : ServerRoot <vị trí cài đặt Apache>

Listen : quy định địa chỉ IP hoặc cổng mà Apache nhận kết nối từ client
Cú pháp: listen <port/IP>

Server Admin:địa chỉ mail của người quản trị hệ thống
Cú pháp: ServerAdmin <địa chỉ email>

Server name: tên máy tính của server
Cú pháp: ServerName <tên máy server>ort

DocumentRoot: lưu trữ nội dung của website, web server lấy lấy những tập tin trong thư mục (htdocs) phục vụ cho yêu cầu của client
Cú pháp: DocumentRoot <đường dẫn thư mục>

DirectoryIndex:các tập tin mặc định được truy vấn khi truy cập web
Cú pháp: DirectoryIndex <danh sách các tập tin>

Error Log :chỉ ra tập tin để server ghi vào những lỗi mà nó gặp phải
Cú pháp:ErrorLog <vị trí log>

Alias:ánh xạ đường dẫn cục bộ(không nằm trong document) thành đường dẫn địa chỉ URL
Cú pháp:alias<đường dẫn http><đường dẫn cục bộ>

##7.    Mutiprocessing

Có 2 khái niệm về khả năng xử lý của webserver

Single-threaded web server: không có khả năng xử lý đồng thời nhiều request một lúc
Multi-thread web server: có khả năng xử lý nhiều request một lúc, gồm 2 kĩ thuật chính là :
Multi-process: tạo process cho từng request, có 2 loại chủ yếu
Prefork: tạo các process riêng biệt. Lỗi trên 1 process không gây ảnh hưởng tới process khác
Multi-thread: tạo Thread mới cho từng request
Worker: tạo các thread riêng biệt cho request, hợp với đa lõi, nhưng nếu có 1 thread bị lỗi sẽ có thể gây ảnh hưởng tới các thread trong cùng process đó
Đánh giá chung: Thread thì tiết kiệm tài nguyên hơn là Process. Nhưng còn tùy thuộc vào các yếu tố khác nhau, ví dụ PHP thì nên dùng Prefork, vì nó không ổn định với hình thức chia sẻ bộ nhớ chung (Process thì sẽ tạo tài nguyên riêng cho từng process, nên sẽ không bị ảnh hưởng khi dùng PHP). (Thread dùng chung bộ nhớ, tài nguyên à ảnh hưởng)

( tra thêm tài liệu để hiểu rõ sự khác biệt giữa process và thread)
