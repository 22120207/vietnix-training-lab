# Training Notes

## 1. Các sản phẩm cơ bản của Vietnix
### a. Hosting -> cung cap tnguyen may chu de luu tru website
Shared Hosting -> Dung chung may chu
Dedicated Hosting -> thue 1 may vly , toan quyen kiem soat
### b. VPS Hosting --> Shared + Dedicated, dung chung 1 may vly nhung duoc chia nho ra
VPS --> Cung cap 1 may ao hoat dong nhu 1 may vly
### c. Domain
DNS --> hệ thống chuyển đổi tên miền thành địa chỉ IP của máy chủ.
### d. DNS - Domain Name System
DNS Record
    + CNAME Record: Là một bản ghi tên quy chuẩn (Canonical Name Record). Đây là một dạng bản ghi tài nguyên trong hệ thống tên miền.
      được dùng để đặt bí danh cho tên domain này bằng một cái tên miền khác. Vi du A record cho vietnix.vn -> IP server. Sau do CNAME Record www.vietnix.vn -> vietnix.vn
    + A Record: Dùng để trỏ tên miền website tới một địa chỉ IP cụ thể.
    + MX Record: Bản ghi này bạn có thể sử dụng để trỏ tên miền đến mail server.
    + AAAA Record: Dùng để trỏ tên miền đến địa chỉ IPv6, TTL và IPv6.
--> TTL: Time to live (TTL) là thời gian một đối tượng được lưu trữ trong hệ thống bộ nhớ đệm trước khi nó bị xóa hoặc làm mới. Trong trường hợp của CDN, Time to live thường đề cập đến bộ nhớ đệm nội dung, là quá trình lưu trữ bản sao tài nguyên trang web của bạn trên proxy CDN để cải thiện tốc độ tải trang và giảm tiêu thụ băng thông của server gốc.
    + TXT Record: Ngoài ra, có thể thêm giá trị TXT, Host mới, TTL và Point To để chứa các thông tin định dạng văn bản domain.
    + SRV Record: Đây là bản ghi DNS đặc biệt, dùng để xác định chính xác dịch vụ nào đang chạy Port nào. Và thông qua bản ghi này bạn có thể thêm Priority, Port, Weight, TTL, Point to Point.
    + NS Record: Bản ghi này có thể chỉ định Name Server cho từng tên miền phụ và bên cạnh đó có thể tạo tên Name Server, TTL hay host mới.
Loai NS:
    + Root Name Server: một dịch vụ phân giải tên miền gốc và trên thế giới có khoảng 12 DNS root Server. Quản lý tất cả các tên miền Top-level. Khi có yêu cầu phân giải một Domain Name thành một địa chỉ IP, client sẽ gửi yêu cầu đến DNS gần nhất (DNS ISP). DNS ISP sẽ kết nối tới DNS root Server để hỏi địa chỉ của Domain Name.
    + Local Name Server: ùng để chứa thông tin để truy xuất và tìm kiếm máy chủ tên miền
    + DNS Recursor: có nhiệm vụ chuyển đổi tên miền thành địa chỉ IP.
    + DNS Recursor: khi người dùng nhập một tên miền, DNS Recursor sẽ tìm kiếm thông tin đó trong cơ sở dữ liệu của mình. Nếu không tìm thấy, nó sẽ liên hệ với các DNS Recursor khác để tìm kiếm. DNS Recursor cũng sử dụng bộ nhớ đệm để lưu trữ thông tin về các tên miền mà nó đã từng truy cập.
    + TLD Name Server (Top Level Domain): máy chủ tên miền cấp cao nhất, chịu trách nhiệm lưu trữ thông tin về các tên miền có phần mở rộng chung (gTLD), chẳng hạn như .com, .org, .net
    + Authoritative Name Server: lưu trữ thông tin về tên miền và địa chỉ IP tương ứng. Là điểm cuối của quá trình truy vấn và phân giải địa chỉ IP cần thiết cho DNS Recursor.
SLides of 1:
Colocation: DOanh nghiep mua tbi, router,... nhung dat trong co so cua nha cung cap dich vu

