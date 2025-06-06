# Bài tập 06 của sinh viên: K225480106028 - Vũ Bảo Khánh - Môn Hệ quản trị CSDL

## Deadline: 23h59 NGÀY 25/4/2025

## ĐIỀU KIỆN: (ĐÃ HOÀN THÀNH CÁC BÀI TRƯỚC)

## BÀI TOÁN:

Cho file dữ liệu `sv_tnut.sql` có dung lượng hơn 1.6MB, chứa bảng SinhVien với hơn 9000 dòng.

### Mục tiêu:
1. Import được dữ liệu từ file `sv_tnut.sql` vào SQL Server.
2. Thực hiện các truy vấn SELECT để kiểm tra thông tin theo dữ liệu cá nhân.
3. Phân tích và suy luận logic các truy vấn.

---

## 1. Các bước import file sv_tnut.sql vào SQL Server:
- Tạo CSDL mới: `SV_TNUT_DB` bằng lệnh:
```sql
CREATE DATABASE SV_TNUT_DB;
GO
USE SV_TNUT_DB;
```
- Mở file `sv_tnut.sql` bằng cách vào `File > Open > File` trong SSMS.
- Chọn đúng file và nhấn **Execute** (F5) để chạy.

---

## 2. Dữ liệu cá nhân:
- Họ tên: **Vũ Bảo Khánh**
- SĐT: **0972903814**
- Ngày sinh: **2004-10-02**

---

## 3. Tìm các sinh viên trùng **ngày/tháng/năm sinh**:
```sql
SELECT * FROM SinhVien
WHERE NgaySinh = '2004-10-02';
```

## 4. Tìm các sinh viên trùng **ngày và tháng sinh**:
```sql
SELECT * FROM SinhVien
WHERE DAY(NgaySinh) = 02 AND MONTH(NgaySinh) = 10;
```

## 5. Tìm các sinh viên trùng **tháng và năm sinh**:
```sql
SELECT * FROM SinhVien
WHERE MONTH(NgaySinh) = 1010 AND YEAR(NgaySinh) = 2004;
```

## 6. Tìm các sinh viên trùng **tên** với em (Khánh):
```sql
SELECT * FROM SinhVien
WHERE RIGHT(LTRIM(RTRIM(HoTen)), CHARINDEX(' ', REVERSE(HoTen)) - 1) = 'Khánh';
```

## 7. Tìm các sinh viên trùng **họ và tên đệm** với em (Vũ Bảo):
```sql
SELECT * FROM SinhVien
WHERE LEFT(HoTen, LEN(HoTen) - CHARINDEX(' ', REVERSE(HoTen))) = 'Vũ Bảo';
```

## 8. Tìm các sinh viên có **SĐT sai khác đúng 1 chữ số**:
> Giải pháp này phức tạp do SQL Server không hỗ trợ hàm so sánh ký tự từng vị trí. Cần viết UDF riêng hoặc xử lý ngoài SQL.
> Tạm thời ta lọc các số có độ dài tương tự:
```sql
SELECT * FROM SinhVien
WHERE LEN(SoDT) = 10 AND SoDT LIKE '0972903814';
```

## 9. Liệt kê tất cả sinh viên **ngành KMT**, sắp xếp theo **tên và họ đệm**, chuẩn tiếng Việt:
```sql
SELECT * FROM SinhVien
WHERE Nganh = 'KMT'
ORDER BY 
    RIGHT(HoTen, CHARINDEX(' ', REVERSE(HoTen)) - 1) COLLATE Vietnamese_CI_AS,
    LEFT(HoTen, LEN(HoTen) - CHARINDEX(' ', REVERSE(HoTen))) COLLATE Vietnamese_CI_AS;
```
> **Giải thích:**
> - `RIGHT(...)`: tách tên cuối
> - `LEFT(...)`: tách họ và tên đệm
> - `COLLATE Vietnamese_CI_AS`: đảm bảo sắp xếp theo bảng mã tiếng Việt đúng

## 10. Liệt kê tất cả **SV nữ ngành KMT**:
```sql
SELECT * FROM SinhVien
WHERE GioiTinh = N'Nữ' AND Nganh = 'KMT';
```
> **Suy nghĩ:** 
> - Kết hợp điều kiện `GioiTinh = 'Nữ'` và `Nganh = 'KMT'`
> - Có thể có lỗi nếu bảng không ghi rõ giới tính theo chuẩn (ví dụ: "Nu", "nữ", "NỮ"…), nên nên dùng `COLLATE` hoặc chuyển về chữ thường để kiểm tra chắc chắn.

---

## KẾT LUẬN:
Thông qua bài tập này, em đã thực hành nâng cao kỹ năng truy vấn SELECT trong SQL Server, xử lý các bài toán thực tế liên quan đến dữ liệu lớn (9000+ bản ghi) và làm quen với cách tách chuỗi trong SQL để xử lý tên tiếng Việt.
