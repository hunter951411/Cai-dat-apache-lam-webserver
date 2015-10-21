# cai--at-apache-lam-webserver
Cài đặt apache làm webserver

Apache web Server đi vào thế giới Server từ giữa những năm 90. Một nhà lập trình đã nhận định: “Apache như là 1 viên đá quí của chương trình mã nguồn mở, chi phí cho nó thì hầu như không có, hoạt động tốt hơn những đối thủ cạnh tranh khác, do đó nó được sử dụng ngày càng rộng rãi hơn những Web Servers thương mại khác”.
- Apache thường đi kèm với bản phân phối cùng Linux hoặc tải từ trang www.apache.org (nó đảm bảo cho bạn luôn có phiên bản mới nhất)
Tiến trình giải quyết yêu cầu và đặc điểm Apache
- Web Server là sự kết hợp giữa phần cứng và phần mềm phục
vụ cho những tài liệu HTTP khi client yêu cầu. Một web Server
cơ bản là một máy tính với hệ điều Linux, một file hệ thống đầy
đủ khà năng hổ trợ tốt cho ứng dụng Web Server, và một kết nối
mạng (đó là đặt trưng cho Internet hoặc tổ chức intranet). Khi
làm việc với Web Server cần có sự cân nhắc về các loại người
dùng đảm bảo hệ thống chạy thực sự hiệu quả, như là:
· Mục đích Web Server
· Tiến trình request/response cho Client
+ Mục đích của Web Server có thể thay đổi. Từ đơn giản như
mạng server nội bộ, đến phức tạp như e-commerce server. Nó
rất quan trọng để xác định mục đích Server trước khi xây dựng
và đưa vào hoạt động
+ Tiến trình request/response bắt đầu từ việc Client yêu cầu,
thường là từ trình duyệt Web, và sự trả lời từ Server, trả về
thông tin cho Client
- Tiến trình hoạt động Web Server
Biên soạn bởi mcsevietnam
53 / 80
+ Client sử dụng trình duyệt Web kết nối đến Server và đưa ra yêu
cầu. Yêu cầu này sử dụng giao thức HTTP mà người dùng muốn
Server cung cấp, và nói cho Server biết phiên bản nào HTTP dùng
để trả lời. Web Server lắng nghe những yêu cầu trên mạng. Khi một
yêu cầu được gửi đến , Web Server phân tích thành 3 phần:
· Cách thức sử dụng là GET, POST, hay HEAD.
Phương pháp GET yêu cầu Uniform Resource
Indicator (URI - sự chỉ định tài nguyên đồng nhất)
hoặc tài liệu từ Web server. Phương pháp POST gửi
dữ liệu điều khiển chỉ định bởi URI. Phương pháp
HEAD chỉ yêu cầu headers từ Web server.
· Tài nguyên đang được yêu cầu: Web Server đổi
URI, xác định đối tượng yêu cầu thành đường dẫn
vật lý trên hệ thống file của Web server
· Phiên bản HTTP
+ Web Server tiếp tục quy trình giải quyết yêu cầu bằng việc dùng
child processes ( tiến trình con ) để hoàn thành yêu cầu, và gửi trả
lời lại cho người dùng. Trong khoản thời gian đó Web Server sẽ
kiểm tra quyền hạn của Client. Trước khi hoàn tất yêu cầu, Web
Server sẽ xác định loại MIME của đối tượng được yêu cầu và sắp
đặt lại aliases
+ Yêu cầu Client đã được thực hiện. Trình duyệt Web sẽ cập nhập
thông tin. Ví dụ một trang HTML, một file, một thông báo lỗi sẽ xuất
hiện. Khi kết thúc yêu cầu Web server sẽ cập nhập lại file log và ngắt
kết nối đến Client.
- Đặc điểm Web Server:
Là phần mềm mã nguồn mở và hoàn toàn miễn phí. Hỗ trợ trên
những hệ điều hành khác nhau như: Linux, UNIX, Windows (95, 98,
NT, and 2000), OS/2, Solaris, FreeBSD, OpenBSD, và HP/UX.
Redhat Linux
54 / 80
Apache là một Modular, dễ lựa chọn và có thể tích hợp với sản
phẩm khác như là IBM Websphere
Cài đặt và cầu hình
A. Xây dựng và cài đặt Apache Web Server
- Khi bạn tải phiên bản Apache. Có 2 cách để cài : từ source code
hoặc từ tập tin nhị phân ( RPM ). Bạn có thể sử dụng cả 2 cách
để cài đặt.
- Cài đặt từ RPM
+  Tải file RPM từ trang http://www.rpmfind.net
+ Login với quyền Root và gõ lệnh:
 rpm –ivh apache-1 .3.xx-y.i386.rpm
 + Nếu muốn nâng cấp bạn phải stop Apache và gõ lệnh
 rpm –Uvh apache-1 .3.xx-y.i386.rpm
