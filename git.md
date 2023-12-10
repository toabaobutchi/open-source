# Một số câu lệnh trong Git

Tải Git tại: **https://git-scm.com/downloads**

## Cấu hình tên và email

Sau khi tải [**Git**](https://git-scm.com/downloads), ta cần cấu hình lại tên và email như sau:

```sh
git config --global user.name '<tên>'
git config --global user.email '<email>'
```
Trong đó `<tên>` và `<email>` thậm chí không có thực vẫn được (tuỳ ý).

## Tạo Git repo (repository) ở local

Tại thư mục muốn làm việc với git (Workspace), mở Terminal (hoặc môi trường bảng lệnh nào khác như Command Promt, Windows Terminal, ...) và sử dụng lệnh sau:

```sh
git init
```

Kết quả:

```
Initialized empty Git repository in D:/Temporary/Git/.git/
```

Bây giờ, ta có thể tạo một số file trong thư mục workspace và thêm một số nội dung bất kỳ vào.

## Xem trạng thái của local repo

Sử dụng lệnh:

```sh
git status
```

Lệnh này cho biết trạng thái của các file trong local repo hiện tại (untracked, modified, ...)

Ví dụ:

```
PS D:\Temporary\Git> git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        index.html
```

## Các khu vực và trạng thái

Có 3 khu vực khi làm việc với git:

* Thư mục hiện tại: các file vừa tạo ra hoặc vừa cập nhật (bao gồm cả xoá) chưa được `add`.

* Staging Area: khu vực chứa các file sẽ được thêm vào repo khi thực hiện lệnh `git add .` hoặc `git add <tên file>`.

* Commited: khu vực các file được commit với lệnh `git commit -m "<message>"`. Khi gọi `git commit` thì repo sẽ nhận các file được gọi `git add`.




