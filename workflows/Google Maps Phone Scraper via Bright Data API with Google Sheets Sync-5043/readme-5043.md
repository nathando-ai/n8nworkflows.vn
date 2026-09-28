---
title: "🚀 Tự động quét số điện thoại từ Google Maps với Bright Data và Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu doanh nghiệp, số điện thoại từ Google Maps sử dụng Bright Data API và lưu trữ thẳng vào Google Sheets."
slug: "google-maps-phone-scraper-bright-data-google-sheets"
tags: [n8n, automation, no-code, bright-data, google-sheets, lead-generation, sales]
keywords: [n8n workflow, google maps scraper, bright data api, cào số điện thoại google maps, tự động hóa sales, google sheets n8n]
---

# 🚀 Tự động quét số điện thoại từ Google Maps bằng n8n & Bright Data

Việc tìm kiếm khách hàng tiềm năng (Lead Generation) từ Google Maps thủ công như copy tên, địa chỉ, số điện thoại, website... tốn vô số thời gian và công sức của đội ngũ sales. Chưa kể, việc này rất dễ nhàm chán và sai sót.

Giải pháp ở đây là gì? Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình: Nhập từ khóa và khu vực vào form -> Gửi yêu cầu cào dữ liệu qua Bright Data API -> Kiểm tra trạng thái -> Lấy kết quả và đồng bộ thẳng vào Google Sheets. Tất cả diễn ra hoàn toàn tự động mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Thay vì ngồi copy-paste thủ công từng doanh nghiệp, hệ thống cào hàng trăm kết quả chỉ trong vài phút.
- **Dữ liệu sạch & chuẩn xác:** Thu thập đầy đủ thông tin: Tên doanh nghiệp, số điện thoại, website, địa chỉ...
- **Tự động hóa hoàn toàn:** Chỉ cần nhập yêu cầu qua form, dữ liệu sẽ tự động đổ về Google Sheets sẵn sàng cho đội sales gọi điện chốt đơn.
- **Vận hành bền bỉ:** Cơ chế kiểm tra trạng thái và chờ thông minh giúp xử lý mượt mà các tập dữ liệu lớn từ Bright Data.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Tài khoản Bright Data:** Cần có tài khoản và API Key/Dataset ID để sử dụng dịch vụ cào dữ liệu Google Maps.
- **Google Sheets:** Một file Google Sheet được thiết kế sẵn các cột để lưu thông tin doanh nghiệp và kết nối qua Google OAuth2.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ n8n.io (Link gốc: [Workflow #5043](https://n8n.io/workflows/5043)), sau đó vào n8n Editor chọn **Import from File** hoặc copy và paste trực tiếp đoạn JSON vào workspace.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 8 nodes được sắp xếp logic. Các sếp cần cấu hình kỹ các điểm sau:

- **Form Trigger - Submit Location and Keywords:** Nơi người dùng nhập từ khóa ngành nghề (Ví dụ: `Spa`, `Coffee shop`) và khu vực (Ví dụ: `Hanoi`, `District 1`). Các sếp có thể tùy chỉnh thêm các trường thông tin trên Form nếu cần.
- **Bright Data API - Request Business Data & Check Scraping Status:** Node HTTP Request cấu hình kết nối tới Bright Data API. Các sếp cần điền `API Key` của Bright Data vào phần Header Authentication và đúng Dataset Trigger Endpoint.
- **Check If Status Ready & Wait Before Retry:** Cơ chế thông minh giúp kiểm tra xem Bright Data đã xử lý xong dữ liệu chưa. Nếu chưa (`False`), nó sẽ đi qua node **Wait** (chờ 1 phút) rồi quay lại kiểm tra tiếp, tránh việc lỗi do request quá sớm.
- **Save to Google Sheets:** Cấu hình tài khoản `googleSheetsOAuth2Api`, chọn file Google Sheet và Sheet Name tương ứng. Map các trường dữ liệu thu được từ Bright Data (Tên, SĐT, URL...) vào các cột trong Sheet.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Node** ở Form Trigger để test thử bằng một dữ liệu mẫu.
- Kiểm tra kết quả trên Google Sheets xem dữ liệu đã đổ về chuẩn chỉnh chưa.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để chính thức vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để bắn thông báo về nhóm Sales ngay khi quá trình quét dữ liệu hoàn tất.
- **Tự động làm sạch số điện thoại:** Kết hợp thêm các hàm JavaScript trong n8n để chuẩn hóa định dạng số điện thoại (ví dụ: chuyển `+84` thành `0`) trước khi lưu vào Google Sheets.
- **Gửi Email tự động:** Nối tiếp workflow này với một chuỗi Cold Email tự động gửi tài liệu giới thiệu dịch vụ tới các website thu thập được.

### 📌 Kết luận
Workflow **Google Maps Phone Scraper via Bright Data API** là một "vũ khí" cực mạnh cho các đội ngũ Sales, Marketing và Agency làm dịch vụ Local SEO. Hãy thiết lập ngay hôm nay để tự động hóa phễu tìm kiếm khách hàng tiềm năng của doanh nghiệp các sếp nhé!