## 2.1. Cpanel
--> cPanel is a widely used, Linux-based web hosting control panel that provides a user-friendly graphical interface for managing websites and server resources
TInh nang:
- Email: 
    + Tạo email, xóa email, kiểm tra email, quản lý email, cấu hình email cho mail client.
    + Forwarders: forward Email đến 1 email khác. Ví dụ forward các email gửi đến test1@hosting.com (email trên hosting) → tech@vietnix.vn
    + Email Routing: route mail nhan -> 1 server cu the (phai luon set local mail exchange)
    + Autoresponders: Cấu hình trả lời Email tự động.
    + Default Address: Nơi cấu hình Catch-all Email. Explain: Thay vì khi nhận Hosting nhận được một email đến 1 địa chỉ không tồn tại trên hosting thì nó sẽ trả về cho người gửi thông báo “No Such User Here“, thì khi cấu hình Default Address Hosting sẽ gửi các email đó đến email default.
    + Mailling Lists: Chức năng của Mailling List là khi có một email gửi tới tech@vietnix.vn thì sẽ được gửi đồng thời đến tất cả email trong group.
    + Track Delivery: Theo dõi trạng thái của email gửi ra.
    + Global Email Filters: Filter email với toàn bộ email account trên Hosting
    + Email Filters: Filter email với từng email account trên Hosting
    + Email Deliverablity: Kiểm tra, lấy cấu hình DKIM, SPF, PTR đối với domain email trên Hosting
    + Address Importer: Import danh sách email account lên Hosting. Bạn có thể tạo nhanh 1 list email trên hosting bằng cách tạo 1 file .csv, Với email user, password, disk quota
    + Spam Filters
    + BoxTrapper: Xác thực người gửi, Blacklist & Whitelist, Xử lý thư rác, Quản lý danh sách liên hệ
    + Email Disk Usage Thống kê disk của từng email
    + ASSP Antispam: Diều chỉnh giá trị spam score, từ lowest → highest. Hoặc bật tắt tính năng này cho từng domain email. Delaying filter
- File:
    + File Manager: Upload file, xóa, sửa file, nén, giải nén. Ngoài ra để hiển thị file ẩn (.htaccess, .env…)
    + Images: Công cụ convert, edit hình ảnh của cPanel
    + Directory Privacy: Cài đặt user/pass cho các thư mục trên cPanel → Tương tự htpasswd
    + Disk Usage: Thống lê disk đang sử dụng
    + Web Disk: Quản lý dữ liệu trên web, tương tự như google drive, onedrive. Web disk hỗ trợ giao thức webdav để truyền tải.
    + FTP Accounts: Tạo tài khoản ftp account, hỗ trợ phân quyền tài khoản cho thư mục
    + Backup & Backup Wizard: Backup của cPanel → Không sử dụng
    + Git Version Control: Làm việc với github, tự động pull code khi có update code mới trên repo
    + JetBackup 5:
        --> Full backups: Ðây là các bản backup full, khi restore lại sẽ restore toàn bộ hosting, bao gồm database, source, ssl,…
        --> Home Directory: Ðây là backup file, có thể lựa chọn riêng từng file để restore
        --> Databases: Restore database
- Database:
    + phpMyAdmin: tk login la tk MySQL
    + MySQL Databases: tao db, user, grant quyen
    + MySQL Database Wizard: Hỗ trợ tạo Database step-by-step. Giúp người tạo không bị quên các bước như tạo user, add user vào database, grant quyền
    + Remote MySQL Bật remote Mysql đối với database
- Domain:
    + WP Toolkit: tai theme wordpress, plugin
    + Site Publisher: Tạo nhanh 1 website bằng template có sẵn của cPanel
    + Domains: Thêm, xóa domain
    + Redirects: Redirect domain
    + Zone Editor: Sau khi trỏ NS về Hosting thì có thể điều chỉnh các record ở đây. NS của hosting có dạng, ví dụ host212.vietnix.vn
    + Dynamic DNS: Sau khi tạo cPanel sẽ cấp cho mình 1 Url. Khi muốn cập nhật NS cho subdomain này thì chỉ cần curl đến URL này.
    + IP Manager (chỉ có trên Hosting SEO): Dùng để đổi IP cho các domain
- Metrics: 
    + Visitors: Access-logs. Có thể dùng để xác định hosting đang bị đánh.
    + Errors: Apache Error Logs
    + Bandwidth: Thống kê traffic từng ngày theo từng domain.
    + Raw Access: Cho phép download raw access log. Nếu khách cần log có thể nói khách vào đây để download.
    + Resource Usage: 
        --> Server chạy cloudlinux sẽ có mục này, các giá trị cần tìm hiểu:
            . SPEED: CPU Hosting
            . PMEM: Ram Hosting
            . IO: I/O Hosting
            . EP: Số lượng connect tối đa
            . NPROC: Số lượng Process tối đa
            . IOPS: I/O per second Hosting
- Security:
    + SSH Access: SSH lên hosting, có thể cho phép add ssh key
    + IP Blocker: Block ip không cho truy cập vào website của bạn
    + SSL/TLS: Quản lý SSL Server
    + Manage API Tokens: Tạo API Key để tương tác với cPanel
    + Hotlink & Leech Protection: Hotlink Protection: Giúp chặn các website khác chèn các directlink hình ảnh, file download của mình trên website của họ.
    + Leech Protection: Tính này liên quan đến phần Directory Privacy ở trên. Ví dụ sau khi tạo user/pass được phép truy cập vào 1 folder nào đó trên hosting. Mà user đó bị lộ pass và bị truy cập nhiều lần vào folder đó thì sẽ bị chặn và redirect đến 1 link khác hoặc thông báo cho admin.
    + SSL/TLS Status: Cài đặt AutoSSL
    + Two-Factor Authentication
    + Imunify360: Quét virus, quá trình quét virus là tự động
