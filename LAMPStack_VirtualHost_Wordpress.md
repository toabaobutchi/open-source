# Cài đặt LAMP Stack - Tạo Virtual host

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

### Bước 1: Khai báo thư mục sẽ chứa nội dung khi truy cập vào host ảo

* Nếu như **WampServer** hay **Xampp** sử dụng thư mục gốc là `C:\wamp64\www` hay `C:\xampp\htdocs` thì thư mục của máy chủ Apache trong Linux sử dụng là `/var/www`. Để đăng ký một host ảo trong localhost, hãy di chuyển vào thư mục này
 
 ```console
 # từ bất kỳ đường dẫn hiện tại nào
 cd /var/www
```

> [!Note]
> Trong thư mục `/var/www` có thư mục `html` chứa file `index.html`. File `index.html` là file khởi động khi truy cập vào `localhost`.

* Từ thư mục `/var/www`, ta có thể tạo một thư mục mới trùng tên với host ảo cần tạo. Về cơ bản thì muốn tạo thư mục ở đâu cũng được (Desktop, thư mục tự tạo, ...).

```console
mkdir yourvhost
```

> [!Important]
> * Ở các ví dụ sau, tên host ảo sẽ là **`yourvhost.com`**. Hãy chỉnh sửa lại cho phù hợp với nhu cầu.
>
> * Có thể tạo thư mục `yourvhost` ở thư mục `html` bên trong hoặc bất cứ vị trí nào bắt đầu từ `/var/www`. Nội dung sau sẽ chỉ định đường dẫn cụ thể.
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

* Di chuyển vào thư mục **/etc/apache2/sites-available**: thư mục này chứa các file cấu hình cho host

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
    DocumentRoot [path to yourvhost]
</VirtualHost>
```

Đoạn mã trên chỉ là một ví dụ đơn giản dùng để bắt toàn bộ IP với port 80 (`*:80`). Có thể chỉ định thông tin khác.

### Bước 3: Đăng ký host ảo
* Đăng ký host ảo vừa tạo:

```console
sudo nano /etc/hosts
```

Ở đây đang muốn cấu hình localhost có tên khác là yourvhost.com, nên hãy viết trong file `/etc/hosts`:

```console
127.0.0.1 yourvhost.com
```

Hoặc có thể chỉ định 1 IP khác, ví dụ:

```console
127.0.1.2 yourvhost.com
```

* Kích hoạt host ảo mới: 
```console
sudo a2ensite [virtual-host-name].conf
```
- Tắt `000-default.conf` (nếu như muốn tắt `localhost`):

```console
sudo a2dissite 000-default.conf
```

* Khởi động lại Apache2:

```console
sudo systemctl reload apache2
```

Truy cập vào host ảo trong trình duyệt và kiểm tra.


Cài đặt Wordpress: [**Wordpress**](https://ubuntu.com/tutorials/install-and-configure-wordpress)
