# Bài tập 03 của sinh viên: K225480106028 - Vũ Bảo Khánh - Môn Hệ quản trị CSDL

## Deadline: 23h59 NGÀY 30/3/2025

## ĐIỀU KIỆN: (ĐÃ LÀM XONG BÀI 2)

## BÀI TOÁN:
Sửa bài 02 để có csdl như sau:

  1,  SinhVien(#masv,hoten,NgaySinh)
  
  2,  Lop(#maLop,tenLop)
  
  3,  GVCN(#@maLop,#@magv,#HK)
  
  4,  LopSV(#@maLop,#@maSV,ChucVu)
  
  5,  GiaoVien(#magv,hoten,NgaySinh,@maBM)
  
  6,  BoMon(#MaBM,tenBM,@maKhoa)
  
  7,  Khoa(#maKhoa,tenKhoa)
  
  8,  MonHoc(#mamon,Tenmon,STC)
  
  9,  LopHP(#maLopHP,TenLopHP,HK,@maMon,@maGV)
  
  10, DKMH(#id_dk,#@maLopHP,#@maSV,DiemThi,PhanTramThi)
  
  11, Diem(#id, @id_dk, diem)

## Yêu cầu
1. Sửa bảng DKMH và bảng Điểm từ bài tập 2 để có các bảng như yêu cầu.
2. Nhập dữ liệu demo cho các bảng (nhập có kiểm soát từ tính năng Edit trên UI của mssm)
3. Viết lệnh truy vấn để: Tính được điểm thành phần của 1 sinh viên đang học tại 1 lớp học phần.

## HÌNH THỨC LÀM BÀI:
1. Tạo file bai_tap3.md trên cùng repository của bài tập 2:
   Nội dung chứa đề bài, và ảnh chụp quá trình thao tác các yêu cầu khác.
2. Chụp ảnh quá trình sửa bảng DKMH và quá trình thêm bảng Diem, chú ý @ là FK, và thêm CK cho trường điểm
3. Hình sau khi chụp paste trực tiếp vào file bai_tap3.md trên github, cần mô tả các phần trên ảnh để tỏ ra là hiểu hết!
4. dùng tính năng: Tasks -> Generate Scrips => sinh ra file: bai_tap_3_schema.sql  (chỉ chứa lệnh tạo cấu trúc của db)
5. dùng tính năng: Tasks -> Generate Scrips => advance => Check Data only => sinh ra file: bai_tap_3_data.sql  (chỉ chứa dữ liệu đã nhập demo vào db)
6. Tạo diagram mô tả các PK, FK của db. Chụp hình kết quả các bảng có các đường nối 1-->nhiều
7. upload 2 file  bai_tap_3_schema.sql và bai_tap_3_data.sql lên repository.
8. nhớ commit để save nội dung file bai_tap3.md

## Bài làm

#### 1. Sửa bảng DKMH và bảng Điểm từ bài tập 2 để có các bảng như yêu cầu.
![image](https://github.com/user-attachments/assets/6ab213dd-c72b-4433-b14d-41d4b9dcd3f3)

![image](https://github.com/user-attachments/assets/eb14bf11-90a7-4a4a-bc94-bc70059716e1)

Đã chỉnh sửa bảng DKMH và thêm bảng Điểm

#### 2. Nhập dữ liệu demo cho các bảng (nhập có kiểm soát từ tính năng Edit trên UI của mssm).

![image](https://github.com/user-attachments/assets/4340348f-95f3-41ab-8fdf-ccc777fce106)

Dữ liệu demo của các bảng DKMH, Bộ môn, Giáo viên, Điểm

![image](https://github.com/user-attachments/assets/3b766a42-33a1-4745-a48e-d311ada7496b)

Dữ liệu demo của các bảng Khoa, Lớp, Lớp học phần, Lớp sinh viên

![image](https://github.com/user-attachments/assets/ccbb78ca-c2c1-4b23-9b7a-3e3d0534c2f7)

Dữ liệu demo của các bảng Môn học, Sinh viên

#### 3. Viết lệnh truy vấn để: Tính được điểm thành phần của 1 sinh viên đang học tại 1 lớp học phần.

SELECT SV.masv, SV.hoten, LHP.TenLopHP, D.DiemTP
FROM SinhVien SV
JOIN DKMH DK ON SV.masv = DK.maSV
JOIN LopHP LHP ON DK.maLopHP = LHP.maLopHP
JOIN Diem D ON DK.id_dk = D.id_dk
WHERE SV.masv = 'SV001' AND LHP.maLopHP = 'LHP001';

![image](https://github.com/user-attachments/assets/73952838-8879-4feb-a6d1-5b6b4fc42409)

Kết quả của lệnh truy vấn 

##### Chú thích.

SELECT là lựa chọn. Sau SELECT thường là:
                                           - 1 hoặc nhiều trường dữ liệu (hay còn gọi là các cột).
                                           - Tất cả dữ liệu trong bảng.
                                           - Dữ liệu từ nhiều bảng.
                                           - Dữ liệu có điều kiện.
COALESCE: hàm sử dụng một dữ liệu để trả về giá trị không NULL.
FROM chỉ ra bảng chứa dữ liệu mà SELECT truy vấn.
JOIN (INNER JOIN) dùng để kết hợp 2 hoặc nhiều bảng dựa trên một điều kiện chung. Biểu thức chung: FROM <Tên bảng> JOIN <Tên bảng> ON <Biểu thức>;
LEFT JOIN: Lấy hết bảng bên trái và phần dữ liệu chung. Nhưng dữ liệu nào bảng bên phải không có thì hiển thị NULL.
WHERE dùng để lọc dữ liệu theo một điều kiện nào đó

Ngoài ra ở phần JOIN còn có RIGHT JOIN (Ngược lại của LEFT JOIN), FULL JOIN(Lấy cả 2 bảng nhưng phần nào không có thì hiển thị NULL)
