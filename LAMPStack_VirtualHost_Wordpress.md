# Cài đặt LAMP Stack - Tạo Virtual host - Wordpress

## Truy cập bằng quyền Root

Sử dụng lệnh `sudo su` và nhập mật khẩu. Các lệnh phía sau sẽ không cần bắt đầu bằng lệnh `sudo`.

## Cài đặt máy chủ Apache2

* Cài đặt:
```console
sudo apt install apache2
```

* Kiểm tra trạng thái máy chủ Apache2:

```console
sudo systemctl status apache2
```
> [!Note]
> Một cách khác để kiểm tra máy chủ Apache đã khởi chạy hay chưa là mở trình duyệt và truy cập vào `localhost`.

* Các lệnh liên quan khác - sử dụng cú pháp sau:

```console
sudo systemctl [command] apache2

# [command] thông dụng: start, stop, restart, reload, ...
```

## Cài đặt máy chủ MySQL

* Cài đặt:
```console
sudo apt install mysql-server
```

* Kiểm tra:
```console
sudo mysql
```
Kết quả là một đoạn kết quả hiện ra cùng với dòng lệnh bắt đầu bằng `mysql >`.

## Cài đặt PHP

* Cài đặt (bao gồm PHP và các gói cần thiết với Apache và MySQL):
```console
sudo apt install php libapache2-mod-php php-mysql
```

* Kiểm tra:
```console
php -v
```

## Tạo host ảo trong localhost

### Sơ lược các nội dung cần nắm:

* Thư mục `/etc/apache2/sites-available` chứa các file `*.conf` để cấu hình các host: chạy với URL như thế nào, port bao nhiêu, trỏ đến thư mục nào để lấy nội dung, ...

* File `/etc/hosts` chứa các host được đăng ký trong máy Linux.

### Quick start

> [!Note]
> Hãy bỏ qua các phần sau nếu muốn thực hiện nhanh các thao tác.

Lần lượt chạy các lệnh sau (theo từng dòng):

* Vào thư mục **`/var/www/html`**, tạo thư mục **`<tên-host-ảo>`** và tạo file **`index.php`** (hoặc **`index.html`**)

```console
cd /var/www/html && sudo mkdir <tên-host-ảo> && cd <tên-host-ảo> && sudo nano index.php
```

_Nhập một đoạn mã PHP (hoặc HTML) vào file **`index.php`**, ví dụ:_

```php
<?= "Hello World!" ?>
```

_Nội dung file này sẽ hiển thị khi gọi đến host ảo trên URL (sau khi thực hiện các phần sau)_

* Di chuyển vào thư mục **`/etc/apache2/sites-available`**, tạo file cấu hình host ảo **`<tên-host-ảo>.conf`**:

```console
cd /etc/apache2/sites-available && sudo nano <tên-host-ảo>.conf
```

_Chép đoạn mã bên dưới vào file cấu hình vừa tạo:_

```console
<VirtualHost *:80>
    ServerName  <tên-miền>
    DocumentRoot /var/www/html/<tên-host-ảo>
</VirtualHost>
```

**`<tên-miền>`** là đường dẫn của host ảo muốn truy cập trên thanh địa chỉ, ví dụ như yourhost.com, yourhost.dev, yourhost.cc, yourhost.io, ...

* Đăng ký host ảo:

```console
sudo nano /etc/hosts
```
_Tìm một dòng trống bên dưới các IP được đăng ký sẵn, đăng ký host ảo vừa tạo ra:_

```console
127.0.0.1       localhost
127.0.1.1       ngohoaianVM
<IP>    <tên-miền> # viết ở đây
# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
```

* Kích hoạt host ảo mới: 
```console
sudo a2ensite <tên-host-ảo>.conf
```

* Reload lại apache2

```console
sudo systemctl reload apache2
```
### Bước 1: Khai báo thư mục sẽ chứa nội dung khi truy cập vào host ảo

* Nếu như **WampServer** hay **Xampp** sử dụng thư mục gốc là `C:\wamp64\www` hay `C:\xampp\htdocs` thì thư mục của máy chủ Apache trong Linux sử dụng là `/var/www`. Để đăng ký một host ảo trong localhost, hãy di chuyển vào thư mục này
 
 ```console
 # từ bất kỳ đường dẫn hiện tại nào
 cd /var/www/html
```

> [!Note]
> Trong thư mục `/var/www/html` chứa file `index.html`. File `index.html` này là file khởi động khi truy cập vào `localhost`.

* Từ thư mục `/var/www/html`, ta có thể tạo một thư mục mới trùng tên với host ảo cần tạo. Về cơ bản thì muốn tạo thư mục ở đâu cũng được (Desktop, thư mục tự tạo, ...).

```console
mkdir yourvhost
```

> [!Important]
> * Ở các ví dụ sau, tên host ảo sẽ là **`yourvhost.com`**. Hãy chỉnh sửa lại cho phù hợp với nhu cầu.
>
> * Đường dẫn cần phải nhớ phần sau sẽ cấu hình trỏ đến thư mục này
>
> * Ở đa phần các trang web hướng dẫn sẽ trỏ đến `/var/www/html`.

* Tạo một file `index.php` (hoặc bất kỳ, lát nữa sẽ hiển thị trên web):

