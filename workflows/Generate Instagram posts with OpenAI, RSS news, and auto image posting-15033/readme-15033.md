---
title: "🚀 Tự động hóa sáng tạo và đăng bài Instagram với OpenAI, RSS News và Image Generation"
description: "Hướng dẫn xây dựng hệ thống tự động lấy tin tức từ RSS, sử dụng OpenAI tạo nội dung & prompt ảnh, xử lý hình ảnh, kiểm duyệt qua Telegram và tự động đăng lên Instagram."
slug: "tu-dong-hoa-dang-bai-instagram-openai-rss-news"
tags: [n8n, automation, instagram, openai, ai-agent, content-creation]
keywords: [n8n workflow, tự động đăng Instagram, AI tạo nội dung, OpenAI chat model, RSS news automation]
---

# 🚀 Tự động hóa sáng tạo và đăng bài Instagram với OpenAI, RSS News và Image Generation

Các sếp có thấy mệt mỏi khi mỗi ngày phải lục lọi tin tức, nghĩ ý tưởng viết caption, tạo hình ảnh rồi thủ công đăng lên Instagram không? Việc này ngốn rất nhiều thời gian mà đôi khi độ tương tác lại không như ý.

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ xịn sò, tự động hóa từ A-Z quy trình: **Lấy tin tức RSS ➡️ Dùng AI tạo Caption & Prompt ➡️ Tạo ảnh tự động ➡️ Lưu trữ Cloud S3 ➡️ Gửi Telegram duyệt ➡️ Đăng lên Instagram**. Hệ thống chạy ngầm 24/7, giúp các sếp duy trì kênh social đều đặn mà không tốn chút sức lực thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần tự tay tìm kiếm tin tức hay viết bài mỗi ngày.
- **AI thông minh:** Tự động tóm tắt tin tức thành góc nhìn mới, tạo caption cuốn hút kèm hashtag chuẩn SEO.
- **Kiểm soát tuyệt đối (Human-in-the-loop):** Trước khi đăng bài, hình ảnh và caption sẽ được gửi qua Telegram để các sếp duyệt (Approve/Reject).
- **Hoạt động 24/7:** Chạy tự động theo lịch trình (Schedule Trigger) định sẵn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **OpenAI API Key** (Sử dụng cho AI Agent và GPT Model).
- **Telegram Bot Token & Chat ID** (Dùng để nhận thông báo duyệt bài).
- **Instagram Business Account** (Đã kết nối với n8n node).
- **Dịch vụ lưu trữ S3 (AWS S3, MinIO, hoặc Cloudflare R2)** để tạo public URL cho hình ảnh trước khi đẩy lên Instagram.
- **API tạo hình ảnh (HTTP NanoBanana 3.1 hoặc tương tự)** được cấu hình trong HTTP Request node.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã JSON từ [n8n Workflow #15033](https://n8n.io/workflows/15033).
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from JSON** và dán mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node quan trọng sau:
- **Schedule Trigger1:** Cài đặt lại tần suất chạy (hàng ngày, hàng tuần tùy nhu cầu).
- **CODE TEMAS & CODE RSS:** Tùy chỉnh danh sách các chủ đề (themes) và nguồn tin RSS phù hợp với lĩnh vực kinh doanh của các sếp.
- **OpenAI Chat Model & AI Agent1:** Chọn đúng credentials OpenAI và chọn model (ví dụ: `gpt-4o-mini` hoặc `gpt-4o`). Node này sẽ biến tin tức thô thành structured output gồm caption và prompt tạo ảnh.
- **HTTP NANOBANANA 3.1:** Thay thế endpoint và API key của dịch vụ tạo ảnh mà các sếp đang sử dụng.
- **Edit Image1 & Upload a file (S3):** Cấu hình credentials S3 để đẩy file ảnh đã tạo lên cloud. **Lưu ý:** Node upload phải trả về một trường dữ liệu tên là `public_image_url` vì Instagram API bắt buộc phải dùng URL công khai để nhận diện ảnh.
- **Send message and wait for response1 (Telegram):** Kết nối bot Telegram của các sếp để nhận hình ảnh kèm nút bấm duyệt/từ chối.
- **Publish1 (Instagram):** Kết nối tài khoản Instagram Business và đảm bảo truyền đúng biến `public_image_url` vào bài đăng.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm (Test run) với dữ liệu giả lập từ RSS.
- Kiểm tra tin nhắn Telegram xem bot đã gửi ảnh và caption chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh mạng xã hội:** Mở rộng workflow bằng cách thêm các node LinkedIn, Twitter (X) hoặc Facebook để đăng chéo nội dung cùng lúc.
- **Lưu trữ dữ liệu:** Thêm node Google Sheets hoặc Airtable sau bước xuất bản để lưu lại lịch sử các bài đăng, giúp dễ dàng theo dõi hiệu suất.
- **Tùy chỉnh phong cách:** Tinh chỉnh system prompt trong AI Agent để nội dung chuẩn giọng điệu (Tone of voice) của thương hiệu hơn.

### 📌 Kết luận
Workflow này là một cỗ máy tự động hoàn hảo cho những ai làm, quản lý nội dung số hoặc xây dựng thương hiệu cá nhân. Hãy triển khai ngay hôm nay để tối ưu hóa thời gian và bứt phá lượng tương tác trên Instagram nhé các sếp!