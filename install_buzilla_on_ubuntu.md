# Cài đặt Bugzilla trong Ubuntu

* Nguồn: [Quick start (Ubuntu Linux 22.04)](https://bugzilla.readthedocs.io/en/latest/installing/quick-start.html#quick-start)

## Cập nhật danh sách các gói phần mềm apt

Sử dụng lần lượt các lệnh sau:
```console
    sudo apt update
    sudo apt upgrade -y
```
Option `-y` dùng để đồng ý các xác nhận `[Y/n]` khi cập nhật, làm cho quá trình diễn ra tự động.

Hoặc **sử dụng duy nhất 1 dòng lệnh** như sau:
```console
    sudo apt update && sudo apt upgrade -y
```

## Sử dụng quyền root

```console
    sudo su
```

Các lệnh ở các phần bên dưới sẽ không cần bắt đầu bằng `sudo`.

## Cài đặt các thành phần phụ thuộc
* Tải trình soạn thảo nano: `apt install git nano`.
* Sử dụng lệnh tổng hợp sau để cài đặt toàn bộ các thành phần cần thiết:

```console
   apt install apache2 build-essential mariadb-server libcgi-pm-perl libdigest-sha-perl libtimedate-perl libdatetime-perl libdatetime-timezone-perl libdbi-perl libdbix-connector-perl libtemplate-perl libemail-address-perl libemail-sender-perl libemail-mime-perl liburi-perl liblist-moreutils-perl libmath-random-isaac-perl libjson-xs-perl libgd-perl libchart-perl libtemplate-plugin-gd-perl libgd-text-perl libgd-graph-perl libmime-tools-perl libwww-perl libxml-twig-perl libnet-ldap-perl libauthen-sasl-perl libnet-smtp-ssl-perl libauthen-radius-perl libsoap-lite-perl libxmlrpc-lite-perl libjson-rpc-perl libtest-taint-perl libhtml-parser-perl libhtml-scrubber-perl libencode-perl libencode-detect-perl libemail-reply-perl libhtml-formattext-withlinks-perl libtheschwartz-perl libdaemon-generic-perl libapache2-mod-perl2 libapache2-mod-perl2-dev libfile-mimeinfo-perl libio-stringy-perl libcache-memcached-perl libfile-copy-recursive-perl libfile-which-perl libdbd-mysql-perl perlmagick lynx graphviz python3-sphinx rst2pdf
```

## Cấu hình MariaDB

```console
nano /etc/mysql/mariadb.conf.d/50-server.cnf
```
* Bỏ comment (Uncomment) dòng 34 để có `max_allowed_packet`.
* Thêm ở dòng 42: `ft_min_word_len=2`.

> **Mẹo:** Sử dụng `Ctrl` + `/` để di chuyển đến dòng chỉ định. Nhập số dòng và ấn **Enter**.

* Lưu và thoát ra. Để lưu thì chọn `Ctrl` + `O` (không phải số 0) và ấn **Enter**. Thoát ra bằng `Ctrl` + `X`.

* Tạo cơ sở dữ liệu `bugs` cho Bugzilla:

```console
    mysql -u root -e "CREATE DATABASE IF NOT EXISTS bugs CHARACTER SET = 'utf8'"
```
* Thêm user MariaDB dùng cho Bugzilla:
```console
    mysql -u root -e "GRANT ALL PRIVILEGES ON bugs.* TO bugs@localhost IDENTIFIED BY '...'"
```
Thay phần `...` thành mật khẩu muốn tạo cho user.

* Khởi động lại MariaDB: `service mariadb restart`. Sẽ có một số dòng lệnh được nhắc nhở khi sử dụng lệnh này. Hãy chạy các lệnh đó.

## Cầu hình Apache

```console
    nano /etc/apache2/sites-available/bugzilla.conf
```
Sao chép và dán đoạn nội dung bên dưới. Sau đó thì lưu lại.
```console
Alias /bugzilla /var/www/webapps/bugzilla
<Directory /var/www/webapps/bugzilla>
  AddHandler cgi-script .cgi
  Options +ExecCGI
  DirectoryIndex index.cgi index.html
  AllowOverride All
</Directory>
```

Cấu hình trên thiết lập Bugzilla được phân phát trên máy chủ của bạn theo đường dẫn `localhost/bugzilla`.

Chạy lần lượt các lệnh sau:
```console
    a2ensite bugzilla

    a2enmod cgi headers expires rewrite

    service apache2 restart
```

Khi sử dụng các lệnh trên, sẽ có một só lệnh được khuyến nghị cần chạy.

## Tải Bugzilla

```console
    mkdir -p /var/www/webapps

    cd /var/www/webapps

    git clone --branch release-5.0-stable https://github.com/bugzilla/bugzilla bugzilla
```
## Check setup

```console
    cd /var/www/webapps/bugzilla
    ./checksetup.pl
    nano localconfig
```
* Đặt các giá trị sau trong `localconfig`:
    * Dòng 29: đặt `$webservergroup` thành `www-data`.
    * Dòng 67: đặt `$db_pass` thành mật khẩu đã đặt với tài khoản `bugs` ở bước [Cấu hình MariaDB](#cấu-hình-mariadb).

* Chạy lại lệnh `./checksetup.pl`.

* Test server
```console
    ./testserver.pl http://localhost/bugzilla
```
Bỏ qua lỗi liên quan đến `gdlib-config`.

## Truy cập Bugzilla

```console
    lynx http://localhost/bugzilla
```
## Cấu hình Bugzilla

Once you have worked out how to access your Bugzilla in a graphical web browser, bring up the front page, click Log In in the header, and log in as the admin user you defined in step 10.

Click the Parameters link on the page it gives you, and set the following parameters in the Required Settings section:

* **urlbase:** http://<servername>/bugzilla/ or http://<ip address>/bugzilla/
* **ssl_redirect**: on if you set up an SSL certificate

Click Save Changes at the bottom of the page.

There are several ways to get Bugzilla to send email. The easiest is to use Gmail, so we do that here so you have it working. Visit https://gmail.com and create a new Gmail account for your Bugzilla to use. Then, open the Email section of the Parameters using the link in the left column, and set the following parameter values:

* **mail_delivery_method**: SMTP
* **mailfrom**: new_gmail_address@gmail.com
* **smtpserver**: smtp.gmail.com:465
* **smtp_username**: new_gmail_address@gmail.com
* **smtp_password**: new_gmail_password
* **smtp_ssl**: On

Click Save Changes at the bottom of the page.

And you’re all ready to go. :-)
