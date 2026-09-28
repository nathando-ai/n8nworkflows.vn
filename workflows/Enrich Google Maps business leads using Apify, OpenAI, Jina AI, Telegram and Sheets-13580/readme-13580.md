---
title: "🚀 Tự động quét và làm giàu thông tin Lead từ Google Maps với Apify, OpenAI & Telegram"
description: "Hướng dẫn cài đặt workflow n8n tự động tìm kiếm khách hàng tiềm năng trên Google Maps qua Telegram, cào dữ liệu bằng Apify, phân tích website bằng Jina AI và lưu trữ vào Google Sheets."
slug: "tu-dong-quet-va-lam-giau-thong-tin-lead-google-maps-n8n"
tags: [n8n, automation, lead-generation, apify, openai, google-sheets, telegram]
keywords: [n8n workflow, quét lead google maps, apify n8n, openAI trích xuất email, tự động hóa lead generation]
---

# 🚀 Tự động quét và làm giàu thông tin Lead từ Google Maps với Apify, OpenAI & Telegram

Các sếp có đang tốn hàng giờ đồng hồ mỗi ngày để tìm kiếm khách hàng tiềm năng (leads) trên Google Maps, copy thông tin thủ công vào Excel, sau đó lại phải vào từng website để mò email và tóm tắt dịch vụ của họ? Công việc lặp đi lặp lại này vừa nhàm chán, vừa tốn thời gian mà năng suất lại thấp.

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một **workflow n8n tự động hóa 100%**: Chỉ cần gửi một tin nhắn qua Telegram, hệ thống sẽ tự động quét Google Maps, loại bỏ bản ghi trùng lặp, dùng AI tóm tắt thông tin công ty, cào nội dung website để trích xuất email và lưu toàn bộ vào Google Sheets một cách mượt mà!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo sập giữa chừng khi xử lý danh sách hàng trăm leads, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Kích hoạt linh hoạt:** Chỉ cần nhắn qua Telegram theo cú pháp đơn giản là hệ thống tự chạy.
- **Dữ liệu sạch sẽ:** Tự động loại bỏ các địa điểm trùng lặp (`Deduplicate Places`) nhờ các node thông minh.
- **Làm giàu thông tin (Enrichment):** Sử dụng OpenAI để tóm tắt doanh nghiệp và trích xuất email chính xác từ website.
- **Báo cáo tức thì:** Nhận thông báo hoàn thành qua Telegram ngay khi quét xong toàn bộ danh sách.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow chạy trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Telegram Bot Token** (tạo qua BotFather).
- **Apify Account & API Key** (để chạy Google Maps Scraper Actor).
- **OpenAI API Key** (dùng cho GPT tóm tắt công ty và trích xuất email).
- **Jina AI API Key** (dùng để cào nội dung website nhanh chóng).
- **Google Sheets** (tạo sẵn file chứa bảng dữ liệu leads).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, vào n8n editor, chọn **Add workflow** -> **Import from JSON** và dán vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 15 nodes được chia thành các cụm chức năng rõ ràng. Các sếp cần cấu hình chính xác các điểm sau:

- **Receive Telegram Input & Send Done Notification:** Kết nối node với Telegram Credentials của sếp. Node kích hoạt sẽ lắng nghe tin nhắn theo cú pháp: `ngành nghề; giới hạn số lượng; link google maps`.
- **Run Maps Scraper & Fetch Dataset Items:** Kết nối Apify API credentials. Chọn Actor Google Maps Scraper phù hợp và map tham số đầu vào từ Telegram (`Parse Input Parameters`).
- **Upsert Places to Sheet & Update Email in Sheet:** Kết nối tài khoản Google Sheets OAuth2. Chọn đúng **Spreadsheet ID** và **Sheet Name** của các sếp. Node này sử dụng tính năng `appendOrUpdate` để thêm mới hoặc cập nhật dòng dữ liệu tránh bị trùng lặp.
- **Fetch Website Content:** Nhập Jina AI API Key để hệ thống crawl nội dung HTML của website doanh nghiệp.
- **Extract Website Email & Generate Company Summary:** Kết nối OpenAI API credentials, chọn model (ví dụ: `gpt-4o-mini`) để tối ưu chi phí khi xử lý văn bản và trích xuất email.
- **Wait Rate Limit:** Node này cực kỳ quan trọng để tránh bị chặn IP hoặc vượt quá giới hạn API (Rate limit) khi cào dữ liệu hàng loạt. Các sếp có thể chỉnh thời gian chờ giữa các request cho phù hợp.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (`Test workflow`) bằng cách gửi một tin nhắn mẫu qua Telegram bot của các sếp.
- Kiểm tra xem dữ liệu đã được đẩy về Google Sheets chưa.
- Sau khi mọi thứ chạy mượt mà, gạt nút **Active** để workflow hoạt động tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp CRM:** Thay vì chỉ lưu Google Sheets, các sếp có thể nối thêm node để đẩy leads thẳng vào HubSpot, Close CRM hoặc Notion.
- **Gửi Email tự động:** Sau khi có email từ website, tiếp tục dùng AI viết nội dung cold email chào hàng và tự động gửi qua Gmail hoặc Resend.
- **Log lỗi:** Thêm node xử lý lỗi (Error Trigger) để nếu một website nào đó bị chết (Error 404), workflow vẫn tiếp tục chạy mà không bị dừng đột ngột.

### 📌 Kết luận
Workflow "Enrich Google Maps business leads" là một cỗ máy tự động hóa cực kỳ mạnh mẽ giúp các sếp tối ưu hóa quy trình tìm kiếm khách hàng B2B. Hãy cài đặt ngay hôm nay để giải phóng sức lao động và tập trung vào việc chốt sales!