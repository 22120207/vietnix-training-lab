# Lab Triển Khai LEMP & LAMP Stack

## A. Nội dung cần nắm trước khi làm bài Lab

### 1. Reverse Proxy
![Reverse Proxy Flow](reverse-proxy-flow.png)

Reverse Proxy bản chất là một server tiếp nhận request từ phía Clients, và sau đó nó sẽ điều hướng các requests đến cho phía web server.
Việc dựng một Reverse Proxy giúp giấu đi địa chỉ IP thực của phía web server, tránh được việc các hacker DDOS đến web server dẫn đến tình trạng quá tải. Ngoài ra ta cũng có thể cấu hình Reverse Proxy load balancing các request đến web server sao cho đảm bảo tài nguyên các từng web server đều được tận dụng ở mức tối ưu nhất.

### 2. Phân biệt giữa static và dynamic website

#### 2.1 Static Website
Static Website là website tĩnh, nội dung không thay đổi theo thời gian thực. Khi Clients truy cập đến website thì phía web server sẽ trả về các file tĩnh như HTML, CSS, Javascript cho phía Client. Vì các file này là file tĩnh nên phía server không cần phải thực hiện các tác vụ xử lý và nó cũng không cần phải tương tác với database → do đó tốc độ truy cập sẽ nhanh hơn so với Dynamic Website.

Một vài ví dụ về Static Website như: Portfolio Page, Landing Pages, ...

#### 2.2 Dynamic Website
Dynamic Website là website động, nội dung thay đổi theo thời gian thực. Website sẽ có backend để xử lý request đến từ Clients (có thể thêm/xóa/sửa/lấy data từ phía database) và trả kết quả về cho người dùng. Vì phía server phải thực hiện các tác vụ để xử lý request nên tốc độ sẽ chậm hơn Static Website. Nhưng đổi lại thì người dùng có thể tương tác, nhận kết quả từ phía web server.

Một vài ví dụ về Dynamic Website như: Ecommerce Website, ...

### 3. LAMP/LEMP stack là gì?

#### 3.1. LAMP stack
LAMP stack bao gồm Linux, Apache, MySQL, PHP. Trong đó ta sẽ triển khai Apache như một web server. PHP dùng để dựng nên phía backend và giao tiếp với Database là MySQL để thêm/xóa/cập nhật dữ liệu.

#### 3.2. LEMP stack
LEMP cũng tương tự như LAMP nhưng thay vì dùng Apache làm Web Server thì ta sẽ dùng Nginx. Nginx sẽ phù hợp với các trường hợp host static web, nhanh và nhẹ hơn so với Apache. Ngược lại thì Apache sẽ phù hợp với việc host web động và nó có thể cấu hình nhiều tính năng hơn so với Nginx.

#### 3.3. Trường hợp sử dụng

**Apache** sử dụng cấu trúc processed-based, nghĩa là mỗi yêu cầu sẽ được nó tạo một tiến trình (process) riêng để xử lý cho từng requests. Về lợi thì sẽ giúp các requests được xử lý riêng biệt → ổn định. Về vấn đề phát sinh đó chính là trường hợp cao điểm có nhiều requests đến server thì sẽ dẫn đến tình trạng bị quá tải, vì càng nhiều requests thì càng nhiều process được tạo ra → tốn CPU và Memory

**Nginx** sử dụng kiến trúc event-driven và đơn luồng. Nghĩa là nó chỉ sử dụng một thread duy nhất để nhận các request từ phía Clients và đưa vào hàng đợi để xử lý các events. Vì chỉ sử dụng một luồng và chỉ việc đưa các request đến cho hàng đợi events xử lý. Các requests sẽ được phân chia thành events khác nhau để xử lý. Ví dụ đối với Apache thì nếu nhận N requests thì nó sẽ tạo ra N process để xử lý. Còn đối với Nginx thì đối các N requests đó thì nó sẽ tạo ra các events chung để xử lý đối với từng requests 

→ Nếu Nginx dùng để host static web thì nó chỉ events là gửi các static file về cho người dùng mà không cần phải gửi requests đến để chờ phía backend xử lý.
→ Còn Apache sẽ ổn định hơn khi hosting dynamic web vì nó tạo từng process riêng để xử lý cho từng requests, giúp cô lập trong trường hợp xảy ra lỗi.

#### 3.4. Một trang web có thể vừa static vừa dynamic không ?
Một trang web có thể vừa static và dynamic. Đối với phía Frontend, ta sẽ dùng các static file như HTML, CSS, Javascripts hoặc ReactJS, VueJS,... Khi Clients tương tác với phía Frontend thì nó sẽ gửi requests đến phía Backend (PHP, Nodejs, Java,...) để xử lý và trả về kết cho phía Frontend để hiển thị cho người dùng

