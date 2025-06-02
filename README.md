# Training Notes

## Mục lục
- [1. Các sản phẩm cơ bản của Vietnix](#1-các-sản-phẩm-cơ-bản-của-vietnix)
  - [a. Hosting](#a-hosting)
  - [b. VPS Hosting](#b-vps-hosting)
  - [c. Domain](#c-domain)
  - [d. DNS - Domain Name System](#d-dns---domain-name-system)
- [2. Control Panels](#2-control-panels)
  - [2.1. cPanel](#21-cpanel)
  - [2.2. WHM](#22-whm)
- [3. Web and Server Control Panels](#3-web-and-server-control-panels)
  - [3.1. Web Panel](#31-web-panel)
  - [3.2. Server Control Panel](#32-server-control-panel)
    - [a. DirectAdmin](#a-directadmin)
    - [b. aaPanel](#b-aapanel)
    - [c. CyberPanel](#c-cyberpanel)
    - [d. VestaCP](#d-vestacp)
- [4. WordPress Hosting](#4-wordpress-hosting)
- [5. iptables](#5-iptables)
- [6. Lab](#6-lab)

## 1. Các sản phẩm cơ bản của Vietnix

### a. Hosting
Cung cấp tài nguyên máy chủ để lưu trữ website.

- **Shared Hosting**: Dùng chung máy chủ.
- **Dedicated Hosting**: Thuê một máy vật lý, toàn quyền kiểm soát.

### b. VPS Hosting
Kết hợp giữa Shared và Dedicated, dùng chung một máy vật lý nhưng được chia nhỏ ra.

- **VPS**: Cung cấp một máy ảo hoạt động như một máy vật lý.

### c. Domain
Hệ thống chuyển đổi tên miền thành địa chỉ IP của máy chủ.

### d. DNS - Domain Name System
Các loại bản ghi DNS:

- **CNAME Record**: Bản ghi tên quy chuẩn (Canonical Name Record), đặt bí danh cho tên miền này bằng một tên miền khác. Ví dụ: A Record cho `vietnix.vn` trỏ đến IP server, sau đó CNAME Record `www.vietnix.vn` trỏ đến `vietnix.vn`.
- **A Record**: Trỏ tên miền website tới một địa chỉ IP cụ thể.
- **MX Record**: Trỏ tên miền đến mail server.
- **AAAA Record**: Trỏ tên miền đến địa chỉ IPv6, kèm TTL và IPv6.
- **TTL**: Time to Live, thời gian một đối tượng được lưu trữ trong bộ nhớ đệm trước khi bị xóa hoặc làm mới. Trong CDN, TTL liên quan đến bộ nhớ đệm nội dung, lưu trữ bản sao tài nguyên trang web trên proxy CDN để cải thiện tốc độ tải trang và giảm tiêu thụ băng thông của server gốc.
- **TXT Record**: Chứa các thông tin định dạng văn bản cho domain, có thể thêm giá trị TXT, Host mới, TTL và Point To.
- **SRV Record**: Xác định dịch vụ chạy trên port nào, thêm Priority, Port, Weight, TTL, Point to Point.
- **NS Record**: Chỉ định Name Server cho từng tên miền phụ, tạo Name Server, TTL hoặc host mới.

**Loại NS**:
- **Root Name Server**: Dịch vụ phân giải tên miền gốc, khoảng 12 DNS root server trên thế giới, quản lý tất cả tên miền cấp cao (Top-level). Khi có yêu cầu phân giải tên miền thành địa chỉ IP, client gửi yêu cầu đến DNS gần nhất (DNS ISP), sau đó kết nối tới DNS root server để hỏi địa chỉ của Domain Name.
- **Local Name Server**: Chứa thông tin để truy xuất và tìm kiếm máy chủ tên miền.
- **DNS Recursor**: Chuyển đổi tên miền thành địa chỉ IP. Nếu không tìm thấy thông tin trong cơ sở dữ liệu, nó liên hệ với các DNS Recursor khác và sử dụng bộ nhớ đệm để lưu trữ thông tin đã truy cập.
- **TLD Name Server (Top Level Domain)**: Lưu trữ thông tin về các tên miền có phần mở rộng chung (gTLD) như `.com`, `.org`, `.net`.
- **Authoritative Name Server**: Lưu trữ thông tin về tên miền và địa chỉ IP tương ứng, là điểm cuối của quá trình truy vấn và phân giải địa chỉ IP.

### Colocation
Doanh nghiệp mua thiết bị (router, server,...) nhưng đặt trong cơ sở của nhà cung cấp dịch vụ.

## 2. Control Panels

### 2.1. cPanel
cPanel là bảng điều khiển lưu trữ web dựa trên Linux, cung cấp giao diện đồ họa thân thiện để quản lý website và tài nguyên máy chủ.

**Tính năng**:

#### Email
- Tạo, xóa, kiểm tra, quản lý email, cấu hình email cho mail client.
- **Forwarders**: Chuyển tiếp email đến một email khác. Ví dụ: forward các email gửi đến `test1@hosting.com` → `tech@vietnix.vn`.
- **Email Routing**: Định tuyến email nhận đến một server cụ thể (phải luôn đặt local mail exchanger).
- **Autoresponders**: Cấu hình trả lời email tự động.
- **Default Address**: Cấu hình Catch-all Email. Thay vì trả về thông báo “No Such User Here” khi email gửi đến địa chỉ không tồn tại, hosting sẽ chuyển email đó đến email mặc định.
- **Mailing Lists**: Gửi email đến `tech@vietnix.vn` sẽ được gửi đồng thời đến tất cả email trong group.
- **Track Delivery**: Theo dõi trạng thái email gửi ra.
- **Global Email Filters**: Lọc email cho toàn bộ tài khoản email trên hosting.
- **Email Filters**: Lọc email cho từng tài khoản email trên hosting.
- **Email Deliverability**: Kiểm tra, lấy cấu hình DKIM, SPF, PTR cho domain email trên hosting.
- **Address Importer**: Import danh sách email account lên hosting bằng file `.csv` (email user, password, disk quota).
- **Spam Filters**: Lọc thư rác.
- **BoxTrapper**: Xác thực người gửi, quản lý Blacklist & Whitelist, xử lý thư rác, quản lý danh sách liên hệ.
- **Email Disk Usage**: Thống kê dung lượng disk của từng email.
- **ASSP Antispam**: Điều chỉnh giá trị spam score từ lowest đến highest, bật/tắt tính năng cho từng domain email, Delaying filter.

#### File
- **File Manager**: Upload, xóa, sửa file, nén, giải nén, hiển thị file ẩn (`.htaccess`, `.env`,...).
- **Images**: Công cụ convert, chỉnh sửa hình ảnh của cPanel.
- **Directory Privacy**: Cài đặt user/pass cho các thư mục trên cPanel, tương tự `htpasswd`.
- **Disk Usage**: Thống kê dung lượng disk đang sử dụng.
- **Web Disk**: Quản lý dữ liệu trên web, hỗ trợ giao thức WebDAV, tương tự Google Drive, OneDrive.
- **FTP Accounts**: Tạo tài khoản FTP, hỗ trợ phân quyền cho thư mục.
- **Backup & Backup Wizard**: Backup của cPanel (không khuyến khích sử dụng).
- **Git Version Control**: Làm việc với GitHub, tự động pull code khi có cập nhật trên repository.
- **JetBackup 5**:
  - **Full Backups**: Sao lưu toàn bộ hosting (database, source, SSL,...).
  - **Home Directory**: Sao lưu file, có thể chọn từng file để khôi phục.
  - **Databases**: Khôi phục database.

#### Database
- **phpMyAdmin**: Đăng nhập bằng tài khoản MySQL.
- **MySQL Databases**: Tạo database, user, cấp quyền.
- **MySQL Database Wizard**: Hỗ trợ tạo database từng bước, đảm bảo không quên các bước như tạo user, thêm user vào database, cấp quyền.
- **Remote MySQL**: Bật remote MySQL cho database.

#### Domain
- **WP Toolkit**: Tải theme, plugin WordPress.
- **Site Publisher**: Tạo nhanh website bằng template có sẵn của cPanel.
- **Domains**: Thêm, xóa domain.
- **Redirects**: Chuyển hướng domain.
- **Zone Editor**: Điều chỉnh các bản ghi DNS sau khi trỏ NS về hosting (NS của hosting có dạng `host212.vietnix.vn`).
- **Dynamic DNS**: CPanel cấp URL để cập nhật NS cho subdomain bằng cách curl đến URL này.
- **IP Manager** (chỉ có trên Hosting SEO): Đổi IP cho các domain.

#### Metrics
- **Visitors**: Access logs, dùng để xác định hosting có đang bị tấn công.
- **Errors**: Apache Error Logs.
- **Bandwidth**: Thống kê traffic từng ngày theo từng domain.
- **Raw Access**: Cho phép tải raw access log. Nếu khách cần log, có thể hướng dẫn vào đây để tải.
- **Resource Usage**: 
  - Server chạy CloudLinux sẽ có mục này, các giá trị cần tìm hiểu:
    - **SPEED**: CPU Hosting.
    - **PMEM**: RAM Hosting.
    - **IO**: I/O Hosting.
    - **EP**: Số lượng kết nối tối đa.
    - **NPROC**: Số lượng tiến trình tối đa.
    - **IOPS**: I/O per second Hosting.

#### Security
- **SSH Access**: SSH lên hosting, hỗ trợ thêm SSH key.
- **IP Blocker**: Chặn IP không cho truy cập vào website.
- **SSL/TLS**: Quản lý SSL server.
- **Manage API Tokens**: Tạo API Key để tương tác với cPanel.
- **Hotlink & Leech Protection**:
  - **Hotlink Protection**: Chặn các website khác chèn direct link hình ảnh, file download từ website của bạn.
  - **Leech Protection**: Liên quan đến Directory Privacy. Nếu user/pass của một thư mục bị lộ và bị truy cập nhiều lần, hệ thống sẽ chặn và redirect đến link khác hoặc thông báo cho admin.
- **SSL/TLS Status**: Cài đặt AutoSSL.
- **Two-Factor Authentication**: Xác thực hai yếu tố.
- **Imunify360**: Quét virus tự động.

#### Software
- **WordPress Manager by Softaculous**: Tạo WordPress tự động, tương tự WP Toolkit.
- **PHP PEAR Packages**: Gói PEAR dùng để chạy trong PHP.
- **Perl Modules**: Mô-đun PERL hỗ trợ tạo các tác vụ PERL.
- **Site Software**: Bổ sung phần mềm như bảng thương mại điện tử, bảng tin.
- **Optimize Website**: Tối ưu thời gian phản hồi của Apache Web Server.
- **Application Manager**: Đăng ký, quản lý, triển khai ứng dụng tùy chỉnh bằng Phusion Passenger.
- **MultiPHP Manager**: Chọn phiên bản PHP khác nhau cho từng website.
- **MultiPHP INI Editor**: Bật/tắt các biến môi trường PHP.
- **Softaculous Apps Installer**: Cài đặt ứng dụng (WordPress, Laravel, Moodle, NextCloud,...) bằng một click.
- **Setup Node.js App**: Cài đặt ứng dụng Node.js.
- **Select PHP Version** (hỗ trợ bởi CloudLinux): Chọn phiên bản PHP khác nhau cho từng website.

#### Advanced
- **LiteSpeed Web Cache Manager**: Hỗ trợ flush cache từ giao diện cPanel nếu khách sử dụng LSCache plugin.
- **Terminal**: Chạy các lệnh terminal.
- **Cron Jobs**: Tự động hóa các nhiệm vụ lặp lại theo lịch, ví dụ: tạo hóa đơn lúc 12:00 hàng ngày.
- **Track DNS**: Kiểm tra tuyến đường từ PC đến máy chủ để kiểm tra cài đặt DNS.
- **Indexes**: Tùy chỉnh trang chỉ mục Apache mặc định.
- **Error Pages**: Cấu hình cách hiển thị trang lỗi khi khách truy cập.
- **Apache Handlers**: Các tùy chọn xử lý của Apache.
- **MIME Types**: Hướng dẫn xử lý các phần mở rộng tệp như `.html`, `.htm`.

### 2.2. WHM
WHM (WebHost Manager) cung cấp quyền kiểm soát quản trị cho máy chủ chuyên dụng hoặc VPS, cho phép nhà cung cấp hosting quản lý tài khoản khách hàng. WHM cũng là bảng điều khiển cho reseller, nhưng quyền reseller bị giới hạn so với quyền root trên VPS/Dedicated Server.

**Tính năng**:
- **Primary Domain**: Quản lý domain chính.
- **Migrate và Transfer**: Sử dụng Transfer Tool để migrate từ server cũ, điền IP của server cũ vào ô Remote Server Address.

**So sánh**:
- cPanel: Quản lý một website (dành cho người không chuyên).
- WHM: Quản lý nhiều website, tạo tài khoản cPanel, quản lý toàn bộ server.

## 3. Web and Server Control Panels

### 3.1. Web Panel
**Kết luận**: Dịch vụ hosting web là dịch vụ mà nhiều máy chủ của nhà cung cấp đóng vai trò host, cho phép người dùng lưu trữ website trên đó. Người dùng quản lý hosting qua cPanel, trong khi nhà cung cấp (reseller) quản lý tất cả hosting bằng WHM.

### 3.2. Server Control Panel

#### a. DirectAdmin
Bảng điều khiển quản trị Web Hosting phổ biến với giao diện đơn giản, trực quan, dễ sử dụng, đặc biệt cho người ít kinh nghiệm.

**Tính năng**:
- Quản lý domain, subdomain, DNS, FTP, cơ sở dữ liệu MySQL.
- Chạy tốt trên Linux và các bản phân phối như CloudLinux, CentOS, Ubuntu, Debian, Red Hat.

**Ưu điểm**:
- Giao diện trực quan, dễ sử dụng.
- Giá cả phải chăng.
- Hỗ trợ từ nhà cung cấp và kỹ thuật viên DirectAdmin qua hệ thống ticket (gói Lite, Standard).
- Ổn định, tự động phục hồi sự cố.
- Xử lý nhanh, ít tiêu tốn tài nguyên.
- Hỗ trợ nhiều phân cấp user, cấu hình thủ công.

**Nhược điểm**:
- Khả năng thêm chức năng hạn chế.
- Không hỗ trợ font Unicode (ngôn ngữ không phải tiếng Anh).
- Cộng đồng người dùng nhỏ.
- Giao diện khá phức tạp với người mới.

#### b. aaPanel
Bảng điều khiển miễn phí, quản lý server với giao diện GUI đơn giản, chạy mô hình LEMP/LAMP (Linux, NGINX/Apache, MySQL, PHP). Là phiên bản quốc tế của BAOTA Panel.

**Chức năng**:
- Quản lý web, database, FTP, file.

**Ưu điểm**:
- Nhẹ (512MB RAM).
- Cài đặt và sử dụng dễ dàng.
- Chỉnh sửa cấu hình PHP, Webserver nhanh chóng qua giao diện.
- Cài đặt Redis, Memcached, Google Drive,... bằng một click.
- File Manager thân thiện, hỗ trợ code editor đơn giản.
- Backup lên Google Drive, FTP, Amazon S3.
- Cộng đồng người dùng tương đối lớn.

**Nhược điểm**:
- Cấu hình MySQL/MariaDB mặc định cao, dễ gây lỗi tự tắt.
- Không hỗ trợ phân quyền người dùng, chỉ truy cập bằng một tài khoản duy nhất.
- Phù hợp với VPS cấu hình thấp, không phù hợp cho cấu hình cao.

#### c. CyberPanel
Miễn phí, hỗ trợ Tiếng Việt, sử dụng OpenLiteSpeed làm webserver.

#### d. VestaCP
Bảng điều khiển mã nguồn mở miễn phí, dễ cài đặt và cấu hình trên Linux.

**Khi nào nên dùng VestaCP**:
- Dịch vụ web và mã nguồn PHP, MySQL.
- Dịch vụ email (mail server, webmail).
- Dịch vụ DNS.
- Sao lưu tự động/thủ công, khôi phục dữ liệu.
- Cấu hình firewall.
- Dịch vụ FTP để upload/download.
- Phân bổ, chia sẻ dữ liệu/tài nguyên, phân quyền người dùng.

## 4. WordPress Hosting
Hệ thống quản lý nội dung (CMS) mã nguồn mở, giúp tạo và quản lý website mà không cần kiến thức code.

**Vấn đề**:
- Website chậm, điểm PageSpeed thấp.
  - **Giải pháp**: Sử dụng LiteSpeed Cache, CDN, SEO (Rank Math), tối ưu hình ảnh, HTML, CSS, JS.

**Quá nhiều plugin**:
- Gây xung đột, giảm hiệu suất và bảo mật.
- **Giải pháp**: Gỡ plugin không cần thiết, cập nhật plugin thường xuyên, kiểm tra tương thích.

## 5. iptables

## 6. Lab

### 6.1. Nội dung cần nắm trước khi làm bài Lab

#### 1. Reverse Proxy
![Reverse Proxy Flow](reverse-proxy-flow.png)

Reverse Proxy bản chất là một server tiếp nhận request từ phía Clients, và sau đó nó sẽ điều hướng các requests đến cho phía web server.
Việc dựng một Reverse Proxy giúp giấu đi địa chỉ IP thực của phía web server, tránh được việc các hacker DDOS đến web server dẫn đến tình trạng quá tải. Ngoài ra ta cũng có thể cấu hình Reverse Proxy load balancing các request đến web server sao cho đảm bảo tài nguyên các từng web server đều được tận dụng ở mức tối ưu nhất.

#### 2. Phân biệt giữa static và dynamic website

##### 2.1 Static Website
Static Website là website tĩnh, nội dung không thay đổi theo thời gian thực. Khi Clients truy cập đến website thì phía web server sẽ trả về các file tĩnh như HTML, CSS, Javascript cho phía Client. Vì các file này là file tĩnh nên phía server không cần phải thực hiện các tác vụ xử lý và nó cũng không cần phải tương tác với database → do đó tốc độ truy cập sẽ nhanh hơn so với Dynamic Website.

Một vài ví dụ về Static Website như: Portfolio Page, Landing Pages, ...

##### 2.2 Dynamic Website
Dynamic Website là website động, nội dung thay đổi theo thời gian thực. Website sẽ có backend để xử lý request đến từ Clients (có thể thêm/xóa/sửa/lấy data từ phía database) và trả kết quả về cho người dùng. Vì phía server phải thực hiện các tác vụ để xử lý request nên tốc độ sẽ chậm hơn Static Website. Nhưng đổi lại thì người dùng có thể tương tác, nhận kết quả từ phía web server.

Một vài ví dụ về Dynamic Website như: Ecommerce Website, ...

#### 3. LAMP/LEMP stack là gì?

##### 3.1. LAMP stack
LAMP stack bao gồm Linux, Apache, MySQL, PHP. Trong đó ta sẽ triển khai Apache như một web server. PHP dùng để dựng nên phía backend và giao tiếp với Database là MySQL để thêm/xóa/cập nhật dữ liệu.

##### 3.2. LEMP stack
LEMP cũng tương tự như LAMP nhưng thay vì dùng Apache làm Web Server thì ta sẽ dùng Nginx. Nginx sẽ phù hợp với các trường hợp host static web, nhanh và nhẹ hơn so với Apache. Ngược lại thì Apache sẽ phù hợp với việc host web động và nó có thể cấu hình nhiều tính năng hơn so với Nginx.

##### 3.3. Trường hợp sử dụng

**Apache** sử dụng cấu trúc processed-based, nghĩa là mỗi yêu cầu sẽ được nó tạo một tiến trình (process) riêng để xử lý cho từng requests. Về lợi thì sẽ giúp các requests được xử lý riêng biệt → ổn định. Về vấn đề phát sinh đó chính là trường hợp cao điểm có nhiều requests đến server thì sẽ dẫn đến tình trạng bị quá tải, vì càng nhiều requests thì càng nhiều process được tạo ra → tốn CPU và Memory

**Nginx** sử dụng kiến trúc event-driven và đơn luồng. Nghĩa là nó chỉ sử dụng một thread duy nhất để nhận các request từ phía Clients và đưa vào hàng đợi để xử lý các events. Vì chỉ sử dụng một luồng và chỉ việc đưa các request đến cho hàng đợi events xử lý. Các requests sẽ được phân chia thành events khác nhau để xử lý. Ví dụ đối với Apache thì nếu nhận N requests thì nó sẽ tạo ra N process để xử lý. Còn đối với Nginx thì đối các N requests đó thì nó sẽ tạo ra các events chung để xử lý đối với từng requests 

→ Nếu Nginx dùng để host static web thì nó chỉ events là gửi các static file về cho người dùng mà không cần phải gửi requests đến để chờ phía backend xử lý.

→ Còn Apache sẽ ổn định hơn khi hosting dynamic web vì nó tạo từng process riêng để xử lý cho từng requests, giúp cô lập trong trường hợp xảy ra lỗi.

##### 3.4. Một trang web có thể vừa static vừa dynamic không ?
Một trang web có thể vừa static và dynamic. Đối với phía Frontend, ta sẽ dùng các static file như HTML, CSS, Javascripts hoặc ReactJS, VueJS,... Khi Clients tương tác với phía Frontend thì nó sẽ gửi requests đến phía Backend (PHP, Nodejs, Java,...) để xử lý và trả về kết quả cho phía Frontend để hiển thị cho người dùng

**Dựa vào những ưu điểm của từng webserver đã nêu trên, ta có thể tận dụng để tối ưu đối với trường hợp website vừa static vừa dynamic như sau:**

→ Vì nginx phù hợp cho việc xử nhiều kết nối đồng thời đối với những static files, nên ta sẽ dùng nó để host Frontend Server, nhập các requests từ người dùng. Đối với trường hợp web browser của Clients truy cập vào website để tải về các static files (html,css, javascripts, images, videos, ...) có sẵn ở server Frontend, thì Nginx sẽ trả về cho phía Clients mà không cần gửi requests đến phía Backend Server là Apache → giúp Apache không bị quá tải/tốn CPU, RAM để xử lý.

→ Ở phía Backend Server ta sẽ host bằng Apache. Trường hợp người dùng cần tải các file động (PHP scripts,...) thì Nginx sẽ hoạt động như 1 reverse proxy gửi requests đến cho phía Apache để xử lý và trả kết quả lại cho Clients.

### 6.2. Từng bước cấu hình

**OS Template sử dụng:** `Ubuntu-Server-22.04-x64`

---

##### Workflow của bài lab
![WORK-FLOW](work-flow.png)

##### MySQL setup

```sql
CREATE DATABASE wordpress_db;  
CREATE USER 'wordpress_user'@'localhost' IDENTIFIED BY 'secure_password';  
GRANT ALL PRIVILEGES ON wordpress_db.* TO 'wordpress_user'@'localhost';  
CREATE DATABASE laravel_db;  
CREATE USER 'laravel_user'@'localhost' IDENTIFIED BY 'secure_password';  
GRANT ALL PRIVILEGES ON laravel_db.* TO 'laravel_user'@'localhost';  
FLUSH PRIVILEGES;  
EXIT;
```

##### Laravel  
```bash
composer create-project laravel/laravel /var/www/laravel  
sudo chown -R www-data:www-data /var/www/laravel  
sudo chmod -R 755 /var/www/laravel  
sudo chmod -R 775 /var/www/laravel/storage  
sudo chmod -R 775 /var/www/laravel/bootstrap/cache  
cd /var/www/laravel  
cp .env.example .env  
vi .env  
```

##### Dán nội dung sau vào trong file .env
```
DB_CONNECTION=mysql  
DB_HOST=127.0.0.1  
DB_PORT=3306  
DB_DATABASE=laravel_db  
DB_USERNAME=laravel_user  
DB_PASSWORD=secure_password  
```

```bash
php artisan key:generate  
```

##### Config apache2
```bash
sudo vi /etc/apache2/ports.conf  
sudo vi /etc/apache2/sites-available/laravel.conf   
```

##### Dán vào file cấu hình của laravel
```apache
<VirtualHost *:8080>  
    ServerName laravel.caotienminh.software  
    ServerAlias www.laravel.caotienminh.software  
    DocumentRoot /var/www/laravel/public  

    <Directory /var/www/laravel/public>  
        AllowOverride All  
        Require all granted  
    </Directory>  

    <FilesMatch \.php$>  
        SetHandler "proxy:unix:/var/run/php/php8.1-fpm.sock|fcgi://localhost/"  
    </FilesMatch>  
</VirtualHost>  
```

##### Chạy lệnh sau  
```bash
sudo a2enmod proxy proxy_fcgi  
sudo a2ensite laravel  
sudo systemctl restart apache2
```

##### Wordpress Setup
```bash
wget https://wordpress.org/latest.zip  
unzip latest.zip -d /var/www/  
sudo mv /var/www/wordpress /var/www/wordpress_site  

sudo chown -R www-data:www-data /var/www/wordpress_site  
sudo chmod -R 755 /var/www/wordpress_site
```

##### Cấu hình Nginx cho Wordpress
```bash
vi /etc/nginx/sites-available/wordpress.conf
```

```nginx
server {  
    listen 80;  
    server_name wordpress.caotienminh.software www.wordpress.caotienminh.software;  
    root /var/www/wordpress_site;  
    index index.php index.html index.htm;  

    location / {  
        try_files $uri $uri/ /index.php?$args;  
    }  

    location ~ \.php$ {  
        include snippets/fastcgi-php.conf;  
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;  
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;  
        include fastcgi_params;  
    }  
}  

```

##### Tạo symbolic link  
```bash
sudo ln -s /etc/nginx/sites-available/wordpress.conf /etc/nginx/sites-enabled/  
sudo nginx -t  
sudo systemctl restart nginx
```  

##### Tải mysqli
```bash
sudo apt install php-mysql
```

##### Cấu hình routes API cho laravel  
```bash
cd /var/www/laravel  
vi routes/api.php
```

##### Dán vào file api.php  
```php
<?php  

use Illuminate\Http\Request;  
use Illuminate\Support\Facades\Route;  

Route::get('/posts', function () {  
    return response()->json([  
        'posts' => [  
            ['id' => 1, 'title' => 'First Post', 'content' => 'This is the first API post.'],  
            ['id' => 2, 'title' => 'Second Post', 'content' => 'This is the second API post.'],  
        ]  
    ]);  
});  
```

##### Chạy lệnh sau để áp dụng cấu hình cho apache2
```bash
sudo a2enmod rewrite  
systemctl restart apache2
```

##### Kiểm tra thử prefix http://laravel.caotienminh.software:8080/api/posts  
![LARAVEL API](laravel-api.png)

##### Tạo page Frontend trên Wordpress

###### Tạo plugin để curl data từ url http://laravel.caotienminh.software:8080/api/posts  
```bash
mkdir /var/www/wordpress_site/wp-content/plugins/laravel-api  
cd /var/www/wordpress_site/wp-content/plugins/laravel-api  
vi laravel-api.php
```

###### Dán vào file laravel-api.php
```php
<?php  
/*  
Plugin Name: Laravel API Integration  
Description: Fetches posts from a Laravel API and displays them in WordPress.  
Version: 1.0  
Author: Your Name  
*/  

// Shortcode to display Laravel API posts  
function laravel_api_posts_shortcode() {  
    $response = wp_remote_get('http://laravel.caotienminh.software/api/posts');  
    if (is_wp_error($response)) {  
        return '<p>Error fetching posts: ' . $response->get_error_message() . '</p>';  
    }  

    $body = wp_remote_retrieve_body($response);  
    $data = json_decode($body, true);  

    if (empty($data['posts'])) {  
        return '<p>No posts found.</p>';  
    }  

    $output = '<ul>';  
    foreach ($data['posts'] as $post) {  
        $output .= '<li><strong>' . esc_html($post['title']) . '</strong>: ' . esc_html($post['content']) . '</li>';  
    }  
    $output .= '</ul>';  

    return $output;  
}  
add_shortcode('laravel_posts', 'laravel_api_posts_shortcode');  
?>
```

###### Activate plugin  
Vào wordpress /wp-admin đeer activate plugin vừa tạo xong  
![ACTIVATE PLUGIN](activate-plugin.png)

###### Tạo page với template như sau
![WORDPRESS PAGE](wordpress-page.png)

###### Kết quả sau khi tạo thành công
![LAB FINAL RESULTS](lab-final-results.png)

###### Cấu hình HTTPS cho frontend (https://wordpress.caotienminh.software) 
sudo certbot --nginx

##### Cấu hình chặn truy cập trực tiếp đến http://laravel.caotienminh.software
--> Tạo 1 iptables mà nó sẽ rejects tất cả requests đến port 8080 (port của backend) ngoại trừ requests đến từ ip address của chính nó  
sudo iptables -I INPUT -p tcp --dport 8080 ! -s  14.225.212.151 -j REJECT --reject-with tcp-reset  
