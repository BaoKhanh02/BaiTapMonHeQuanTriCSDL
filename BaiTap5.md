# BÀI TẬP VỀ NHÀ 05, Môn Hệ quản trị CSDL

## Thông tin sinh viên
- Họ tên: Vũ Bảo Khánh  
- MSSV: K225480106028  
- Môn: Hệ quản trị cơ sở dữ liệu  
- Bài tập: Bài tập 05 - Trigger on MSSQL

---

# Phần A: Trình bày lại đầu bài đồ án Phân tích & Thiết kế Hệ thống

## 1. Mô tả bài toán
- **Tên đề tài**: Phân tích và thiết kế hệ thống Sổ liên lạc điện tử
- **Mục tiêu**: Xây dựng hệ thống giúp phụ huynh theo dõi điểm số, nhận xét học tập của học sinh từ cấp 1 đến cấp 3, mọi lúc mọi nơi qua internet.
- **Yêu cầu**:
  - Quản lý thông tin học sinh, lớp học, giáo viên chủ nhiệm.
  - Theo dõi kết quả học tập (điểm số thành phần, điểm thi).
  - Gửi nhận xét định kỳ từ giáo viên tới phụ huynh.
  - Tự động tổng hợp điểm trung bình các môn.
  - Tạo báo cáo nhanh chóng cho giáo viên và phụ huynh.

## 2. Cơ sở dữ liệu đồ án
- **Database**: SoLienLac_Database
- **Các bảng dữ liệu chính**:
  - **HocSinh** (`maHS`, `hoTen`, `ngaySinh`, `gioiTinh`, `diaChi`) — PK: `maHS`
  - **LopHoc** (`maLop`, `tenLop`, `khoi`) — PK: `maLop`
  - **GiaoVien** (`maGV`, `hoTen`, `ngaySinh`, `SDT`) — PK: `maGV`
  - **MonHoc** (`maMon`, `tenMon`) — PK: `maMon`
  - **BangDiem** (`id`, `maHS`, `maMon`, `diemTP`, `diemThi`) — PK: `id`, FK: `maHS`, `maMon`
  - **GVCN** (`maLop`, `maGV`, `namHoc`) — PK: (`maLop`, `namHoc`), FK: `maGV`
  - **NhanXet** (`idNX`, `maHS`, `maGV`, `noiDung`, `ngayNhanXet`) — PK: `idNX`, FK: `maHS`, `maGV`

- **Các ràng buộc**:
  - PK (Primary Key) cho từng bảng.
  - FK (Foreign Key) giữa các bảng liên quan: học sinh - lớp, học sinh - điểm, giáo viên - nhận xét.
  - CK (Check Constraint) như giới hạn điểm số từ 0 đến 10.

Dưới đây là hình ảnh hiển thị các bảng đã tạo:

![image](https://github.com/user-attachments/assets/e0bfa7d7-e539-43cb-baa9-efb5e9ee1fa2)

---

# Phần B: Nội dung bài tập 05

## 1. Trường phi chuẩn
- **Thêm trường**: `diemTB` (Điểm trung bình môn) vào bảng `BangDiem`.
- **Logic thêm**:
  - Tính điểm trung bình giữa `diemTP` (thành phần) và `diemThi` (thi cuối kỳ).
  - Khi có trường `diemTB`, việc lấy điểm tổng kết dễ hơn, nhanh hơn thay vì tính toán mỗi lần truy vấn.
  
## 2. Trigger

```sql
CREATE TRIGGER trg_UpdateDiemTB
ON BangDiem
AFTER INSERT, UPDATE
AS
BEGIN
    SET NOCOUNT ON;

    UPDATE BangDiem
    SET diemTB = CASE
                    WHEN diemTP IS NOT NULL AND diemThi IS NOT NULL THEN
                        (diemTP * 0.4 + diemThi * 0.6)
                    ELSE NULL
                 END
    FROM inserted i
    WHERE BangDiem.id = i.id;
END
```

> **Giải thích**:  
> - Trigger tự động tính `diemTB` = 40% điểm thành phần + 60% điểm thi cuối kỳ.
> - Update ngay khi có INSERT hoặc UPDATE điểm.

## 3. Nhập dữ liệu test
- Nhập dữ liệu ví dụ để ta có thể nhìn trigger 1 cách tổng quát
```sql
-- Sử dụng database
USE SoLienLac_Database;
GO

-- 1. Thêm dữ liệu bảng LopHoc
INSERT INTO LopHoc (maLop, tenLop, khoi) VALUES
('1A', N'Lớp 1A', 1),
('2B', N'Lớp 2B', 2),
('3C', N'Lớp 3C', 3);

-- 2. Thêm dữ liệu bảng HocSinh
INSERT INTO HocSinh (maHS, hoTen, ngaySinh, gioiTinh, diaChi) VALUES
('HS001', N'Lê Văn Nam', '2015-09-05', N'Nam', N'Hà Nội'),
('HS002', N'Nguyễn Thị Mai', '2014-04-20', N'Nữ', N'Hồ Chí Minh'),
('HS003', N'Phạm Anh Dũng', '2013-11-11', N'Nam', N'Đà Nẵng');

-- 3. Thêm dữ liệu bảng GiaoVien
INSERT INTO GiaoVien (maGV, hoTen, ngaySinh, SDT) VALUES
('GV001', N'Trần Thị Hoa', '1980-03-15', '0912345678'),
('GV002', N'Ngô Văn Minh', '1975-06-22', '0909876543');

-- 4. Thêm dữ liệu bảng MonHoc
INSERT INTO MonHoc (maMon, tenMon) VALUES
('MH001', N'Toán học'),
('MH002', N'Tiếng Việt'),
('MH003', N'Tiếng Anh');

-- 5. Thêm dữ liệu bảng GVCN
INSERT INTO GVCN (maLop, maGV, namHoc) VALUES
('1A', 'GV001', 2025),
('2B', 'GV002', 2025);

-- 6. Thêm dữ liệu bảng BangDiem
INSERT INTO BangDiem (maHS, maMon, diemTP, diemThi) VALUES
('HS001', 'MH001', 8.0, 9.0),
('HS001', 'MH002', 7.5, 8.5),
('HS002', 'MH001', 9.0, 9.5),
('HS002', 'MH003', 6.0, 7.0),
('HS003', 'MH002', 8.5, 9.0);

-- 7. Thêm dữ liệu bảng NhanXet
INSERT INTO NhanXet (maHS, maGV, noiDung, ngayNhanXet) VALUES
('HS001', 'GV001', N'Học sinh chăm ngoan, tiến bộ nhanh.', '2025-04-20'),
('HS002', 'GV002', N'Cần cố gắng nhiều hơn trong học tập.', '2025-04-21');
```
- Insert điểm thành phần, điểm thi cho vài học sinh.
- Check bảng `BangDiem` để xem `diemTB` tự tính đúng không.
- Dưới đây là kết quả khi nhập dữ liệu

![image](https://github.com/user-attachments/assets/4263def2-70c3-436f-89a6-2d8eb5533aca)

---

## 4. Kết luận
- **Trigger** giúp tự động hóa việc tính điểm tổng kết cho học sinh.
- **Giảm sai sót**, **tăng tốc độ** khi cần truy vấn điểm số.
- **Hiểu sâu hơn** về cách trigger hoạt động tự động sau mỗi thay đổi dữ liệu.