- Software
    + Wordpress Manager by Softaculous: Tạo wordpress tự động, tương tự như Wordpress Toolkit
    + PHP PEAR Packages: Gói PEAR thường dùng để chạy trong PHP.
    + Perl Modules: mô-đun PERL được tạo nhằm giúp bạn có thể tạo các tác vụ PERL.
    + Site Software: Với phần mềm bổ sung thêm như Bảng thương mại điện tử và Bảng tin.
    + Optimize Website: Web Server Apache sẽ tối ưu thời gian phản hồi.
    + Application Manager: Tính năng này cho phép bạn đăng ký, quản lý và triển khai các ứng dụng tùy chỉnh của mình bằng Phusion Passenger.
    + MultiPHP Manager (hỗ trợ bởi cPanel): Có thể tùy chọn các phiên bản PHP khác nhau cho từng website.
    + MultiPHP INI Editor (hỗ trợ bởi cPanel): Bật tắt các biến môi trường php ở đây.
    + Softaculous Apps Installer: Cài đặt app bằng 1 click. Ví dụ: Wordpress, Laravel, Moodle, NextCloud,…
    + Setup Node.js APP: Cài đặt nodeJS App
    + Select PHP Version (hỗ trợ bởi cloudlinux): Có thể tùy chọn các phiên bản PHP khác nhau cho từng website.
- Advanced
    + LiteSpeed Web Cache Manager: Nếu khách có dùng LSCache plugin thì mình có thể hỗ
    + trợ khách flush cache từ giao diện cPanel.
    + Terminal: được dùng để chạy các lệnh terminal.
    + Cron Jobs: Các nhiệm vụ lặp đi lặp lại được tự động hóa vào thời gian đã lên lịch. chẳng hạn như: tạo hóa đơn vào 12:00 hàng ngày.
    + Track DNS: Truy tìm tuyến đường từ PC đến máy chủ nhằm kiểm tra cài đặt DNS.
    + Indexes: Nhằm tùy chỉnh trang chỉ mục Apache mặc định.
    + Error Pages: Giúp định cấu hình cách của các trang lỗi xuất hiện cho khách khi truy cập.
    + Apache Handlers: Ðây là các lựa chọn xử lý của Apache.
    + MIME Types: Dùng để hướng dẫn để xử lý với các phần mở rộng tệp khác nhau, chẳng hạn như: .html, .htm.

## 2.2. WHM
-->  WHM (WebHost Manager) provides administrative control over your dedicated server or VPS. It allows a hosting provider to manage a customer’s account. WHM is also a reseller control panel. It is what our customers receive with all Reseller hosting plans and use to manage all their resold hosting accounts in their reseller plans. However, a reseller has restricted reseller rights in WHM comparing to VPS and Dedicated Servers WHM (root user rights), so some functions are not available for them:.

--> cPanel manage a website (for people who is non-tech). --> WHM: managed multiple website, create cPanel account. WHM is for entirn Server 

TInh nang:
    + Primary Domain
    + Migrate và Transfer: Từ server cần migrate đến, vào Transfer Tool → Ðiền IP của server cũ vào ô Remote Server Address

## 3.1. Web Panel

--> My thought: "FIrst, hosting web service is a service that multiple server of producer act as a host and allow user to host their websites on it, user can control their host with cPanel. ANd the producer controll all web hosting with WHM"

## 3.2. Server COntrol Panel
### a. Direct Admin: --> co phi
    + một trong số những Bảng điều khiển (Control Panel) dành cho người quản trị Web Hosting được sử dụng phổ biến hiện nay với giao diện đơn giản, trực quan, dễ dàng sử dụng. DirectAdmin được thiết kế để dễ dàng thực hiện các công việc hàng ngày của webmaster, đặc biệt là những người có ít hoặc không có kinh nghiệm trước đó.
    + domain, subdomain, DNS, FTP và cơ sở dữ liệu MySQL
    + chạy rất tốt trong Linux và các bản phân phối chính của nó – CloudLinux, CentOS, Ubuntu, Debian, Red Had
