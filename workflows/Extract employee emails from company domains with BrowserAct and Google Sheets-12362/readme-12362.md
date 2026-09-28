---
title: "🚀 Tự động trích xuất email nhân sự theo tên miền công ty với BrowserAct và Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động quét danh sách tên miền doanh nghiệp từ Google Sheets, sử dụng BrowserAct để tìm kiếm email nhân sự và lưu trữ kết quả."
slug: "trich-xuat-email-nhan-su-browseract-google-sheets"
tags: [n8n, automation, lead-generation, browseract, google-sheets, web-scraping]
keywords: [n8n workflow, trích xuất email, browseract, google sheets automation, lead generation, tự động hóa tìm kiếm khách hàng]
---

# 🚀 Tự động trích xuất email nhân sự theo tên miền công ty với BrowserAct và Google Sheets

Việc tìm kiếm thông tin liên hệ (email, chức vụ) của nhân sự tại các công ty mục tiêu để phục vụ cho các chiến dịch B2B Sales, Cold Outreach hay Lead Generation thường ngốn rất nhiều thời gian nếu làm thủ công. Các sếp thường phải copy từng tên miền, dán vào các công cụ tìm kiếm, sau đó lọc và nhập liệu bằng tay vào Excel.

Đừng tốn thời gian cho việc lặp đi lặp lại đó nữa! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực mạnh mẽ, tự động hóa 100% quy trình: đọc danh sách tên miền từ Google Sheets, sử dụng **BrowserAct** để cào dữ liệu email nhân sự thông qua Hunter.io, xử lý logic an toàn (phòng hờ CAPTCHA) và tự động lưu kết quả vào một database mới trên Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Quét hàng loạt tên miền công ty chỉ với một cú click kích hoạt (`Execute Manually`).
- **Lưu trữ khoa học:** Tự động tạo Google Sheet mới, thiết lập sẵn tiêu đề cột (Name, Email, Position) và ghi nhận dữ liệu theo từng dòng một cách ngăn nắp.
- **Xử lý thông minh & An toàn:** Tích hợp bộ lọc `Human verification Switch` cùng hệ thống cảnh báo qua Telegram (`Send Failure Alert`) nếu gặp CAPTCHA hoặc lỗi xác thực.
- **Báo cáo tức thì:** Gửi thông báo hoàn thành qua Slack (`Send Finishing Message`) ngay khi quét xong toàn bộ danh sách.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Google Sheets:** Kết nối OAuth2 để đọc/ghi dữ liệu.
- **Tài khoản BrowserAct:** Cần có BrowserAct API Key và chuẩn bị template **Company Domain to Email Enrichment** trên nền tảng BrowserAct.
- **Tài khoản Slack & Telegram:** Để nhận thông báo kết quả và cảnh báo lỗi (tuỳ chọn nhưng khuyến khích).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp, hoặc sử dụng tính năng copy/paste JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node sau để workflow chạy mượt mà:
- **Chuẩn bị Google Sheet nguồn:** Tạo một Google Sheet có tên `"Company URLs"`, trong đó dòng đầu tiên (Row 1) chứa tiêu đề `Company url`, các dòng tiếp theo là danh sách các tên miền công ty cần quét.
- **Node `Reading company data` (Google Sheets):** Trỏ tới file Google Sheet `"Company URLs"` vừa tạo để workflow lấy dữ liệu đầu vào.
- **Node `Domain-Specific Lead Extraction` & `Get Data From BrowserAct`:** Kết nối với tài khoản BrowserAct thông qua `browserActApi`. Đảm bảo sếp đã lưu template **Company Domain to Email Enrichment** trong tài khoản BrowserAct của mình.
- **Node `Human verification Switch`:** Kiểm tra logic rẽ nhánh nếu quá trình crawl gặp yêu cầu xác thực người dùng.
- **Node `Send Failure Alert` (Telegram) & `Send Finishing Message` (Slack):** Cấu hình Credentials tương ứng để nhận thông báo trạng thái.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để test thử với một vài domain mẫu trong Google Sheet.
- Kiểm tra kết quả hiển thị ở sheet mới được tự động tạo ra.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để sẵn sàng sử dụng lâu dài.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ dùng Slack/Telegram, các sếp có thể tích hợp thêm Webhook để đẩy dữ liệu lead trực tiếp về CRM như HubSpot, Notion hoặc Airtable.
- **Tối ưu tốc độ:** Điều chỉnh thông số ở node `Give Time to Complete Verification` (`wait`) và `Loop Over Items` (`splitInBatches`) cho phù hợp với tốc độ phản hồi của trang đích để tránh bị chặn IP.
- **Lưu log lỗi:** Thiết lập thêm một bảng ghi nhận các domain bị lỗi (không tìm thấy email hoặc bị CAPTCHA) để dễ dàng kiểm tra lại sau đó.

### 📌 Kết luận
Workflow tích hợp giữa n8n, BrowserAct và Google Sheets này là một "vũ khí" cực kỳ lợi hại cho các đội ngũ Sales và Marketing trong việc xây dựng danh sách khách hàng tiềm năng B2B một cách tự động và tiết kiệm thời gian tối đa. Hãy thiết lập ngay hôm nay và tối ưu hóa quy trình làm việc của các sếp!