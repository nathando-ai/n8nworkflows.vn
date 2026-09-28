---
title: "🚀 Tự động tìm LinkedIn URL của công ty hàng loạt với Apify & Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa tìm kiếm LinkedIn URL cho danh sách công ty từ Google Sheets sử dụng Apify Actor và lưu kết quả vào sheet mới."
slug: "tim-linkedin-url-cong-ty-voi-apify-google-sheets"
tags: [n8n, automation, lead-generation, apify, google-sheets, linkedin]
keywords: [n8n workflow, apify linkedin, tìm linkedin công ty, google sheets automation, lead generation]
---

# 🚀 Tự động tìm LinkedIn URL của công ty hàng loạt với Apify & Google Sheets

Các sếp có đang tốn hàng giờ đồng hồ để tìm kiếm thủ công từng trang LinkedIn của công ty khách hàng phục vụ cho việc Sales, tuyển dụng hay Marketing không? Việc tra cứu thủ công vừa chậm chạp, dễ sai sót, lại tốn kém nhân lực.

Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ, kết hợp giữa **Google Sheets** và **Apify Actor**, giúp tự động hóa 100% quy trình tìm kiếm LinkedIn Company URL chỉ bằng một cú click chuột!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chuyển đổi danh sách tên công ty thành các đường dẫn LinkedIn chính xác mà không cần copy/paste thủ công.
- **Tiết kiệm thời gian:** Xử lý hàng trăm, hàng ngàn dòng dữ liệu chỉ trong vài phút.
- **Dữ liệu sạch sẽ, đồng bộ:** Tự động tạo một Google Sheet mới chứa kết quả đã tìm thấy, giúp làm giàu dữ liệu (Data Enrichment) cho CRM hoặc danh sách outreach.
- **Đa dụng:** Phù hợp cho Sales Teams, Recruiters, Growth Marketers, và các Agency làm Lead Generation.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Google** (để kết nối Google Sheets).
- **Tài khoản Apify** và đã sử dụng/đăng ký Actor [LinkedIn Company URL Finder](https://apify.com/anchor/linkedin-company-url-finder) của tác giả Anchor.
- **Một Google Sheet đầu vào** chứa danh sách tên các công ty cần tìm kiếm (mỗi công ty 1 dòng).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, paste trực tiếp vào n8n Editor hoặc sử dụng template mã nguồn `10738` từ n8n.io.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 9 nodes chính hoạt động nhịp nhàng. Các sếp cần chú ý cấu hình các node sau:

- **`Get URLs from first sheet` (Google Sheets):** Kết nối tài khoản Google Sheets của các sếp (chọn `googleSheetsOAuth2Api`) để đọc danh sách công ty ban đầu.
- **`Set google sheet URL & original sheet name` (Set):** 
  - Mở node này và thay thế URL của Google Sheet mẫu bằng URL của file Google Sheet chứa danh sách công ty của các sếp.
  - Điền tên sheet nguồn chứa dữ liệu (ví dụ: `companies`).
  ```json
  [
   {
     "google_sheet_url": "YOUR_GOOGLE_SHEET_URL",
     "google_sheet_name": "companies"
   }
  ]
  ```
- **`Run Actor on Apify` & `Get Results from Apify` (Apify):** 
  - Kết nối Credentials tài khoản Apify (`apifyApi`).
  - Đảm bảo các sếp đã cấu hình Actor *LinkedIn Company URL Finder* trong tài khoản Apify của mình.
- **`Create new sheet for founded compnaies` & `Add company urls into the new Sheet` (Google Sheets):** Cấp quyền đọc/ghi Google Sheets để workflow có thể tự động tạo file sheet mới chứa kết quả trả về.

#### 3. Kích hoạt ⚡️
- Nhấn nút **`When clicking ‘Execute workflow’`** để test chạy thử với dữ liệu mẫu.
- Kiểm tra lại Google Drive xem sheet mới đã được tạo và điền dữ liệu chính xác chưa.
- Sau khi test thành công, bật **Active** để workflow sẵn sàng hoạt động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node **Slack** hoặc **Telegram** vào cuối workflow để nhận thông báo ngay khi Apify quét xong và tạo sheet mới.
- **Lên lịch chạy định động:** Thay thế node `manualTrigger` bằng `Schedule Trigger` để tự động hóa việc tìm kiếm hàng tuần/tháng.
- **Đẩy thẳng vào CRM:** Thay vì lưu ra Google Sheet mới, các sếp có thể cấu hình node cuối đẩy thẳng dữ liệu vào HubSpot, Close CRM hoặc PostgreSQL.

### 📌 Kết luận
Workflow này là một "vũ khí" hạng nặng giúp tối ưu hóa thời gian nghiên cứu thị trường và tìm kiếm khách hàng tiềm năng. Hãy cài đặt ngay hôm nay để giải phóng đội ngũ khỏi những công việc thủ công nhàm chán các sếp nhé!