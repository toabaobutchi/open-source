# Cài đặt LAMP Stack - Tạo Virtual host


Cài đặt Apache2:`sudo apt install apache2`

Kiểm tra trạng thái máy chủ apache2: `sudo systemctl status apache2`

Cài đặt máy chủ MySQL: `sudo apt install mysql-server`

Kiểm tra máy chủ MySQL: `sudo mysql`

Cài đặt PHP `sudo apt install php libapache2-mod-php php-mysql`

Kiểm tra PHP `php -v`

Tạo host ảo
- Di chuyển vào thư mục **/var/www**: `cd /var/www`

- Tạo thư mục có tên trùng với virtual host cần tạo: `mkdir myweb`
  
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
