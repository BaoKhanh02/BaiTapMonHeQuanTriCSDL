# Bài tập 02 của sinh viên: K225480106028 - Vũ Bảo Khánh - Môn Hệ quản trị CSDL

## Deadline: 23h59 NGÀY 25/3/2025

## ĐIỀU KIỆN: (ĐÃ LÀM XONG BÀI 1)
1. Đã cài đặt SQL Server 2022 Dev.
2. Đã cài đặt SQL Managerment Studio bản mới nhất.
3. Đã kết nối từ SQL Managerment Studio vào SQL Server.
4. Đã có tài khoản github, biết cách tạo repository(kho lưu trữ) cho phép truy cập public.

## BÀI TOÁN:
Tạo csdl quan hệ với tên QLSV gồm các bảng sau:
  1,  SinhVien(#masv,hoten,NgaySinh)
  2,  Lop(#maLop,tenLop)
  3,  GVCN(#@maLop,#@magv,#HK)
  4,  LopSV(#@maLop,#@maSV,ChucVu)
  5,  GiaoVien(#magv,hoten,NgaySinh,@maBM)
  6,  BoMon(#MaBM,tenBM,@maKhoa)
  7,  Khoa(#maKhoa,tenKhoa)
  8,  MonHoc(#mamon,Tenmon,STC)
  9,  LopHP(#maLopHP,TenLopHP,HK,@maMon,@maGV)
  10, DKMH(#@maLopHP,#@maSV,DiemTP,DiemThi,PhanTramThi)

## Yêu cầu
1. Thực hiện các hành động sau trên giao diện đồ hoạ để tạo cơ sở dữ liệu cho bài toán:
  + Tạo database mới, mô tả các tham số(nếu có) trong quá trình.
  + Tạo các bảng dữ liệu với các trường như mô tả, chọn kiểu dữ liệu phù hợp với thực tế (tự tìm hiểu)
  + Mỗi bảng cần thiết lập PK, FK(s) và CK(s) nếu cần thiết. (chú ý dấu # và @: # là chỉ PK, @ chỉ FK)
2. Chuyển các thao tác đồ hoạ trên thành lệnh SQL tương đương. lưu tất cả các lệnh SQL trong file: Script_DML.sql

## HÌNH THỨC LÀM BÀI:
1. Tạo repository mới, tạo file readme.md (có hướng dẫn trên zalo group)
2. Sinh viên thao tác trên máy tính cá nhân, chụp màn hình quá trình làm, chỉ cần chụp active window, thi thoảng chụp full màn hình để thấy sự cá nhân hoá.
3. Hình sau khi chụp paste trực tiếp vào file readme trên github, cần mô tả các phần trên ảnh để tỏ ra là hiểu hết!
4. upload các file liên quan: Script_DML.sql
5. Update link của repository vào cột bài tập 2 trên file excel online của thầy (đã ghim link trên zalo group)

## Chú ý:
1. Được phép dùng AI và tham khảo bài của bạn, nhưng phải có sự khác biệt đáng kể.
2. Nghiêm cấm copy, clone. Tham khảo và copy là 2 việc khác hẳn nhau. Thầy có tool để check!
3. Bài làm phải có dấu ấn cá nhân (hãy sáng tạo và biết cách bảo vệ mình nếu bạn là bản chính)
4. Kết quả AI phải phù hợp với yêu cầu, nếu quá sai lệch <=> sv ko đọc => Cấm thi
5. Nên nhớ: cấm thi là ko có vùng cấm và thầy chưa bao giờ nói đùa về việc cấm thi.

# Bài Làm
![1](https://github.com/user-attachments/assets/9ab7cb68-4073-4452-9d6e-09ef72b3a904)

Cơ sở dữ liệu quan hệ với tên "QLSV" gồm các bảng sau:
  
  1,  SinhVien(#masv,hoten,NgaySinh)

![2](https://github.com/user-attachments/assets/ce60b13e-7b4a-445a-9cba-9de8c1766004)

Bảng Sinh viên bao gồm: Mã sinh viên (Khóa Chính), Họ và tên, Ngày sinh

![3](https://github.com/user-attachments/assets/5b008a03-f5c3-4b99-a5f5-077846c1cf58)

Mối quan hệ giữa các bảng với bảng Sinh viên với mã sinh viên là khóa ngoại của các bảng khác

![4](https://github.com/user-attachments/assets/2aa995d8-b091-4d5e-b245-c2b785fa1c16)

Đặt ràng buộc trong bảng Sinh viên

  2,  Lop(#maLop,tenLop)

![5](https://github.com/user-attachments/assets/d6841882-fb90-41d5-8f0b-0e18b8ec3c7c)

Tương tự như bảng Sinh viên

![6](https://github.com/user-attachments/assets/0c09de69-2b4b-4640-95d7-e4ea6ce7c557)

Mối quan hệ giữa bảng Lớp với các bảng khác
  
  3,  GVCN(#@maLop,#@magv,#HK)

![7](https://github.com/user-attachments/assets/39a934fd-c981-4329-88ad-a9b6f1214287)

![8](https://github.com/user-attachments/assets/2a08b944-5f33-4872-9170-e9ec1eb00419)

  4,  LopSV(#@maLop,#@maSV,ChucVu)

![9](https://github.com/user-attachments/assets/fa87566b-7661-4ca4-9a7a-5e9d0e7845cd)

![10](https://github.com/user-attachments/assets/42d415ea-49aa-43f7-b1a7-d8bbdf80ea51)

  5,  GiaoVien(#magv,hoten,NgaySinh,@maBM)

![11](https://github.com/user-attachments/assets/66501ad1-ad30-427a-b9f6-2ab7895e9f4a)

![12](https://github.com/user-attachments/assets/19ccd00c-5d1b-4a05-a909-4756c70cf455)

  6,  BoMon(#MaBM,tenBM,@maKhoa)

![13](https://github.com/user-attachments/assets/2ba25d0b-c43b-4390-93fc-2a4ce34f2d61)

![14](https://github.com/user-attachments/assets/0e6bc00d-9213-4666-b2ae-7b554676e1d5)

  7,  Khoa(#maKhoa,tenKhoa)

![15](https://github.com/user-attachments/assets/d8c749f3-1cee-4f5f-a768-6559e3defb6a)

![16](https://github.com/user-attachments/assets/a440021d-4dd4-470e-a145-d8136b9bd5c6)

  8,  MonHoc(#mamon,Tenmon,STC)

![17](https://github.com/user-attachments/assets/1f82bed3-aa3c-4c6b-8971-aa7db089bb82)

  9,  LopHP(#maLopHP,TenLopHP,HK,@maMon,@maGV)

![18](https://github.com/user-attachments/assets/05595b0d-630c-405e-bd5c-939e1ae9610e)

  10, DKMH(#@maLopHP,#@maSV,DiemTP,DiemThi,PhanTramThi)

![19](https://github.com/user-attachments/assets/e9bf301a-5df4-43d6-8a77-312bd133609a)

![20](https://github.com/user-attachments/assets/c6f24981-36c4-48c3-84c1-e041e887c4ca)

