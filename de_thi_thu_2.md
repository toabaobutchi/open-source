# Đề tham khảo

Cài đặt wordpress trên host ảo và localhost. Ta giữ nguyên bản của localhost và tải một bản mới, database, user mới.

Chạy các lần lượt các lệnh sau:

```console
cd /var/www/html

mkdir <tên-thư-mục> (1)

sudo wget -c http://wordpress.org/latest.tar.gz

sudo tar -xzvf latest.tar.gz

sudo chmod -R 777 wordpress/

sudo mysql -u root -p

CREATE DATABASE wordpress; (2)

CREATE USER <username>@localhost IDENTIFIED WITH mysql_native_password BY '<password>'; (3)

GRANT ALL ON wordpress.* TO <username>@localhost; (4)

FLUSH PRIVILEGES;

EXIT; 
```

* `(1)`: `<tên-thư-mục>` sẽ là tên host ảo mà thấy yêu cầu, không cần .com, .linux, ...

* `(2)`, `(3)`, `(4)`: tên `wordpress`, `<username>` và `<password>` **nên thay đổi để không trùng với phiên bản ở localhost**

Sau đó cấu hình host ảo như bình thường bắt đầu từ [**Bước 2**](https://github.com/toabaobutchi/open-source/blob/main/LAMPStack_VirtualHost_Wordpress.md#b%C6%B0%E1%BB%9Bc-2-c%E1%BA%A5u-h%C3%ACnh-host-%E1%BA%A3o).

Tuy nhiên, bây giờ phải đăng ký theo host ảo mà thầy yêu cầu.