**Dựa vào những ưu điểm của từng webserver đã nêu trên, ta có thể tận dụng để tối ưu đối với trường hợp website vừa staic vừa dynammic như sau:**

→ Vì nginx phù hợp cho việc xử nhiều kết nối đồng thời đối với những static files, nên ta sẽ dùng nó để host Frontend Server, nhập các requests từ người dùng. Đối với trường hợp web browser của Clients truy cập vào website để tải về các static files (html,css, javascripts, images, videos, ...) có sẵn ở server Frontend, thì Nginx sẽ trả về cho phía Clients mà không cần gửi requests đến phía Backend Server là Apache → giúp Apache không bị quá tải/tốn CPU, RAM để xử lý.

→ Ở phía Backend Server ta sẽ host bằng Apache. Trường hợp người dùng cần tương tác với tải các file tĩnh (PHP scripts,...) thì Nginx sẽ hoạt động như 1 reverse proxy gửi requests đến cho phía Apache để xử lý và trả kết quả lại cho Clients.

---

## B. Lab

**OS Template sử dụng:** `Ubuntu-Server-22.04-x64`

---

### I. Triển khai LEMP stack chạy Wordpress

#### 1. Link kết quả deploy
[https://wordpress.caotienminh.software](https://wordpress.caotienminh.software)

#### 2. Từng bước cấu hình

##### 2.1. Tải Nginx

Chạy các câu lệnh sau để tải nginx:
```bash
sudo apt update
sudo apt install nginx
```

Chạy 2 câu lệnh sau để enable nginx luôn start ngay cả khi bị reboot:
```bash
sudo systemctl enable nginx
sudo systemctl start nginx
```

##### 2.2. Tải MySQL
```bash
sudo apt install mysql-server -y
mysql -u root -p
```

Sau khi login thành công vào MySQL, chạy cách lệnh sau đây:
```sql
CREATE DATABASE wordpress_db;
CREATE USER 'wordpress_user'@'localhost' IDENTIFIED BY 'strong_password';
GRANT ALL PRIVILEGES ON wordpress_db.* TO 'wordpress_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

##### 2.3. Tải PHP
```bash
sudo apt install php8.1-fpm php8.1-mysql php8.1-curl php8.1-gd php8.1-mbstring php8.1-xml php8.1-xmlrpc php8.1-soap php8.1-intl php8.1-zip -y 
sudo systemctl start php8.1-fpm 
sudo systemctl enable php8.1-fpm
```

##### 2.4. Tải Wordpress
```bash
sudo mkdir -p /var/www/wordpress.caotienminh.software
cd /tmp
wget https://wordpress.org/latest.tar.gz
tar -xvzf latest.tar.gz
sudo chown -R www-data:www-data /var/www/www/wordpress.caotienminh.software
sudo find /var/www/www/wordpress.caotienminh.software/ -type d -exec chmod 755 {} \;
sudo find /var/www/www/wordpress.caotienminh.software/ -type f -exec chmod 644 {} \;
```

Cấu hình wordpress:
```bash
sudo cp /var/www/wordpress.caotienminh.software/wp-config-sample.php /var/www/wordpress.caotienminh.software/wp-config.php
sudo nano /var/www/wordpress.caotienminh.software/wp-config.php
```

Dán các dòng sau vào file cấu hình của wordpress (thông tin user, password, database của MySQL):
```php
define( 'DB_NAME', 'wordpress_db' );
define( 'DB_USER', 'wordpress_user' );  
define( 'DB_PASSWORD', 'strong_password' );
```

##### 2.5. Cấu hình Nginx
```bash
sudo nano /etc/nginx/sites-available/wordpress.caotienminh.software
```

Dán các dòng sau vào file cấu hình của wordpress (thông tin user, password, database của MySQL)
```nginx
server {
    server_name wordpress.caotienminh.software www.wordpress.caotienminh.software;
    root /var/www/wordpress.caotienminh.software;

    index index.php index.html index.htm;
    client_max_body_size 20M;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }

    location ~ /\.ht {
        deny all;
    }

    location ~ /(wp-content|wp-includes|wp-admin)/.+\.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }

    location ~* \.(js|css|png|jpg|jpeg|gif|ico)$ {
        expires max;
        log_not_found off;
    }
}
```

Sau khi cấu hình thành công, ta sẽ tạo một symbolic link liên kết đến folder /etc/nginx/sites-enabled, và cần phải kiểm tra xem cấu hình có thành công hay không thông qua lệnh nginx -t và cuối cùng là chạy lênh nginx reload để apply lại cấu hình
```bash
sudo ln -s /etc/nginx/sites-available/wordpress.caotienminh.software /etc/nginx/sites-enabled/
sudo nginx -t
sudo nginx -s reload
```

##### 2.6. Cấu hình HTTPS với Certbot

Tải snap
```bash
sudo apt install snapd -y
```

Tải cerbot
```bash
sudo snap install --classic certbot
sudo ln -s /snap/bin/certbot /usr/bin/certbot
sudo certbot –nginx
```

Tạo shortcut (symbolic link) cho certbot
```bash
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```

Chạy lệnh phía dưới, nhập tên email và các tên miền mà ta muốn xác thực ssl, và certbot sẽ tự động cấu hình lại nginx và cấp ssl certificate miễn phí để xác thực https cho web server
```bash
sudo certbot –nginx
```

#### 3. Kết quả
![LEMP Result](lemp-result.png)

---

### II. Triển khai LAMP stack chạy Laravel

#### 1. Link kết quả deploy
[https://laravel.caotienminh.software](https://laravel.caotienminh.software)

#### 2. Từng bước cấu hình

##### 2.1. Tải Apache2
```bash
sudo apt update
sudo apt install apache2
sudo systemctl enable apache2
sudo systemctl start apache2
```

##### 2.2. Tải MySQL và tạo DB
```bash
sudo apt install mysql-server -y
mysql -u root -p
```

```sql
CREATE DATABASE travellist;
CREATE USER 'travellist_user'@'%' IDENTIFIED WITH mysql_native_password BY 'password';
GRANT ALL ON travellist.* TO 'travellist_user'@'%';
EXIT;
```

Tạo bảng dữ liệu test:
```sql
CREATE TABLE travellist.places (
	id INT AUTO_INCREMENT,
	name VARCHAR(255),
	visited BOOLEAN,
	PRIMARY KEY(id)
);

