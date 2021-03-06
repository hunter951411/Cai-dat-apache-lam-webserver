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

- Ta thêm 1 card mạng ảo bằng lệnh:
**sudo ifconfig eth0:1 192.168.221.140 up**

- Thêm thư mục cho Site Ipbased:

**sudo mkdir /var/www/html/hunter**

- Tạo file index.html:
<img src="http://i.imgur.com/i7iUpnR.png">

- Ta sửa lại file config trong tập tin /etc/apache2/sites-available/000-default.conf
- Thêm vào các thông tin cho site Ipbased:

<img src="http://i.imgur.com/Yyvad2S.png">

- Sau đó ta thử đánh địa chỉ của 2 trang web vào để kiểm tra:

Site chính, Ip add 192.168.221.139

<img src="http://i.imgur.com/ccUwQ9V.png">

Site Ipbased, Ip add 192.168.221.140

<img src="http://i.imgur.com/wPNjlii.png">
