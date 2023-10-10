# Cài đặt Bugzilla trong Ubuntu


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

## Tải và cài đặt Apache
