---
title: "🚀 Tự động tạo từ khóa SEO và lấy lượng tìm kiếm với Google Ads API qua n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa việc sinh từ khóa SEO mới và lấy dữ liệu lượng tìm kiếm hằng tháng (search volume) sử dụng Google Ads API và lưu vào Google Sheets."
slug: "tu-dong-tao-tu-khoa-seo-google-ads-api-n8n"
tags: [n8n, automation, google-ads, seo, marketing, google-sheets]
keywords: [n8n workflow, google ads api, tao tu khoa seo, tu dong hoa marketing, search volume keywords]
---

# 🚀 Tự động tạo từ khóa SEO và lượng tìm kiếm với Google Ads API

Các sếp làm SEO hay chạy quảng cáo Google Ads chắc chắn hiểu cảm giác "đau đầu" khi phải ngồi hàng giờ nghiên cứu từ khóa, kiểm tra lượng tìm kiếm (Search Volume) thủ công cho từng từ một. Việc này không chỉ tốn thời gian mà còn dễ bỏ sót những cơ hội từ khóa tiềm năng.

Workflow n8n này do chuyên gia **Imperol** xây dựng chính là "vũ khí bí mật" giúp các sếp tự động hóa 100% quy trình: Nhận danh sách từ khóa gốc, gọi trực tiếp vào **Google Ads API** để sinh ra hàng loạt từ khóa liên quan kèm theo số liệu lượng tìm kiếm hằng tháng, sau đó tự động lưu trữ gọn gàng vào **Google Sheets**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chỉ cần cấp danh sách từ khóa hạt giống (seed keywords), hệ thống tự lo phần còn lại.
- **Dữ liệu chuẩn xác từ Google:** Khai thác trực tiếp từ kho dữ liệu Google Ads thông qua API chính thống.
- **Tiết kiệm 90% thời gian:** Không còn cảnh copy-paste thủ công giữa Google Keyword Planner và file Excel.
- **Dễ dàng mở rộng:** Dữ liệu sau khi thu thập có thể đẩy tiếp về Slack, Telegram hoặc Email để đội ngũ content nắm bắt ngay.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Ads Account:** Tài khoản Google Ads có quyền truy cập API (Developer Token, Customer ID, Login Customer ID) và cấu hình `googleAdsOAuth2Api`.
- **Google Sheets Account:** Kết nối `googleSheetsOAuth2Api` để lưu trữ dữ liệu.
- **Google Sheet Mẫu:** [Tạo bản sao Google Sheets tại đây](https://docs.google.com/spreadsheets/d/10mXXLB987b7UySHtS9F4EilxeqbQjTkLOfMabnR2i5s/edit?usp=sharing) để đồng bộ cấu trúc cột.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow và paste trực tiếp vào n8n Editor của mình, hoặc import file JSON tải về từ nguồn gốc. Workflow bao gồm 6 nodes chính:
- **Trigger** (`executeWorkflowTrigger`): Điểm khởi chạy workflow (có thể thay đổi thành Webhook hoặc Manual).
- **Set Keywords** (`set`): Nơi tiếp nhận và thiết lập danh sách từ khóa đầu vào.
- **Generate new keywords** (`httpRequest`): Gửi request đến Google Ads API để lấy ý tưởng từ khóa và search volume.
- **Split Out** (`splitOut`): Tách mảng dữ liệu trả về từ API thành các item riêng lẻ.
- **Edit Fields** (`set`): Chuẩn hóa và lọc lấy các trường dữ liệu cần thiết (từ khóa, lượng tìm kiếm trung bình...).
- **Upsert** (`googleSheets`): Đẩy dữ liệu đã xử lý vào Google Sheets.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node Trigger:** Mặc định là `Execute Workflow Trigger`. Các sếp có thể thay thế bằng Webhook, Schedule hoặc Manual Trigger tùy theo nhu cầu vận hành thực tế.
- **Node Set Keywords:** Đảm bảo dữ liệu đầu vào truyền vào node này có định dạng mảng (`array`) và chứa cột tên là `Keyword`.
- **Node Generate new keywords (HTTP Request):** 
  - Cập nhật `{customer_id}` trực tiếp trên URL: `https://googleads.googleapis.com/v18/customers/{customer-id}:generateKeywordIdeas`
  - Cấu hình Header với các thông tin xác thực:
    - `content-type`: `application/json`
    - `developer-token`: `{developer-token của sếp}`
    - `login-customer-id`: `{login-customer-id của sếp}`
  - Cấu hình JSON Body phù hợp với vị trí địa lý (`geoTargetConstants`), ngôn ngữ (`language`) và từ khóa hạt giống (`keywordSeed`).
- **Node Upsert (Google Sheets):** Chọn credential Google Sheets, trỏ đến file Google Sheet đã sao chép ở phần chuẩn bị và chọn thao tác `Append` (hoặc Upsert dựa trên tên từ khóa).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một vài từ khóa mẫu để kiểm tra kết quả trả về ở từng node.
- Sau khi dữ liệu đổ về Google Sheets chính xác, bật công tắc **Active** để đưa workflow vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack ngay sau node Google Sheets để bot gửi thông báo *"Đã nghiên cứu xong X từ khóa mới"* về group chat cho team content.
- **Lập lịch tự động:** Thay thế Trigger bằng Cron/Schedule Node để hệ thống tự động quét từ khóa mới hàng tuần/hàng tháng theo chiến dịch SEO.
- **Lọc từ khóa thông minh:** Thêm một node Code (JavaScript) sau node Split Out để lọc bỏ các từ khóa có lượng tìm kiếm quá thấp (ví dụ < 10) nhằm tối ưu chất lượng data lưu trữ.

### 📌 Kết luận
Việc tự động hóa nghiên cứu từ khóa với Google Ads API và n8n sẽ giúp các sếp tiết kiệm nguồn lực đáng kể, đồng thời duy trì lợi thế cạnh tranh với lượng dữ liệu từ khóa luôn được cập nhật liên tục. Hãy "lên đồ" ngay cho hệ thống của mình nhé!