---
title: "🚀 Tự động quét Lead từ Google Maps và trích xuất thông tin liên hệ Impressum bằng AI"
description: "Hướng dẫn xây dựng workflow n8n tự động tìm kiếm doanh nghiệp trên Google Maps, cào trang Impressum và dùng OpenAI trích xuất thông tin người ra quyết định, email, số điện thoại lưu vào Airtable."
slug: "google-maps-airtable-lead-scraper-gpt-impressum"
tags: [n8n, automation, no-code, openai, airtable, lead-generation, google-maps]
keywords: [n8n workflow, quét lead google maps, trích xuất impressum openai, airtable lead generation, tự động hóa n8n]
---

# 🚀 Tự động quét Lead từ Google Maps và trích xuất thông tin liên hệ Impressum bằng AI

Các sếp có đang đau đầu vì việc tìm kiếm khách hàng tiềm năng (lead generation) thủ công trên Google Maps tốn quá nhiều thời gian? Việc copy-paste từng tên công ty, số điện thoại, địa chỉ website rồi mò mẫm vào trang giới thiệu (Impressum) để tìm email người ra quyết định thực sự là một cơn ác mộng lặp đi lặp lại.

Workflow n8n tuyệt vời này do tác giả **Sulieman Said** xây dựng sẽ giúp các sếp tự động hóa 100% quy trình: Quét địa điểm từ Google Maps theo thành phố, kiểm tra dữ liệu trùng lặp trên Airtable, truy cập trang Impressum của doanh nghiệp, sử dụng **OpenAI GPT** để trích xuất thông tin chi tiết (Email, Số điện thoại, Tên người ra quyết định) và lưu trữ gọn gàng vào cơ sở dữ liệu Airtable.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn quy trình Sales:** Từ việc lấy từ khóa thành phố, tìm kiếm Google Maps, cào web đến lưu trữ dữ liệu.
- **Sức mạnh AI thông minh:** Sử dụng OpenAI (`gpt-4.1-mini`) để đọc hiểu nội dung trang Impressum và bóc tách chính xác thông tin liên hệ ẩn sâu bên trong.
- **Quản lý thông minh chống trùng lặp:** Hệ thống tự động kiểm tra xem doanh nghiệp đã được quét hay chưa, đồng thời lưu trạng thái theo từng thành phố để có thể tiếp tục chạy nếu bị gián đoạn.
- **Đồng bộ hóa dữ liệu real-time:** Mọi thông tin sạch sẽ, chuẩn xác được đẩy thẳng vào bảng Airtable sẵn sàng cho các chiến dịch Outreach.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Tài khoản Airtable** với các bảng (table) chứa danh sách thành phố cần quét và bảng lưu trữ Lead.
- **Google Maps API Key** (hoặc API tương thích để tìm kiếm địa điểm qua HTTP Request).
- **OpenAI API Key** để chạy mô hình AI trích xuất thông tin (Information Extractor).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ n8n.io hoặc copy toàn bộ mã nguồn JSON, sau đó mở n8n Editor, tạo một workflow mới và Paste (Ctrl+V / Cmd+V) trực tiếp vào không gian làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần cấu hình các node quan trọng sau:

- **Node `Searchword` & `Airtable2` / `already scraped` / `Airtable1` / `Write in DB`**: Kết nối tài khoản Airtable bằng thông tin `airtableTokenApi`. Đảm bảo tên bảng (Table Name) và Base ID trùng khớp với cấu trúc quản lý danh sách Thành phố và danh sách Lead của các sếp.
- **Node `search Place` & `Place Details`**: Cung cấp thông tin xác thực (`httpQueryAuth`) chứa API Key của Google Maps (hoặc dịch vụ tìm kiếm địa điểm tương đương) để hệ thống gọi HTTP Request lấy danh sách doanh nghiệp theo thành phố.
- **Node `OpenAI Chat Model`**: Chọn kết nối `openAiApi` và cấu hình model `gpt-4.1-mini` để đảm bảo tốc độ và độ chính xác khi xử lý dữ liệu văn bản.
- **Node `Relevant Infos from Impressum`**: Kiểm tra prompt trong Information Extractor để đảm bảo AI trích xuất đúng các trường dữ liệu mong muốn (Quyết định viên, Email, Số điện thoại).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thử với một thành phố mẫu để kiểm tra dữ liệu trả về ở các node `HTML` và `Relevant Infos from Impressum`.
- Sau khi test thành công không báo lỗi, bật công tắc **Active** ở góc trên bên phải để workflow tự động hoạt động theo lịch trình hoặc khi được kích hoạt.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack:** Thêm một node Telegram hoặc Slack vào cuối chuỗi `Write in DB` để nhận thông báo ngay lập tức mỗi khi hệ thống quét xong một doanh nghiệp tiềm năng mới.
- **Mở rộng làm giàu dữ liệu (Data Enrichment):** Kết hợp thêm các bước kiểm tra tính hợp lệ của email (Email Verification) trước khi ghi vào Airtable để tối ưu tỷ lệ gửi email thành công.
- **Chạy định kỳ tự động:** Thay vì dùng `Manual Trigger` hoặc `Execute Workflow Trigger`, hãy gắn thêm một node `Schedule Trigger` để hệ thống tự động quét danh sách thành phố mới vào mỗi khung giờ cố định hàng tuần.

### 📌 Kết luận
Workflow **Google Maps to Airtable Lead Scraper** là một giải pháp cực kỳ mạnh mẽ giúp tự động hóa khâu tìm kiếm khách hàng bằng sự kết hợp hoàn hảo giữa No-code và AI. Hãy áp dụng ngay hôm nay để giải phóng đội ngũ sales khỏi những tác vụ thủ công nhàm chán!