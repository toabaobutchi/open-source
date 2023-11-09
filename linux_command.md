# Các câu lệnh thường dùng trên Linux

## Update & Upgrade các gói phần mềm trên Ubuntu - Linux

* Update: tải các thông tin gói từ tất cả các nguồn được cấu hình, thường được xác định trong `/etc/apt/sources.list` và một số khác từ `/etc/apt/sources.list.d/`.

```console
sudo apt update
# hoặc
sudo apt-get update
```

* Upgrade: cài đặt các gói từ nguồn được cấu hình.

```console
sudo apt upgrade
# hoặc
sudo apt-get upgrade
```

Có thể sử dụng tuỳ chọn `-y` để đồng ý và bỏ qua xác nhận khi sử dụng `sudo apt upgrade`.

```console
sudo apt upgrade -y
```

Cả `apt` và `apt-get` đều là những công cụ trình quản lý gói dành cho các bản phân phối Linux dựa trên Debian như **Debian**, **Ubuntu**, **Linux Mint** và **elementary OS**. 

Tuy nhiên, `apt` là phiên bản mới hơn của `apt-get` và được thiết kế để trở thành lệnh thay thế thân thiện với người dùng hơn thay cho `apt-get`.

## Xoá màn hình

Sử dụng lệnh `clear` hoặc tổ hợp phím `ctrl` + `l`.

## Xem nội dung của thư mục

Sử dụng lệnh `ls` (list) với cú pháp sau:

```console
ls [options] [directory]
```

Nếu `[directory]` không chỉ định, lệnh `ls` sẽ có thực hiện trên đường dẫn hiện tại.

Các `[option]` thường dùng:

* `-a`, `--all`: Xem tất cả thư mục kể cả các thư mục bắt đầu bằng dấu chấm `.` (Trong hệ thống thư mục của Linux, tên thư mục bắt đầu bằng dấu chấm được hiểu là thư mục ẩn)

* `-l`: hiển thị nội dung thư mục dưới định dạng dài, nhiều thông tin hơn bao gồm: quyền truy cập, owner, group, thời gian tạo, ...