INSERT INTO travellist.places (name, visited) 
VALUES ("Tokyo", false),
("Budapest", true),
("Nairobi", false),
("Berlin", true),
("Lisbon", true),
("Denver", false),
("Moscow", false),
("Olso", false),
("Rio", true),
("Cincinnati", false),
("Helsinki", false);
```

##### 2.3. Tải PHP
```bash
sudo apt install php8.1-fpm php8.1-mysql php8.1-curl php8.1-gd php8.1-mbstring php8.1-xml php8.1-xmlrpc php8.1-soap php8.1-intl php8.1-zip -y 
sudo systemctl start php8.1-fpm 
sudo systemctl enable php8.1-fpm
```

##### 2.4. Tải Composer
```bash
sudo apt install php-cli unzip
cd ~
curl -sS https://getcomposer.org/installer -o /tmp/composer-setup.php
HASH=`curl -sS https://composer.github.io/installer.sig`
php -r "if (hash_file('SHA384', '/tmp/composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
sudo php /tmp/composer-setup.php --install-dir=/usr/local/bin --filename=composer
```

Tạo Laravel App:
```bash
composer create-project --prefer-dist laravel/laravel travellist
cd travellist
```

Ta sẽ tiến hành cấu hình Laravel App bằng cách chỉnh sửa file `.env` (db username, password, database …) như sau: 
```
DB_DATABASE=travellist
DB_USERNAME=travellist_user
DB_PASSWORD=password
```

##### 2.5. Cấu hình Apache
```bash
sudo mv ~/travellist /var/www/travellist
sudo chown -R www-data.www-data /var/www/travellist
sudo nano /etc/apache2/sites-available/000-default.conf
```

Paste vào:
```apache
<VirtualHost *:80>
	ServerName laravel.caotienminh.software
	ServerAlias www.laravel.caotienminh.software

	ServerAdmin webmaster@localhost
	DocumentRoot /var/www/travellist/public/

	<Directory /var/www/travellist/public/>
		AllowOverride All
		Require all granted
	</Directory>

	ErrorLog ${APACHE_LOG_DIR}/error.log
	CustomLog ${APACHE_LOG_DIR}/access.log combined

	RewriteEngine on
	RewriteCond %{SERVER_NAME} =laravel.caotienminh.software [OR]
	RewriteCond %{SERVER_NAME} =www.laravel.caotienminh.software
	RewriteRule ^ https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]
</VirtualHost>
```

```bash
sudo service apache2 reload
```

##### 2.6. Cấu hình HTTPS với Certbot
```bash
sudo apt install snapd -y
sudo snap install --classic certbot
sudo ln -s /snap/bin/certbot /usr/bin/certbot
sudo certbot --apache
```

#### 3. Kết quả
![LAMP Result](lamp-result.png)
