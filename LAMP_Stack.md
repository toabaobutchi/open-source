# Cài đặt LAMP Stack - Tạo Virtual host

Cập nhật `apt`:

```console
    sudo apt update
    sudo apt upgrade
```

## Cài đặt LAMP Stack

### Cài đặt máy chủ Apache

```console
    sudo apt install apache2
```

Thông thường, máy chủ Apache sẽ tự động active sau khi cài đặt, sử dụng lệnh sau để kiểm tra:

```console
    sudo systemctl status apache2
```

Một cách khác để kiểm tra máy chủ Apache là mở trình duyệt và truy vập vào `localhost`.

Nếu máy chủ Apache chưa khởi chạy, sử dụng lệnh sau:

```console
    sudo systemctl start apache2
```
