---
title: "🚀 Tự động lấy Sub/Transcript YouTube miễn phí và lưu vào Supabase bằng n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động cào video mới từ kênh YouTube, lấy transcript qua youtube-transcript.io và lưu trữ vào cơ sở dữ liệu Supabase."
slug: "tu-dong-lay-youtube-transcript-va-luu-vao-supabase-bang-n8n"
tags: [n8n, automation, youtube, supabase, api, no-code]
keywords: [n8n workflow, youtube transcript, luu video youtube supabase, youtube-transcript.io, tu dong hoa youtube]
---

# 🚀 Tự động lấy Sub/Transcript YouTube miễn phí và lưu vào Supabase bằng n8n

Các sếp có đang tốn quá nhiều thời gian để xem, tóm tắt hoặc lấy nội dung sub từ các video YouTube yêu thích phục vụ cho việc sáng tạo nội dung, nghiên cứu thị trường hay làm AI training? Việc copy thủ công từng đoạn transcript vừa mất thời gian vừa nhàm chán.

Đừng lo! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ giúp tự động hóa toàn bộ quy trình: Quét video mới từ kênh YouTube 👉 Lọc bỏ YouTube Shorts 👉 Lấy transcript sạch qua API 👉 Lưu trữ gọn gàng vào cơ sở dữ liệu Supabase. Tất cả hoàn toàn tự động mà không cần viết một dòng code phức tạp nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Tự động hóa hoàn toàn từ khâu quét video mới đến khi lưu trữ dữ liệu.
- **Transcript sạch và chuẩn xác:** Khai thác dữ liệu văn bản từ video thông qua dịch vụ `youtube-transcript.io`.
- **Lọc thông minh:** Tự động loại bỏ các video YouTube Shorts ngắn (hoặc giữ lại tùy cấu hình của các sếp).
- **Lưu trữ khoa học:** Dữ liệu được đẩy thẳng vào Supabase (hoặc Google Sheets, Airtable tùy ý) để dễ dàng khai thác cho các ứng dụng AI, RAG hoặc làm content.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Tài khoản youtube-transcript.io:** Đăng ký tài khoản miễn phí để lấy API Key (gói miễn phí cung cấp 25 transcripts/tháng). Lấy key tại: [youtube-transcript.io](https://www.youtube-transcript.io/).
- **YouTube Channel IDs:** ID các kênh YouTube các sếp muốn theo dõi (có thể tìm nhanh qua [TunePocket Channel ID Finder](https://www.tunepocket.com/youtube-channel-id-finder)).
- **Supabase Account:** Một project Supabase đã tạo sẵn bảng (Table) để hứng dữ liệu transcript.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ nguồn gốc hoặc copy toàn bộ JSON workflow.
- Mở n8n Editor, tạo một workflow mới và chọn tùy chọn **Import from File** hoặc dán trực tiếp (Ctrl+V) vào giao diện làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 26 nodes được chia làm 3 phần chính. Các sếp cần cấu hình các điểm mấu chốt sau:

- **Node `Channels To Track` (Set):** Điền danh sách các YouTube Channel ID mà các sếp muốn hệ thống theo dõi và lấy video mới.
- **Node `Get Transcript From API` (HTTP Request):** 
  - Cấu hình credentials kiểu **Header Auth** hoặc **Query Auth**.
  - Đưa API Key nhận được từ `youtube-transcript.io` vào đây để xác thực.
- **Node `Filter Out YouTube Shorts` (If):** 
  - Theo mặc định, workflow sẽ **bỏ qua** các video YouTube Shorts. 
  - Nếu các sếp muốn lấy cả sub của Shorts, chỉ cần chọn node này và xóa điều kiện lọc thứ hai trong phần thiết lập.
- **Node `Save Data to Supabase` (Supabase):** 
  - Kết nối tài khoản Supabase của các sếp bằng **Supabase API credentials**.
  - Trỏ đúng tới bảng (Table) trong database đã chuẩn bị sẵn để lưu trữ thông tin video và nội dung transcript.

#### 3. Kích hoạt ⚡️
- Nhấn **"Execute Workflow"** thủ công tại node `When clicking ‘Execute workflow’` để test chạy thử với dữ liệu mẫu xem hệ thống có trả về kết quả mượt mà không.
- Sau khi test thành công, thay thế node Trigger thủ công bằng một **Schedule Trigger** (ví dụ: chạy 1 lần/ngày hoặc vài tiếng/lần) và bật công tắc **Active** góc trên bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Đổi nơi lưu trữ:** Nếu không dùng Supabase, các sếp có thể thay thế node `Save Data to Supabase` bằng các node lưu trữ quen thuộc khác như **Google Sheets**, **Airtable**, hoặc **n8n Data Table**.
- **Tích hợp AI tóm tắt:** Nối tiếp sau bước lấy transcript, các sếp có thể chèn thêm node **OpenAI (ChatGPT)** hoặc **Anthropic (Claude)** để tự động tóm tắt ý chính của video trước khi lưu vào database.
- **Nhận thông báo qua Telegram/Slack:** Thêm một node chat notification để bắn thông báo về máy mỗi khi có video mới được quét và trans xong.

### 📌 Kết luận
Với workflow n8n này, việc thu thập dữ liệu nội dung từ YouTube chưa bao giờ dễ dàng đến thế. Hãy áp dụng ngay để xây dựng kho tri thức riêng hoặc tối ưu hóa quy trình làm content của các sếp nhé! Chúc các sếp automation thành công!