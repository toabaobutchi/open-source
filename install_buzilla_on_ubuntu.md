# Cài đặt Bugzilla trong Ubuntu

* Nguồn: [Quick start (Ubuntu Linux 22.04)](https://bugzilla.readthedocs.io/en/latest/installing/quick-start.html#quick-start)

## Cập nhật danh sách các gói phần mềm apt

Sử dụng lần lượt các lệnh sau:
```console
    sudo apt update -y
    sudo apt upgrade -y
```
Option `-y` dùng để đồng ý các xác nhận `[Y/n]` khi cập nhật, làm cho quá trình diễn ra tự động.

Hoặc **sử dụng duy nhất 1 dòng lệnh** như sau:
```console
    sudo apt update -y && sudo apt upgrade -y
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

```sql
    mysql -u root -e "CREATE DATABASE IF NOT EXISTS bugs CHARACTER SET = 'utf8'"
```
