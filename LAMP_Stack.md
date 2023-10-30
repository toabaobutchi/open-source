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
> Ở các ví dụ sau, tên host ảo sẽ là **`yourvhost.com`**. Hãy chỉnh sửa lại cho phù hợp với nhu cầu.

- Tạo một file index.php (có thể đặt tên khác): `sudo nano index.php`
  
- Di chuyển vào thư mục **/etc/apache2/sites-available**: `cd /etc/apache2/sites-available`
  
- Tạo file **[virtual-host-name].conf**: `sudo nano [virtual-host-name].conf` (`[virtual-host-name]` tự  đặt lại)
  
- Chép đoạn mã bên dưới vào file vừa tạo:

```console
    <VirtualHost *:80>
	    ServerName  [virtual-host-name]
	    DocumentRoot /var/www/[virtual-host-name]
    </VirtualHost>
```
- Đăng ký localhost mới cho virtual host vừa tạo: 
    `sudo nano /etc/hosts`
Điền vào dòng chữ: `127.0.0.1 [virtual-host-name]`
- Kích hoạt host ảo mới: 
```console
    sudo a2ensite [virtual-host-name].conf
    sudo systemctl reload apache2
```
- Tắt 000-default.conf:

```console
sudo a2dissite 000-default.conf
sudo systemctl reload apache2
```

Truy cập vào host ảo và kiểm tra.


Cài đặt Wordpress: [**Wordpress**](https://ubuntu.com/tutorials/install-and-configure-wordpress)