```console
sudo nano index.php
```

Có thể dùng các trình soạn thảo khác như `vim`, `kate`, ... Xem thêm tại: [**Top 10 công cụ soạn thảo trên Linux**](https://hotanmy.blogspot.com/2017/08/top-10-cong-cu-soan-thao-hang-dau-tren-linux.html). Ở nội dung này sử dụng `nano`.

Hãy thêm một đoạn mã bất kỳ của PHP vào file vừa tạo, ví dụ:

```php
<?php
    echo "Hello world!";
?>
```

### Bước 2: Cấu hình host ảo

* Di chuyển vào thư mục **`/etc/apache2/sites-available`**: thư mục này chứa các file cấu hình cho host

```console
cd /etc/apache2/sites-available
```

* Tạo file **`yourvhost.conf`**

```console
sudo nano yourvhost.conf
```

* Chép đoạn mã bên dưới vào file vừa tạo:

```console
<VirtualHost *:80>
    ServerName  yourvhost.com
    DocumentRoot /var/www/html/<tên-thư-mục-vừa-tạo-ở-bước-1>
</VirtualHost>
```

Đoạn mã trên chỉ là một ví dụ đơn giản dùng để bắt toàn bộ IP với port 80 (`*:80`). Xem thêm các thông tin khác tại: [**Apache Virtual Host documentation**](https://httpd.apache.org/docs/2.4/vhosts/index.html).

### Bước 3: Đăng ký host ảo
* Đăng ký host ảo vừa tạo:

```console
sudo nano /etc/hosts
```

Chỉ định một IP cụ thể và tên host ảo đang muốn tạo, ví dụ:

```console
127.0.1.2 yourvhost.com
```

* Kích hoạt host ảo mới: 
```console
sudo a2ensite [virtual-host-name].conf
```
- Tắt `000-default.conf` (**nếu như muốn tắt `localhost`**):

```console
sudo a2dissite 000-default.conf
```

> [!Warning]
> Nếu tắt cấu hình của file `000-default.conf` thì sẽ không thể truy cập với đường dẫn bắt đầu bằng `localhost`, hãy cân nhắc. Nếu muốn enable (cho phép) lại file `000-default.conf` thì sử dụng lệnh `sudo a2ensite 000-default.conf`.

* Khởi động lại Apache2:

```console
sudo systemctl reload apache2
```

Truy cập vào host ảo trong trình duyệt và kiểm tra. Nếu đường dẫn có vấn đề, hãy thử một trong các cách sau:

* Sử dụng lệnh `lynx <tên-miền-host-ảo>`.

* Thêm tiền tố `http://` vào đường dẫn trước `<tên-miền-host-ảo>`.

## Cài đặt Wordpress (Ứng dụng Web) khi đã cài đặt LAMP Stack

Tham khảo tại: [**Wordpress with LAMP Stack**](https://vexxhost.com/resources/tutorials/how-to-install-wordpress-with-ubuntu-20-04-and-a-lamp-stack/).

### Cài đặt các gói cần thiết của PHP:

```console
sudo apt install php-curl php-gd php-mbstring php-xml php-xmlrpc php-soap php-intl php-zip
```

* Restart Apache

```console
sudo systemctl restart apache2
```

### Cài đặt Wordpress

* Di chuyển vào thư mục `/var/www/html`:

```console
cd /var/www/html
```

* Tải phiên bản mới nhất của Wordpress:

```console
sudo wget -c http://wordpress.org/latest.tar.gz
```

* Giải nén file:

```console
sudo tar -xzvf latest.tar.gz
```

Thư mục `wordpress` sẽ được giải nén trong đường dẫn `/var/www/html`, và có thể truy cập bằng đường dẫn `localhost/wordpress`.

* Cấp quyền cho truy cập vào thư mục `wordpress`:

```console
sudo chmod -R 777 wordpress/
```

### Tạo và cấu hình Database cho Wordpress

* Truy cập MySQL với tài khoản `root`:

```console
sudo mysql -u root -p
```

* Tạo databse dành cho Wordpress:

```console
CREATE DATABASE wordpress;
```

Có thể thay `wordpress` thành tên tuỳ ý, nó đơn giản chỉ là tên database.

* Tạo user dành cho Wordpress, user này sẽ được Wordpress sử dụng và thao tác trên database vừa tạo ở bước trên.

```console
CREATE USER <username>@localhost IDENTIFIED WITH mysql_native_password BY '<password>';
```

Thay thế `<username>` và `<password>` thành giá trị muốn đặt.

* Cấp quyền cho user vừa tạo (tốt nhất chạy từng lệnh, thay thế `<username>` bằng tên vừa tạo ở bước trên):

```console
GRANT ALL ON wordpress.* TO <username>@localhost;
FLUSH PRIVILEGES;
EXIT;
```

Có thể thay thế `wordpress` thành tên database vừa tạo khi nãy (nếu có).

### Truy cập và cấu hình Wordpress

Truy cập vào đường dẫn `localhost/wordpress` (hoặc host ảo nếu có tạo) và cấu hình các thông tin được yêu cầu.

Có thể cấu hình bằng file nhưng thực hiện bằng giao diện đơn giản hơn nhiều.
