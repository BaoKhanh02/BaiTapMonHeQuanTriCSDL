# Bài tập 04 của sinh viên: K225480106028 - Vũ Bảo Khánh - Môn Hệ quản trị CSDL

## Deadline: 23h59 NGÀY 15/4/2025

## ĐIỀU KIỆN: (ĐÃ LÀM XONG BÀI 3)

---

## BÀI TOÁN:

**Thiết kế và xây dựng cơ sở dữ liệu hệ thống Thời Khoá Biểu (TKB)**

### Yêu cầu:
1. **Tạo CSDL từ nguồn dữ liệu:**  
   Truy cập hệ thống [TMS.tnut.edu.vn](http://tms.tnut.edu.vn) để lấy dữ liệu thời khoá biểu mẫu (tên lớp, phòng, môn học, tiết, giờ vào, giờ ra, giảng viên...).

2. **Xây dựng các bảng dữ liệu theo chuẩn 3NF.**
   Các bảng thiết kế có thể bao gồm:
   - **GiaoVien**(`maGV`, `hoten`)

![image](https://github.com/user-attachments/assets/f12720bd-88a3-452e-a08f-030fb25b8510)

   - **MonHoc**(`maMon`, `tenMon`)

![image](https://github.com/user-attachments/assets/468cb70d-b17a-44f5-a103-13b726b20c1b)

   - **LopHoc**(`maLop`, `tenLop`)

![image](https://github.com/user-attachments/assets/a89eec49-9381-4d1b-a103-a583319c2a78)

   - **PhongHoc**(`maPhong`, `tenPhong`)

![image](https://github.com/user-attachments/assets/210fa9a8-860a-49b8-bff1-42242454eb42)

   - **THOIGIANHOC**(`maLichHoc`, `maGV`, `maMon`, `maLop`, `maPhong`, `thu`, `tietBatDau`, `soTiet`, `gioVao`, `gioRa`, `ngayHoc`)

![image](https://github.com/user-attachments/assets/cb53d9a0-0e60-40bf-9e73-1316906ba5ec)

3. **Nhập dữ liệu từ file Excel**:
   Dán trực tiếp từ Excel vào giao diện Edit Table trong SSMS.

---

## YÊU CẦU TRUY VẤN:

Viết câu lệnh truy vấn SQL để trả lời câu hỏi sau:

> Trong khoảng thời gian từ `@datetime1` đến `@datetime2`, có những giảng viên nào đang bận giảng dạy?

### Kết quả truy vấn gồm 4 cột:
- Họ tên giảng viên
- Môn học
- Giờ vào lớp
- Giờ ra lớp
```sql
SELECT GV.HoTen, MH.TenMon, TGH.GioVao, TGH.GioRa
FROM THOIGIANHOC TGH
JOIN GIAOVIEN GV ON TGH.MaGV = GV.MaGV
JOIN MONHOC MH ON TGH.MaMon = MH.MaMon
WHERE 
    TGH.NgayHoc BETWEEN '2025-03-01' AND '2025-03-30' AND
    '09:20' < TGH.GioRa AND
    '12:00' > TGH.GioVao;
```
---

## HÌNH THỨC LÀM BÀI:

1. **Tạo GitHub repo mới:**  
   Đặt tên repo liên quan đến bài tập ví dụ: `SQL_TKB_BaoKhanh`

2. **Tạo file `README.md` mô tả chi tiết:**  
   - Paste các ảnh chụp quá trình thao tác
   - Ghi chú giải thích bên dưới từng ảnh

3. **Sinh file script:**
   - `bai_tap_4_schema.sql`: cấu trúc cơ sở dữ liệu (Tasks → Generate Scripts)
   - `bai_tap_4_data.sql`: dữ liệu đã nhập (chọn “Data only” trong Generate Scripts)

4. **Vẽ sơ đồ Diagram thể hiện các quan hệ PK, FK**  
   - Chụp ảnh sơ đồ ERD
   - Dán ảnh và mô tả rõ các quan hệ 1 - nhiều

5. **Cam kết (commit) đầy đủ lên GitHub:**
   - `README.md`
   - `bai_tap_4_schema.sql`
   - `bai_tap_4_data.sql`
   - ảnh sơ đồ Diagram

![image](https://github.com/user-attachments/assets/1a1cc376-8f65-4402-963a-456b5553b957)