- Cài đặt từ Source: việc cài đặt từ nguồn không dễ như cài từ
RPM. Có những đòi hỏi khác nhau đối với những hệ điều hành
khác nhau
+ Tải file .tgz hay tar.gz từ trang
http://www.apache.org/dist/httpd/ vào thư mục /usr/local/src
+ Từ thư mục /usr/local/src giải nén file apache_1 .3.24.tar.gz gõ
lệnh
tar zxvf apache_1 .3.24.tar.gz
+ Apache source đã giải nén nằm trong thư mục
/usr/local/src/apache_1 .3.24
+ Tạo User và Group mặc định cho Apache
groupadd www ( tạo group www)
useradd –g www www
Chú ý: Sau khi tạo user www, dùng lệnh passwd với tham số -l
để khoá user www. Điều này sẽ đảm bảo tính bảo mật cao vì
sau này chỉ sử dụng root để cấu hình.
+  Sử dụng configure Script gõ lệnh:
#./configure --prefix=/usr/local/apache --server-uid=www --
server-gid=www --htdocsdir=/opt/web/html --cgidir=/opt/web/cgibin --enable-module=most --enable-shared=max
Biên soạn bởi mcsevietnam
55 / 80
· Tham số --server-uid=www chỉ định Apache server sẽ chạy với
user www. User www phải được tạo trước
· Tham số --server-gid=www chỉ định Apache server sẽ chạy với
nhóm www.
· Tham số --htdocsdir chỉ định Web site files mặc định sẽ đặt
trong thư mục /opt/web/html.
· Tham số --cgidir=/opt/web/cgi-bin chỉ định thư mục mặc định
cài CGI /opt/web/cgi-bin.
+ Gõ lệnh make
+ Gõ lệnh make install
+ Hướng dẫn cài đặt tham khảo từ
http://www.php.net/manual/en/install.unix.php
- Kiểm tra chạy thử Apache http://127.0.0.1
Redhat Linux
56 / 80
B. Cấu hình Apache
1 . Cấu hình Apache tổng quát
- Trong mục này chúng ta sẽ nghiên cứu bản hướng dẫn bảng
hướng dẫn cấu hình Apache tổng quát. Giá trị của bản dưới đây
là giá trị mặc định.
Tham số Miêu tả
ServerType standalone Điều khiển Apache chạy như
là standalone process hay
chạy ở inetd
ServerRoot /etc/httpd Định nghĩa thư mục gốc
Apache chứa tập tin cấu hình
và tập tin log
PidFile /var/run/httpd.pid Qui định tập tin chứa PID (
Process ID) của tiến trình
Master Server
Timeout 300 Thời gian tối đa tính bằng
giây mà Apache chờ để gửi
và nhận packet.
KeepAlive On Cho phép nhiều requests
trong cùng kết nối,. Tăng tốc
Biên soạn bởi mcsevietnam
57 / 80
phân phát tài liệu HTML
MaxKeepAliveRequests
100
Đặt số lượng request cho
phép cho mỗi connection
KeepAliveTimeout 1 5 Khoản thời gian trôi qua giữa
những yêu cầu từ cùng 1
Client trên cùng kết nối khi
KeepAlive ở chế độ On
MinSpareServers 5 Thời gian rãnh tối thiểu cho
Child servers
MaxSpareServers 20 Thời gian rãnh tối đa cho
Child servers ( do master
server sinh ra)
StartServers 8 Số lượng Child server được
tạo khi Apache được khởi
động
MaxClients 150 Số lượng kết nối cùng một lúc
mà Child server hỗ trợ
MaxRequestsPerChild 100 Số lượng Requests tối đa của
mỗi Child Server trước khi đạt
đến giới hạn
Listen [ipaddress:]80 Xác định sự kết hợp giữa địa
chỉ IP và Port mà Apache cho
phép kết nối, nhiều port có
thể được sử dụng
LoadModule modname
filename
Đường dẫn module hoặc tập
tin thư viện trên server và
thêm vào danh sách modules
đang hoạt động Modname
ClearModuleList Xóa list của module đang
hoạt động, nó sẽ được xây
dựng lại khi dùng lệnh
AddModule
AddModule module.c Kích hoạt những built-in
nhưng không active module
module.c
- Khi chỉ đường dẫn tập tin log file trong cấu hình, mặc định sẽ
được gán đường dẫn /etc/httpd. Ví dụ: tập tin log được khai báo
/logs/mylog.log thì đường dẫn sẽ là /etc/httpd/logs/mylog.log.
- Khai bào KeepAlive On sẽ cải thiện hoạt động của Server, làm
tăng sự kết nối thành công giữa Client và Server. Thông số
Redhat Linux
58 / 80
MinSpareServers và MaxSpareServers cho phép Apache tự điều
chỉnh, them vào và xóa đi các tiến trình khi tài nguyên hệ thống
thay đổi đột ngột. Khi có nhiều hơn số MaxClient kết nối, mỗi
yêu cầu sẽ được đưa vào hàng chờ ( first-in-first-out vào trước
ra trước ), những dịch vụ sẽ nhận theo thứ tự những kết hiện
thời và đóng lại, thong số này có lợi cho những WebSite có
lượng truy cập lớn.
- Đối với nhiều Sites giá trị tập tin cấu hình mặc định ở trên không
cần thay đổi. Và cũng không cần thay đổi thứ tự nạp Module và
kích hoạt Module bằng tham số LoadModule và AddModule cho
đến khi nào bạn biết bạn đang làm gì. Một vài Module lệ thuộc
vào các Module khác để hoạt động. Apache sẽ không Start lên
khi Module nạp không đúng
- Hình bên dưới là tập tin cấu hình mặc định của Apache không
có tham số AddModule, AddModule và ClearModuleList.
- Các thông số trên không cần thay đổi nhiều, giá trị này được
đưa ra bởi Apache Group.
2. Cấu hình mặc định ( không chứa Virtual hosts)
- Trước đây, nói đến Default Server hay Primary Server là nói đến
Web Server trả lời tất cả yêu cầu HTTP không dùng đến Virtual
Hosts hay Vitual Servers. Virtual Hosts hay Vitual Servers là
Biên soạn bởi mcsevietnam
59 / 80
Web Server chạy trên 1 máy giống như Default Server nhưng nó
là Main Server có nhiều host name hoặc IP. Cấu hình Default
Server có thể dùng cấu hình Vitual Servers.
- Bảng hướng dẫn cấu hình Default Server
Tham số Miêu tả
Port 80 Cổng dùng cho kết nối đến Server
User [#]apache Chỉ định UID có quyền thực thi Apache
Group [#]apache Chỉ định GID có quyền thực thi Apache
ServerAdmin
root@locahost
Địa chỉ mail sẽ được gửi đến Client khi
có lỗi
ServerName Tên Server như là
www.mydomain.com , khác tên host
trên server
DocumentRoot
“/var/www/html”
Đường dẫn thư mục mặc định chứa
trang web
UserDir public_html Đường dẫn thư mục con trong thư
muc Home của User dùng chứa trang
web
DirectoryIndex filename Chỉ định một hay nhiều tên file Index
khi mà yêu cầu không thể xác định file
AccessFileName
.htaccess
Qui định quyền truy cập tập tin trong
thư mục hay trong thư mục con, khi
tập tin này được chỉ định bởi
AccessFile
UseCanonicalName On Apache tự tham chiếu đến URL. Nếu
On sử dụng tên Server và Port, nếu off
sử dụng tên Host và Port cung cấp cho
Client
TypesConfig
/etc/mime.types
Quy định tên tập tin theo chuẩn MIME,
phần mở rộng được phép trên Server
DefaultType text/plain Chuẩn mặc định của kiểu MIME khi có
yêu cầu được gửi đến.
HostnameLookups Off Qui định việc Apache dung DNS
lookup khi kết nối đến
ErrorLog
/var/log/httpd/error _log
Xác định đường dẫn file error log
LogLevel warn Xác định thông tin chi tiết Apache ghi
vào tập tin error log
LogFormat formatstr Định dạng kiểu formatstr, Apache ghi
lại log vào Access log
Redhat Linux
60 / 80
CustomLog
/var/log/httpd/access_log
combined
Xác định tên của tập tin access log và
định dạng tập tin log.
ServerSignature On Hiển thị tên Server và phiên bản vào
cuối trang khi có thông báo lỗi, liệt kê
tập tin trong FTP,..
Alias urlpath dirpath Liên kết đường dẫn thư mục liên quan
đến DocumentRoot, đến thư mục tập
tin hệ thống, nằm ngoài hệ thống tập
tin server
ScriptAlias urlpath
dirpath
Hoạt động giống Alias và cũng dung
chỉ đường dẫn chức script CGI
IndexOptions
FancyIndexing
Xác định đặc điểm hoạt động thư mục
Apache indexing.
AddIconByEncoding
mimeencoding
Đặt biểu tượng xuất hiện bên cạnh tập
tin dạng mimeencoding, sử với
FancyIndexing
AddIconByType icon
mimetype
Đặt biểu tượng xuất hiện bên cạnh tập
tin dạng mimetype, sử với
FancyIndexing
AddIcon icon name Đặt biểu tượng bên cạnh những tập tin
có phần mở rộng name
DefaultIcon
/icons/unknown.gif
Đặt những biểu tượng mặc định với
những tập tin MIME hoặc không xác
định loại nào
AddDescription str file Gán kiểu String cho phần miêu tả với 1
hay nhiều tập tin file, dung với
FancyIndexing
AddEncoding
mimeencoding name
Gán kiểu mã hoá MIME bởi
mimeencoding cho tập tin có phần mở
rộng name
AddType mimetype
name
Thêm mimetype cho tập tin có phần
mở rộng name vào danh sách MIME
type
Biên soạn bởi mcsevietnam
61 / 80
Dưới đây là bản tham khảo cấu hình Default Server
Port 80
User apache
Group apache
ServerAdmin root@localhost
DocumentRoot “/var/www/html”
<Directory />
Options FollowSymLinks
AllowOverride None
</Directory>
<Directory “/var/www/html”>
Options Indexes Includes FollowSymLinks
AllowOverride None
Order allow,deny
Allow from all
</Directory>
UserDir public_html
DirectoryIndex index.html index.htm index.shtml index.php index.php4 index.php3
index.cgi
AccessFileName .htaccess
<Files ~ “^\.ht”>
Order allow,deny
Deny from all
</Files>
UseCanonicalName On
TypesConfig /etc/mime.types
DefaultType text/plain
<IfModule mod_mime_magic.c>
MIMEMagicFile conf/magic
</IfModule>
HostnameLookups Off
ErrorLog /var/log/httpd/error_log
LogLevel warn
LogFormat “%h %l %u %t \”%r\” %>s %b \”%{Referer}i\” \”%{User-Agent}i\”” combined
LogFormat “%h %l %u %t \”%r\” %>s %b” common
LogFormat “%{Referer}i -> %U” referer
LogFormat “%{User-agent}i” agent
CustomLog /var/log/httpd/access_log combined
ServerSignature On
Alias /icons/ “/var/www/icons/”
<Directory “/var/www/icons”>
Options Indexes MultiViews
AllowOverride None
Order allow,deny
Allow from all
Redhat Linux
62 / 80
</Directory>
ScriptAlias /cgi-bin/ “/var/www/cgi-bin/”
<Directory “/var/www/cgi-bin”>
AllowOverride None
Options ExecCGI
Order allow,deny
Allow from all
</Directory>
IndexOptions FancyIndexing
AddIconByEncoding (CMP,/icons/compressed.gif) x-compress x-gzip
AddIconByType (TXT,/icons/text.gif) text/*
AddIconByType (IMG,/icons/image2.gif) image/*
AddIconByType (SND,/icons/sound2.gif) audio/*
AddIconByType (VID,/icons/movie.gif) video/*
AddIcon /icons/binary.gif .bin .exe
AddIcon /icons/binhex.gif .hqx
AddIcon /icons/tar.gif .tar
AddIcon /icons/world2.gif .wrl .wrl.gz .vrml .vrm .iv
AddIcon /icons/compressed.gif .Z .z .tgz .gz .zip
AddIcon /icons/a.gif .ps .ai .eps
AddIcon /icons/layout.gif .html .shtml .htm .pdf
AddIcon /icons/text.gif .txt
AddIcon /icons/c.gif .c
AddIcon /icons/p.gif .pl .py
AddIcon /icons/f.gif .for
AddIcon /icons/dvi.gif .dvi
AddIcon /icons/uuencoded.gif .uu
AddIcon /icons/script.gif .conf .sh .shar .csh .ksh .tcl
AddIcon /icons/tex.gif .tex
AddIcon /icons/bomb.gif core
AddIcon /icons/back.gif ..
AddIcon /icons/hand.right.gif README
AddIcon /icons/folder.gif ^^DIRECTORY^^
AddIcon /icons/blank.gif ^^BLANKICON^^
DefaultIcon /icons/unknown.gif
ReadmeName README.html
HeaderName HEADER.html
IndexIgnore .??* *~ *# HEADER* README* RCS CVS *,v *,t
AddEncoding x-compress Z
AddEncoding x-gzip gz tgz
AddLanguage en .en
AddLanguage fr .fr
AddLanguage de .de
AddLanguage da .da
AddLanguage el .el
AddLanguage it .it
Biên soạn bởi mcsevietnam
63 / 80
LanguagePriority en fr de
<IfModule mod_php4.c>
AddType application/x-httpd-php .php4 .php3 .phtml .php
AddType application/x-httpd-php-source .phps
</IfModule>
<IfModule mod_php3.c>
AddType application/x-httpd-php3 .php3
AddType application/x-httpd-php3-source .phps
</IfModule>
<IfModule mod_php.c>
AddType application/x-httpd-php .phtml
</IfModule>
AddType application/x-tar .tgz
AddType text/html .shtml
AddHandler server-parsed .shtml
AddHandler imap-file map
BrowserMatch “Mozilla/2” nokeepalive
BrowserMatch “MSIE 4\.0b2;” nokeepalive downgrade-1 .0 force-response-1 .0
BrowserMatch “RealPlayer 4\.0” force-response-1 .0
BrowserMatch “Java/1 \.0” force-response-1 .0
BrowserMatch “JDK/1 \.0” force-response-1 .0
<IfModule mod_perl.c>
Alias /perl/ /var/www/perl/
<Location /perl>
SetHandler perl-script
PerlHandler Apache::Registry
Options +ExecCGI
</Location>
</IfModule>
Alias /doc/ /usr/share/doc/
<Location /doc>
order deny,allow
deny from all
allow from localhost .localdomain
Options Indexes FollowSymLinks
</Location>
- Tham số User và Group cho biết apache là chủ của Child
Server. Điều này sẽ an toàn hơn vì nó không cần những quyền
như root
- Tham số ServerName chỉ rõ những tên được trả về cho Client.
Ví dụ: nếu tên Server DNS là webbeast.mydomain.com bạn có
thể đặc tên Server là www.mydomain.com , lúc này Server sẽ trả
lời yêu cầu gửi đến www.mydomain.com
Redhat Linux
64 / 80
- DocumentRoot /var/www/html xác định thư mục chứa trang Web
của Server. Ví dụ: tên server www.mydomain.com khi Client
truy cập trang www.mydomain.com/index.html ,server sẽ trả về
tập tin /var/www/html/index.html cho Client
- Mỗi thẻ <Directory> </Directory> cấu hình quyền thư mục hay
thư mục con. Thẻ đầu tiên sẽ đặt quyền cho tất cả thư mục:
<Directory />
Options FollowSymLinks
AllowOverride None
</Directory>
+ Thẻ này sẽ tác dụng lên /var/www/html, /var/www/icons và
/var/www/cgi-bin
+ Dưới đây là những Options áp dụng lên thư mục là:
· All : chấp nhận tất cả Option trừ MultiViews. All là giá trị
mặc định
· ExecCGI : cho phép thực thi CGI
· FollowSymLinks : cho phép Link symbolic trong thư mục
· Includes : cho phép SSI (server-side includes)
· IncludesNOEXEC : cho phép SSI như không cho phép
lệnh #exec và #include cho CGI scripts
· Indexes : cho Server trả về danh sách list thư mục và
tập tin nếu không có index.html
· MultiViews : cho phép tìm kiếm MultiViews. Nếu Server
nhận được yêu cầu cho những tài nguyên không tồn tại
ví dụ /doc/resource, sau đó Server sẽ scans những thư
mục tên resouces.* ,nếu có sẽ lựa chọn phù hợp và trả
về cho Client
· None : tắt hết những option cho thư mục và thư mục con
· SymLinksIfOwnerMatch : chỉ cho Server đường dẫn đại
diện của những tập tin và thư mục của UID
+ Ở phần trên chỉ có một Option cho tất cả thư mục từ / (root) là
FollowSymLinks. Từ đó trở về sao tất cả những sự khác biệt với
Option / (root) sẽ có tác dụng trên thư mục bạn qui định
<Directory “/var/www/html”>
Options Indexes Includes FollowSymLinks
AllowOverride None
Order allow.deny
Allow from all
</Directory>
Biên soạn bởi mcsevietnam
65 / 80
+ Mục AllowOverride nói cho Server biết có quyền truy cập
những tập tin được qui định bởi AccessFileName
(AccessFileName .htaccess trong trường hợp trên). Nếu chọn
None Server sẽ lờ đi tập tin access file. Nếu chọn All tập tin
AccessFileName .htaccess sẽ có hiệu lực
+ Order điều khiển thứ tự áp đặc quyền hạn cho những tài
nguyên. Order có các giá trị:
· Order Deny.Allow : Xét quyền Deny trước Allow sau,
mặc định cho phép truy cập. Client không bị Deny và
được Allow thì được truy cập
· Order Allow.Deny : Xét quyền Allow trước Deny sau và
mặc định là Deny. Client nếu không Allow hoặc bị Deny
thì không được truy cập
· Order Mutual-failure : chỉ những Client có trong danh
sách Allow và không có trong danh sách Deny thì được
truy cập
- Cài đặt quyền hạn cho file và thư mục rất quan trọng cho
Apache chạy ổn định và bảo mật. Root sẽ làm chủ file httpd.conf
và thư mục bin. Những User (web) sẽ làm chủ thư mục log v.v..
3. Cấu hình Virtual Hosts
- Bản hướng dẫn sau đây dùng cho cấu hình Vitual Server
Tham số Miêu tả
<Virtual Host ipaddr[:port]>
directives
</VirtualHost>
Xác định địa chỉ IP của Virtual
host. Directives là những tham
số cấu hình default server
NameVirtualHost
ipaddr[:port]
Địa chỉ IP của Vitual Host
ServerName fqdn Tên đầy đủ của Server
VitualHost
ServerAlias altname Cho phép Vitual Host trả lời
những host names khác.
- Cấu hình chuẩn Vitual Server :
...
Port 80
ServerName webbeast.domain.com
NameVirtualHost 192.168.0.1
<VirtualHost 192.168.0.1 >
Redhat Linux
66 / 80
DocumentRoot /var/www/thisdomain
ServerName www.domain.com
</VirtualHost>
<VirtualHOst 192.168.0.1 >
DocumentRoot /var/www/thatdomain
ServerName www.that.domain.com
</VirtualHost>
- Trong ví dụ trên www.domain.com và www.that.domain.com là
những aliases (CNAME records) cho địa chỉ 192.168.0.1  , có
nghĩa 2 tên miền trên và webbeast.domain.com đều trỏ đến
192.168.0.1 . NameVirtualHost được qui định là địa chỉ
192.168.0.1 , tên ServerName là tên máy tính chạy Server
webbeast.domain.com . Yêu cầu gửi đến
www.that.doamain.com sẽ được đáp ứng tứ
/var/www/thatdomain, nhưng yêu cầu gửi đến www.domain.com
sẽ được đáp ứng tứ /var/www/thisdomain.
http://prntscr.com/8tnhqq

http://prntscr.com/8tnii7

http://prntscr.com/8tnqia