--> Ưu điểm: Giao diện trực quan, sử dụng đơn giản, Gói đăng ký giá cả phải chăng. 
    Hỗ trợ: Ngoài sự hỗ trợ của nhà cung cấp dịch vụ lưu trữ, bạn cũng có thể nhận được sự hỗ trợ trực tiếp từ các kỹ thuật viên của DirectAdmin. Người dùng trên gói Lite và Standard có thể   được hưởng lợi từ hệ thống ticket bên trong bảng điều khiển.
    Tính ổn định, phục hồi sự cố tự động. 
    Tốc độ xử lý nhanh, ít tiêu tốn tài nguyên:
    Hỗ trợ nhiều phân cấp user, Manual configuration
--> Nhược điểm: Khả năng thêm các chức năng rất hạn chế.
    Khả năng chỉnh sửa file: DirectAdmin không tương thích với dòng font unicode (khong tuong thich voi ngon ngu k la tieng anh)
    Cộng đồng người dùng ít
    Giao diện khá nâng cao với người dùng
### b. aaPanel:
--> control panel miễn phí, cho phép người dùng quản lý server với giao diện GUI đơn giản. DE chay mo hinh LEMP/LAMP (Linux, NGINX/APache, MySQL, Php)
--> Ban QUoc te cua BAOTA Panel 

- Chức năng
    + một số chức năng cơ bản nhất như: quản lý web, Database, FTP và File
- Ưu nhược điểm:
    - Ưu điểm:
        + nhe (512MB RAM)
        + Người dùng có thể cài đặt aaPanel và sử dụng dễ dàng chỉ bằng một vài thao tác chuột đơn giản.
        + cho phép bạn can thiệp, chỉnh sửa cấu hình PHP hay Webserver trực tiếp trên giao diện một cách nhanh chóng
        + có thể cài đặt Redis, Memcached, Google Drive,… chỉ bằng một lần click chuột
        + quản lý tập tin thông qua File Manager với giao diện thân thiện, đẹp mắt, hỗ trợ code editor đơn giản, tiện lợi
        + backup web lên trên Google Drive, FTP, Amazon S3
        + có cộng đồng người dùng tương đối nhiều
    - Nhược điểm:
        + Cấu hình thiết lập sẵn cho MySQL/MariaDB hơi cao nên thường xuyên xảy ra tình trạng MySQL tự tắt mà không thể khởi động lại được
        + chưa hỗ trợ tính năng phân quyền người dùng, bạn chỉ có thể truy cập vào bảng điều khiển thông qua 1 tài khoản duy nhất
        + chỉ phù hợp với những VPS có cấu hình thấp, ít gây lỗi vặt nhưng lại đủ mạnh mẽ để sử dụng cho cá nhân. Còn những cấu hình cao hơn, bạn cần phải tìm đến một dịch vụ control panel khác.

### c. Cyber Panel
--> miễn phí và hỗ trợ Tiếng Việt sử dụng OpenLiteSpeed làm webserver
### d. VestaCP
--> Vesta Control Panel: mã nguồn mở miễn phí, dễ cài đặt và cấu hình bảng điều khiển dựa trên nền tảng web cho các hệ thống như Linux. Với bất kỳ ai dùng VestaCP,
ngay cả quản trị viên hệ thống mới cũng có thể dễ dàng quản lý các trang web trong VPS.
- Khi nào nên dùng VestaCP?
VestaCP chủ yếu phục vụ cho người dùng với những nhu cầu cơ bản dưới đây:
    ● Dùng dịch vụ web và mã nguồn được viết thông qua ngôn ngữ PHP hoặc cơ sở dữ liệu Mysql.
    ● Áp dụng vào các dịch vụ về Email như: Mail server, webmail,…
    ● Dùng cho những dịch vụ thuộc DNS.
    ● Cấu hình sao lưu tự động hoặc thủ công, restore lại dữ liệu cho từng ứng dụng khác nhau.
    ● Cấu hình firewall cho server
    ● Dùng dịch vụ FTP để upload, download.
    ● Phân bổ, chia sẻ dữ liệu hoặc tài nguyên, phân quyền cho từng người dùng khác nhau.

## 4. WOrdpress HOsting
--> Là một hệ thống quản lý nội dung (CMS) mã nguồn mở, giúp người dùng dễ dàng tạo và quản lý trang web mà không cần kiến thức code
- Van de:
    + Web chậm và điểm Pagespeed: CO the dung liteSpeed Cache, CDN, SEO (rank math), ccu nen hinh anh (toi uu HTML, CSS, JS)
--> QUa nhieu plugin -> xung dot & giam hieu suat & bao mat
    --> Cach giai quyet la go plugin k can thiet, cap nhat plugin thuong xuyen, kiem tra tuong thich

## 5. iptables

---

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

→ Ở phía Backend Server ta sẽ host bằng Apache. Trường hợp người dùng cần tải các file động (PHP scripts,...) thì Nginx sẽ hoạt động như 1 reverse proxy gửi requests đến cho phía Apache để xử lý và trả kết quả lại cho Clients.

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
