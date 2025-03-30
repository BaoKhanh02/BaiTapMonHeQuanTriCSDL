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

