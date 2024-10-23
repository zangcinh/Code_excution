
# Tổng quan
- Code Excution là thuật ngữ chung để chi việc thực thi bất kì đoạn mã nào trên hệ thống

# Biến thể của Code Excution 

**1. RCE**

**a) Định nghĩa**

- RCE ( Remote Code Excution ) là 1 biến thể của Code Excution cho phép kẻ tấn công thực thi mã từ xa mà không cần quyền hợp lệ

**b) Ví dụ**

```
<?php eval("echo ".$_GET["user"].";"); ?>
```

Người phát triển có thể nghĩa rằng người dùng chỉ nhập tên người dùng hợp lệ làm tham số cho URL

```
http://www.example.com/index.php?user=admin
```

Sau đó, ứng dụng sẽ chạy giá trị tham số dưới dạng mã

```
echo admin;
```
và in tên người dùng

Kẻ tấn công có thể chèn mã độc vào bằng cách chèn dấu `;` vào đằng sau URL

```
http://www.example.com/index.php?user=admin;phpinfo();
```

Sau đó, đoạn code sẽ được thực thi như sau

```
echo admin;
phpinfo();
```

**2. ACE**

- ACE ( Arbitrary Code Execution ) là khả năng kẻ tấn công thực thi bất kì mã tùy ý nào trên hệ thống ( có thể thực hiện cục bộ hoặc từ xa )
