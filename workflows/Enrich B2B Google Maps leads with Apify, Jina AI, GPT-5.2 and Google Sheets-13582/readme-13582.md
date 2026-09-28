---
title: "🚀 Tự Động Quét & Làm Sạch Leads B2B Từ Google Maps với Apify, Jina AI, GPT và Google Sheets qua Telegram"
description: "Xây dựng hệ thống tìm kiếm và làm giàu dữ liệu B2B tự động từ Google Maps, cào website bằng Jina AI, phân tích bằng OpenAI GPT và lưu trữ gọn gàng vào Google Sheets, điều khiển trực tiếp qua Telegram."
slug: "tu-dong-quet-lam-sach-leads-b2b-google-maps-apify-jina-ai-gpt-google-sheets"
tags: [n8n, automation, lead-generation, google-maps, openai, apify, google-sheets]
keywords: [n8n workflow, cào lead google maps, apify n8n, jina ai n8n, tự động hóa b2b lead generation, làm giàu dữ liệu khách hàng]
---

# 🚀 Tự Động Quét & Làm Sạch Leads B2B Từ Google Maps qua Telegram

Các sếp có đang tốn hàng giờ để tìm kiếm khách hàng tiềm năng trên Google Maps, copy-paste thủ công từng thông tin tên công ty, số điện thoại, website rồi lại lọ mọ tìm email từng trang web một? Việc này vừa nhàm chán, tốn thời gian lại cực kỳ dễ sai sót.

Đừng lo, workflow n8n cực đỉnh này sẽ giúp các sếp tự động hóa 100% quy trình: **Nhận yêu cầu qua Telegram ➔ Quét Google Maps bằng Apify ➔ Lọc trùng lặp ➔ Tổng hợp thông tin bằng OpenAI GPT ➔ Cào nội dung website bằng Jina AI ➔ Trích xuất email liên hệ ➔ Lưu trọn gói vào Google Sheets và thông báo khi hoàn tất!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ sập giữa chừng khi xử lý danh sách hàng trăm leads, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Chỉ cần gửi tin nhắn qua Telegram theo cú pháp, hệ thống tự động cào và làm sạch dữ liệu.
- **Làm giàu dữ liệu thông minh (Data Enrichment):** Không chỉ có tên và địa chỉ, AI còn viết tóm tắt ngắn gọn về doanh nghiệp và tự động tìm email chính xác từ website của họ.
- **Đồng bộ thời gian thực:** Toàn bộ thông tin được đẩy thẳng vào Google Sheets, sẵn sàng để đội sales tiếp cận.
- **Kiểm soát thông minh:** Có cơ chế chống trùng lặp (`Deduplicate Places`) và quản lý giới hạn tốc độ (`Wait Rate Limit`) để tránh bị block IP hoặc quá tải API.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Telegram Bot Token** (tạo qua `@BotFather`).
- **Apify Account & API Key** (để chạy actor cào dữ liệu Google Maps).
- **OpenAI API Key** (dùng cho các node `Generate Company Summary` và `Extract Website Email`).
- **Jina AI API Key** (để trích xuất nội dung website cực nhanh và sạch).
- **Google Sheets** (tạo sẵn một file Google Sheets để lưu leads).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy toàn bộ mã JSON từ n8n, sau đó paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thông số tại các node trọng điểm sau:
- **Receive Telegram Input (`telegramTrigger`)**: Kết nối với Telegram Bot Credentials của các sếp. Node này nhận tin nhắn theo cú pháp: `sector; limit; mapsUrl` (Ví dụ: `Coffee shop; 20; https://www.google.com/maps/search/...`).
- **Run Maps Scraper & Fetch Dataset Items (`@apify/n8n-nodes-apify.apify`)**: Cấu hình Apify API Credentials và chọn Google Maps Scraper Actor phù hợp.
- **Upsert Places to Sheet & Update Email in Sheet (`googleSheets`)**: Kết nối tài khoản Google Sheets, trỏ tới file Google Sheet ID và chọn đúng tên Sheet của các sếp.
- **Generate Company Summary & Extract Website Email (`openAi`)**: Cấu hình OpenAI API Credentials, chọn model (ví dụ `gpt-4o` hoặc `gpt-4o-mini`) và tinh chỉnh prompt nếu muốn AI tóm tắt theo văn phong riêng.
- **Fetch Website Content (`jinaAi`)**: Nhập Jina AI API Key để hệ thống tự động đọc nội dung trang web của các doanh nghiệp tìm được.

#### 3. Kích hoạt ⚡️
- Chạy thử một request nhỏ (ví dụ limit 5 leads) bằng cách nhắn tin qua Telegram bot để test luồng.
- Sau khi kiểm tra dữ liệu trả về trong Google Sheets chính xác, gạt công tắc sang chế độ **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ gửi thông báo `DONE` qua Telegram, các sếp có thể nối thêm node gửi tin nhắn vào kênh Slack của team kinh doanh.
- **Lưu lịch sử chạy:** Thêm một bước ghi log thời gian và số lượng leads quét được vào một sheet riêng để dễ dàng theo dõi hiệu suất chiến dịch marketing.
- **Tích hợp CRM:** Nối tiếp workflow bằng việc đẩy dữ liệu từ Google Sheets thẳng vào các CRM như HubSpot, Close, hoặc Pipedrive để đội Sales gọi điện ngay lập tức.

### 📌 Kết luận
Workflow này là một "vũ khí tối thượng" cho các đội ngũ Growth Hacking, Sales B2B và Marketing Agency. Thay vì tốn hàng chục triệu đồng cho các tool trả phí đắt đỏ, các sếp hoàn toàn có thể tự dựng một con bot quét lead siêu thông minh, chạy 24/7 với chi phí gần như bằng 0. Cài ngay kẻo lỡ các sếp nhé!