# Cai-dat-apache-lam-webserver
Named based và IP Based

#Cấu hình named based virtual host và ip based virtual host


#1.Named based 

- Một apache server cho phép host nhiều website có domain name khác nhau trên cùng một IP. Name based virtual host được sử dụng để cung cấp shared hosting.

##Cấu hình named based virtual host:

- Trước tiên tạo 2 folder chứa 2 Virtual Host muốn đặt bằng lệnh:

  **sudo mkdir /var/www/html/website1**

  **sudo mkdir /var/www/html/website2**
  
- Sau đó ta copy file config trong tập tin /etc/apache2/sites-available/000-default.conf để dùng sẵn file config mà apache có sẵn bằng lệnh:

  **sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/website1.dev.conf**

  **sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/website2.dev.conf**

- Sau đó ta vào từng file cấu hình vừa đc copy ra và sửa, bằng lệnh:

**sudo nano /etc/apache2/sites-available/website1.dev.conf**

- Ở đây mình sửa file website1.dev.conf, với website2 làm tương tự:

<img src="http://i.imgur.com/0G8c6gE.png">

- Thêm vào ServerName và ServerAlias xong đó Save lại.

- Tạo ra file index.html trong 2 site:

Site Website1.dev
<img src="http://i.imgur.com/itaDctj.png">

Site Website2.dev
<img src="http://i.imgur.com/8n2IbC8.png">

- Tiếp theo dùng lệnh để tạo liên kết, ta dùng lệnh:

**sudo a2ensites website1.dev**

**sudo a2ensites website2.dev**

- Ở đây chưa có DNS nên ta thêm vào file hosts trên máy chủ để test thử
<img src="http://i.imgur.com/ZfhGce5.png">

- Sau đó reload lại Apache2 và kiểm tra các trang web:

###Site webstie1.dev
<img src="http://i.imgur.com/kklQn75.png">

###Site webstie2.dev
<img src="http://i.imgur.com/ROBWLFz.png">

- Nguyên tắc chung của apache (cả name based và ip based virtualhost) sẽ là:
<ul>
<li>Tìm virtual host nào có ip:port phù hợp nhất. Nếu không có virtual host phù hợp thì apache sẽ đọc global server config để sử dụng. (Kiểm tra điều này bằng cách thay đổi tham số ip:port của từng virtualhost ví dụ chuyển hết về thành 192.168.56.1:80)</li>
<li>Sau đó, tìm virtual host có ServerName hoặc ServerAlias khớp với host header của request đến apache. Nếu không tìm thấy thì apache sẽ dùng default virtual host (Là virtual host đầu tiên khớp ip:port). Nếu tìm thấy nhiều hơn một virtual host có ServerName hoặc ServerAlias khớp thì apache dùng virtual host khớp đầu tiên</li>
</ul>

#2. IP based virtual host 

- Một apache server cho phép host nhiều website có domain khác nhau trên các IP khác nhau.

##Cấu hình IP based virtual host:

**Chuẩn bị**
<ServerRoot>/public_html/ipbased/web1/index.html
               <html><body><h1>IP based: Website 1</h1></body></html> 
<ServerRoot>/public_html/ipbased/web2/index.html
               <html><body><h1>IP based: Website 2</h1></body></html> 

- Mỗi website khi này cần các IP khác nhau. Tôi không muốn mua thêm NIC (Network Interface Card). Tôi sẽ cấu hình IP alias trên một interface để tăng số IP gán trên interface này.

sudo ifconfig vboxnet0:0 192.168.56.2 up

Kiểm tra lại bằng ifconfig, bạn sẽ thấy có một alias IP 192.168.56.2 gán trên sub interface vboxnet0:0

Để hủy IP alias, bạn dùng:

sudo ifconfig vboxnet0:0 192.168.56.2 down 

Cấu hình để apache server host hai website kể trên:

vi <ServerRoot>/conf/httpd.conf

Listen 80

<VirtualHost 192.168.56.1:80>
   ServerName web1.ipbased.example.com
   DocumentRoot <ServerRoot>/public_html/ipbased/web1/
</VirtualHost>

<VirtualHost 192.168.56.2:80>
   ServerName web2.ipbased.example.com
   DocumentRoot <ServerRoot>/public_html/ipbased/web2/
</VirtualHost>
