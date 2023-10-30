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

    # [command] thông dụng: start, stop, restart, ...
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

## Cài đặt PHP

* Cài đặt:
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

* Từ thư mục `/var/www`, ta có thể tạo một thư mục mới trùng tên với host ảo cần tạo.

```console
    mkdir yourvhost
```

> [!Important]
> * Ở các ví dụ sau, tên host ảo sẽ là **`yourvhost.com`**. Hãy chỉnh sửa lại cho phù hợp với nhu cầu.
>
> * Có thể tạo thư mục `yourvhost` ở thư mục `html` bên trong hoặc bất cứ vị trí nào bắt đầu từ `/var/www`. Nội dung sau sẽ chỉ định đường dẫn cụ thể.

* Tạo một file `index.php` (hoặc bất kỳ, lát nữa sẽ hiển thị trên web):

```console
    sudo nano index.php
```

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
        DocumentRoot /var/www/[path to yourvhost]
    </VirtualHost>
```

### Bước 3: Đăng ký yourvhost.com như là localhost

* Đăng ký localhost mới cho host ảo vừa tạo:

```console
    sudo nano /etc/hosts
```
Ở đây đang muốn cấu hình localhost có tên khác là yourvhost.com, nên hãy viết trong file `/etc/hosts`:
```console
    127.0.0.1 yourvhost.com
```

* Kích hoạt host ảo mới: 
```console
    sudo a2ensite [virtual-host-name].conf
```
- Tắt 000-default.conf:

```console
    sudo a2dissite 000-default.conf
```

* Khởi động lại Apache2:

```console
    sudo systemctl reload apache2
```

Truy cập vào host ảo trong trình duyệt và kiểm tra.


Cài đặt Wordpress: [**Wordpress**](https://ubuntu.com/tutorials/install-and-configure-wordpress)
