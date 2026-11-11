# BÀI LÀM – HACKATHON 02

- **Mã đề:** 02
- **Họ tên:** Nguyễn Trần Đan Linh
- **Lớp:** HCMK26_CNTT1
- **Link repository:** https://github.com/HCM-K26-CNTT1/HCM-K26-CNTT1_Nhap-mon-CNTT_Hackathon02.git
- **Hệ điều hành (Windows/macOS):** Windows

## 4.2. Thao tác máy tính cơ bản bằng CLI

### Các lệnh đã chạy

```shell
cd D:\starter-kit\bai-xe-website
pwd
ls -Force
mv .\huong_dan_van_hanh.txt .\docs\
mkdir backup
cp .\data\luot_gui_xe_thang_2.xlsx .\backup\
rm *.tmp
cd .\logs\
ls 
cd ..
gci -Recurse -Force



```

### Kết quả liệt kê toàn bộ dự án (Windows: Get-ChildItem -Recurse -Force; macOS: ls -aR)

```text
    Directory: D:\starter-kit\bai-xe-website


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----        11/11/2026   7:57 AM                backup
d-----        11/11/2026   7:52 AM                data
d-----        11/11/2026   7:55 AM                docs
d-----        11/11/2026   7:51 AM                evidence
d-----        11/11/2026   7:52 AM                logs
d-----        11/11/2026   7:50 AM                web
------         11/3/2026   7:06 AM             73 .env
-a----         11/3/2026   7:06 AM           2412 bai_lam.md


    Directory: D:\starter-kit\bai-xe-website\backup


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----         11/3/2026   7:06 AM           6132 luot_gui_xe_thang_2.xlsx


    Directory: D:\starter-kit\bai-xe-website\data


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----         11/3/2026   7:06 AM           6132 luot_gui_xe_thang_2.xlsx


    Directory: D:\starter-kit\bai-xe-website\docs


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----         11/3/2026   7:06 AM            155 huong_dan_van_hanh.txt


    Directory: D:\starter-kit\bai-xe-website\logs


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----         11/3/2026   7:06 AM            977 gate.log


    Directory: D:\starter-kit\bai-xe-website\web


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----        11/11/2026   7:50 AM                images
------         11/3/2026   7:06 AM            600 app.js
------         11/3/2026   7:06 AM            533 index.html
------         11/3/2026   7:06 AM            460 style.css


    Directory: D:\starter-kit\bai-xe-website\web\images


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
------         11/3/2026   7:06 AM           3089 logo-parkeasy.png
```

## 4.3. Lọc log truy cập website

### a) Lệnh lọc các dòng status=500

```shell
 Select-String "status=500" .\logs\gate.log > .\logs\loi_500.txt

```

### 2 dòng đầu tiên trong logs/loi_500.txt

```text
logs\gate.log:3:2026-02-28 08:08:39 POST /api/cho-trong status=500
logs\gate.log:7:2026-02-28 08:23:23 POST /api/cho-trong status=500

```

### b) Lệnh đếm số dòng status=404 và kết quả

```shell
 (Get-Content .\logs\gate.log | Select-String "status=404").Count

```

```text
4

```

## 4.4. Chạy script tong_hop (.ps1 hoặc .sh)

### Lệnh chạy (Windows: nếu dùng Phụ lục 2 thì ghi cả 2 lệnh)

```shell
> @'
>> # Script: tong_hop.ps1
>> # Tac gia: Nguyen Tran Dan Linh
>> # Ngay tao: 11-11-2026
>> Write-Host "Dang tao bao cao..."
>> "=== BAO CAO SU CO WEBSITE ===" > logs/tong_hop.txt
>> Get-Content logs/gate.log | Select-String "status=404" >> logs/tong_hop.txt
>> Get-Content logs/gate.log | Select-String "status=500" | Measure-Object >> logs/tong_hop.txt
>> Write-Host "Hoan thanh!"
>> '@ | Set-Content tong_hop.ps1

.\tong_hop.ps1

Get-Content .\logs\tong_hop.txt
```

### Nội dung file logs/tong_hop.txt

```text
=== BAO CAO SU CO WEBSITE ===

2026-02-28 08:12:50 GET /tin-tuc status=404
2026-02-28 08:31:56 GET /images/so-do-bai.jpg status=404
2026-02-28 08:36:18 GET /images/so-do-bai.jpg status=404
2026-02-28 08:47:02 GET /tin-tuc status=404




Count    : 6
Average  :
Sum      :
Maximum  :
Minimum  :
Property :

```

## 4.5. README.md và bảo vệ thông tin bí mật

> README.md, .gitignore và .env.example được chấm trực tiếp trên file ở gốc dự án. Đánh dấu `[x]` vào các mục đã làm để tự kiểm tra.

- [X] README.md: Heading 1, mô tả có **in đậm** và *in nghiêng*, bảng, code block, task list, blockquote
- [X] .gitignore có dòng `.env` (tên file đúng, không có đuôi .txt)
- [X] .env.example có đủ tên biến, giá trị để trống (tên file đúng, không có đuôi .txt)

## 4.6. Kiểm tra trang web bằng DevTools (F12) và báo cáo lỗi

### Bảng lỗi

| STT | Tab DevTools phát hiện lỗi | Tên file hoặc thông báo lỗi | Cách khắc phục |
| --- | --- | --- | --- |
| 1 | Không tìm thấy đường dẫn |  GET file:///D:/starter-kit/bai-xe-website/web/images/logo.jpg net::ERR_FILE_NOT_FOUND | Thay đúng tên file ảnh  |
| 2 | Sai tên bảng | app.js:18 Uncaught ReferenceError: hienThiGiaGui is not defined
(anonymous)	@	app.js:18 | Sửa "hienThiBangGiaGui" ở code js thành "hienthiGiaGui"  |

> Ảnh chụp màn hình lưu trong thư mục `evidence/` (network.png, console.png).

### Báo cáo lỗi gửi trưởng nhóm

- **Context:** Bạn ơi, mình đang làm trang web bằng Javascript nhưng bị lỗi giá trị bảng ở tab Console
- **Expected:** Mình muốn sửa cho trang web hiển thị bảng giá gửi
- **Actual:** Mình có tìm kiếm thử trên mạng cách sửa lỗi và tự sửa lỗi nhưng không sửa được
- **Log:** Nguyên văn dòng lỗi: "app.js:18 Uncaught ReferenceError: hienThiGiaGui is not defined"
và "chụp màn hình dòng lỗi"

### Câu tìm kiếm Google

```text
site:stackoverflow.com "app.js:18 Uncaught ReferenceError: hienThiGiaGui is not defined" -quangcao
```

## 4.7. Excel

> Phần Excel được chấm trực tiếp trên file `data/luot_gui_xe_thang_2.xlsx`, không cần ghi vào đây.
