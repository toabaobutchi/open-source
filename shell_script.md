# Linux Shell script

* Dòng đầu bắt đầu với `#!/bin/bash`.

* Cấp quyền thực thi: `chmod u+x <file sh>`.

* Thực thi: `./<file sh>`.

## Biến

* Cú pháp

```console
name=value
```
> [!Warning]
> Không có khoảng trắng ở trước và sau dấu `=`.

**Ví dụ:**

```console
a=10
b="John"
```

> [!Note]
> Chuỗi trong Shell Script có thể biểu diễn bằng dấu nháy đôi `"` hoặc nháy đơn `'`.

* Để gọi đến biến, sử dụng dấu `$` phía trước tên biến

**Ví dụ:**

```console
echo $a
```

## Đọc giá trị từ bàn phím

* Cú pháp:

```console
read <tên_biến_1> <tên_biến_2> ...
```
Có thể đọc nhiều giá trị cho biến bằng việc phân cách với khoảng trắng.

## Toán tử & biểu thức

* Toán tử số học: `+`, `-`, `*`, `/`, `%`, `++`, `--`

* Toán tử so sánh: `==`, `!=`, `<=`, `>=`, `<`, `>`

* Toán tử logic: `&&`, `||`, `!`

* Biểu thức:
  * `echo $((a + b))`
 
  * <code>echo \`expr $a + $b\`</code> : lưu ý rằng sử dụng dấu ``` ` ``` không phải là dấu `"` hay `'`.

## Câu lệnh điều kiện

Cú pháp:

```console
if ((biểu thức bool))
then
...
elif
...
else
...
fi
```

