---
title: "🚀 Tự động đăng bài đa nền tảng từ Google Sheets kèm hình ảnh AI với n8n"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động hóa đăng bài viết lên 5 mạng xã hội X, Threads, LinkedIn, Facebook và Instagram kèm hình ảnh do AI tạo ra từ Google Sheets."
slug: "tu-dong-dang-bai-da-nen-tang-google-sheets-ai-images-n8n"
tags: [n8n, automation, social-media, openai, google-sheets]
keywords: [n8n workflow, tự động hóa mạng xã hội, cross-post google sheets, ai image generation n8n, auto post facebook linkedin instagram x threads]
---

# 🚀 Tự động đăng bài đa nền tảng từ Google Sheets kèm hình ảnh AI với n8n

Các sếp có bao giờ cảm thấy mệt mỏi khi phải copy một nội dung bài viết, chỉnh sửa kích thước ảnh, rồi lần lượt đăng thủ công lên từng mạng xã hội như Facebook, LinkedIn, Instagram, X (Twitter) và Threads chưa? Việc này vừa tốn hàng giờ đồng hồ, vừa dễ bỏ sót lịch trình.

Giải pháp cho các sếp đây: Workflow n8n siêu việt này sẽ giúp tự động hóa 100% quy trình. Chỉ cần viết nội dung vào **Google Sheets**, hệ thống sẽ tự động phân tích, tạo hình ảnh minh họa bằng AI, lưu trữ, và đăng tải lên **5 nền tảng mạng xã hội cùng lúc** mà không cần tốn một phút làm thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Viết nội dung một lần duy nhất, phát hành tự động trên 5 nền tảng (X, Threads, LinkedIn, Facebook, Instagram).
- **Hình ảnh AI cá nhân hóa:** Tự động tạo hình ảnh độc quyền phù hợp với nội dung bài viết thông qua OpenAI và OpenRouter.
- **Không bao giờ trùng lặp:** Hệ thống tự động quét và cập nhật trạng thái bài viết trên Google Sheets (Ready To Post ➔ Posted / Errored).
- **Hoạt động 24/7:** Chạy hoàn toàn tự động theo lịch trình định sẵn nhờ Schedule Trigger.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản/Hạ tầng **n8n** (Cloud hoặc Self-hosted).
- **Google Sheets:** Chứa file quản lý nội dung bài đăng.
- **OpenAI API & OpenRouter API:** Dùng cho AI Agent tạo prompt hình ảnh và OpenAI Image (`gpt-image-1`) tạo đồ họa.
- **ImgBB Account:** Để upload và lấy link công khai cho hình ảnh AI tạo ra.
- **Tài khoản và API/OAuth2** của các mạng xã hội:
  - X (Twitter)
  - Threads (qua API/HTTP Request)
  - LinkedIn
  - Facebook Page & Instagram Business (qua Facebook Graph API)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow (hoặc tải file từ nguồn gốc) và dán trực tiếp vào n8n Editor của mình thông qua tính năng Import từ clipboard.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:
- **Get Content & Done / Error (Google Sheets):** Kết nối tài khoản Google Sheets OAuth2. Trỏ đến file Google Sheet quản lý nội dung của sếp, cấu hình để tìm các dòng có `Status = Ready To Post`. Node **Done** và **Error** sẽ cập nhật trạng thái thành `Posted` hoặc `Errored` sau khi chạy xong.
- **OpenRouter Gemini 2.5 Flash & Image Prompt Agent:** Cấu hình OpenRouter API key để AI phân tích nội dung bài viết và viết một prompt tối ưu cho việc tạo ảnh.
- **Generate an image (OpenAI):** Kết nối OpenAI credentials, sử dụng mô hình `gpt-image-1` với prompt đầu ra từ AI Agent để sinh ảnh.
- **ImgBB (HTTP Request):** Cấu hình API key của ImgBB để tự động upload bức ảnh vừa tạo và trả về URL chia sẻ công khai.
- **Các node mạng xã hội (X, Threads, LinkedIn, Facebook, Instagram, Instagram Image):** Kết nối đầy đủ thông tin xác thực OAuth2 hoặc API tương ứng cho từng nền tảng. Lưu ý phân tách rõ:
  - *X & Threads:* Đăng nội dung thuần văn bản (Text-only).
  - *LinkedIn, Facebook & Instagram:* Đăng kèm hình ảnh đã được lưu trữ URL từ ImgBB.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một dòng dữ liệu mẫu trong Google Sheets để kiểm tra toàn bộ luồng từ tạo ảnh đến đăng bài.
- Sau khi test thành công, bật công tắc **Active** để workflow tự động chạy theo lịch trình của `Schedule Trigger`.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Thông báo:** Thêm node Telegram hoặc Slack ở cuối luồng để gửi tin nhắn báo cáo mỗi khi bài viết được đăng thành công hoặc gặp lỗi (`Errored`).
- **Phê duyệt thủ công (Human-in-the-loop):** Thay vì dùng `Schedule Trigger`, các sếp có thể đổi thành Webhook kết hợp với nút bấm trong giao diện chat hoặc Airtable để duyệt bài trước khi hệ thống tự động chạy.
- **Đa dạng hóa phong cách ảnh:** Tinh chỉnh prompt trong AI Agent để thay đổi phong cách nghệ thuật (3D, Cinematic, Minimalist, v.v.) phù hợp với thương hiệu cá nhân hoặc doanh nghiệp.

### 📌 Kết luận
Tự động hóa marketing chưa bao giờ dễ dàng đến thế! Với workflow n8n này, các sếp có thể quản lý cả một hệ sinh thái mạng xã hội chỉ từ một bảng Google Sheets duy nhất. Lên đồ ngay và tối ưu hóa hiệu suất làm việc của mình thôi các sếp! 🚀