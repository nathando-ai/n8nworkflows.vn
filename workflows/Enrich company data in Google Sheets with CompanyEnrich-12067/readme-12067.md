---
title: "🚀 Tự động làm giàu dữ liệu doanh nghiệp trong Google Sheets với CompanyEnrich"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy thông tin chi tiết doanh nghiệp từ tên miền, làm sạch dữ liệu và cập nhật trực tiếp vào Google Sheets."
slug: "tu-dong-lam-giau-du-lieu-doanh-nghiep-google-sheets-companyenrich"
tags: [n8n, automation, no-code, lead-generation, google-sheets, company-enrichment]
keywords: [n8n workflow, tự động hóa lead generation, CompanyEnrich API, làm giàu dữ liệu doanh nghiệp, google sheets automation]
---

# 🚀 Tự động làm giàu dữ liệu doanh nghiệp trong Google Sheets với CompanyEnrich

Trong các chiến dịch Sales và Marketing, việc tìm kiếm và cập nhật thủ công thông tin chi tiết (firmographic data) của hàng trăm doanh nghiệp tốn rất nhiều thời gian và công sức. Việc copy-paste thông tin doanh thu, quy mô nhân sự hay mạng xã hội vào Google Sheets dễ dẫn đến sai sót và mệt mỏi.

Workflow n8n này sẽ giải quyết triệt để bài toán trên bằng cách tự động hóa 100%: đọc tên miền từ Google Sheets, gọi API lấy thông tin từ CompanyEnrich, làm sạch dữ liệu và cập nhật ngược lại vào Google Sheets một cách chính xác mà không cần viết code phức tạp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian**: Không còn phải tra cứu thủ công thông tin từng công ty.
- **Dữ liệu luôn tươi mới**: Khai thác nguồn API chất lượng cao từ CompanyEnrich cho cả doanh nghiệp trong nước và quốc tế.
- **Tối ưu chi phí API**: Tự động lọc bỏ các dòng đã xử lý, tránh gọi API trùng lặp gây lãng phí.
- **Cấu trúc dữ liệu trực quan**: Tự động làm sạch và map dữ liệu lồng nhau thành các cột phẳng trong Google Sheets (`location_country_name`, `revenue`, `employees`,...).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản Google Sheets kết nối với n8n (OAuth2).
- Tài khoản và API Key từ **CompanyEnrich** để gọi dữ liệu doanh nghiệp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tạo một workflow mới trong n8n Editor, sau đó copy toàn bộ JSON của workflow này và dán trực tiếp vào màn hình làm việc của n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các node sau:

- **Get row(s) in sheet & Update row in sheet (`googleSheets`)**: 
  - Kết nối tài khoản Google Sheets của các sếp.
  - Nhập chính xác `Document` ID và `Sheet Name` của bảng tính quản lý danh sách công ty.
- **Filter (`filter`)**: 
  - Kiểm tra điều kiện lọc dữ liệu. Workflow mặc định sẽ lọc ra các dòng chưa có thông tin (`Status` trống hoặc chưa update) để tiết kiệm credit gọi API.
- **Fetch Company Data (`httpRequest`)**: 
  - Cấu hình endpoint API của CompanyEnrich và gắn API Key của các sếp vào phần Header (`Authorization` hoặc `x-api-key`).
  - Truyền tham số `domain` lấy từ Google Sheets vào request.
- **Data Cleaning (JS) (`code`)**: 
  - Node này dùng đoạn mã JavaScript để làm phẳng cấu trúc JSON phức tạp từ API (ví dụ: chuyển đổi `location.city.name` thành `location_city_name`) để khớp hoàn hảo với các cột trong Google Sheets.

#### Chuẩn bị cấu trúc Google Sheet:
Tạo một Google Sheet với các cột cơ bản sau:
1. `Domain` (Tên miền công ty cần tra cứu)
2. `Status` (Trạng thái: Done / Pending)
3. `Last Updated` (Thời gian cập nhật gần nhất)
4. **Các cột thông tin muốn lấy thêm**: `revenue`, `employees`, `socials_linkedin_url`, `location_country_name`,... (Tên cột tự do, node code sẽ tự động khớp tên trường từ API với tiêu đề cột nếu trùng khớp).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử với 1-2 dòng dữ liệu mẫu để kiểm tra kết quả trả về trong Google Sheets.
- Sau khi test thành công, bật nút **Active** để workflow chạy tự động theo lịch trình hoặc sự kiện.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp thông báo**: Thêm node Telegram hoặc Slack vào cuối chuỗi để nhận thông báo ngay khi workflow chạy xong danh sách khách hàng lớn.
- **Tự động hóa theo lịch (Cron)**: Thay thế node `When clicking ‘Execute workflow’` bằng `Schedule Trigger` để n8n tự động quét và làm giàu dữ liệu hàng ngày hoặc hàng tuần.
- **Log lỗi chi tiết**: Thêm nhánh xử lý lỗi (Error Trigger) để ghi nhận các domain lỗi/không tồn tại vào một sheet riêng biệt nhằm kiểm tra lại sau.

### 📌 Kết luận
Workflow tự động làm giàu dữ liệu doanh nghiệp với CompanyEnrich là mảnh ghép hoàn hảo giúp các đội ngũ Sales và Marketing tăng tốc độ xử lý dữ liệu đầu vào. Hãy triển khai ngay lên hệ thống n8n của các sếp để tối ưu hóa quy trình kinh doanh từ hôm nay!