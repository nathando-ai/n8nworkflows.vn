---
title: "🚀 Tự động hóa tạo Video Avatar AI từ URL bằng HeyGen, Gemini và đăng lên Mạng xã hội"
description: "Biến mọi URL bài viết, tin tức hoặc trang web thành video avatar AI ngắn gọn, chuyên nghiệp và tự động đăng tải lên các nền tảng mạng xã hội với n8n."
slug: "tu-dong-hoa-tao-video-avatar-ai-tu-url-heygen-gemini"
tags: [n8n, automation, heygen, gemini, ai-avatar, social-media, content-creation]
keywords: [n8n workflow, tạo video AI, HeyGen automation, Google Gemini, Upload Post, tự động hóa mạng xã hội]
---

# 🚀 Biến mọi URL thành Video Avatar AI và Đăng tải tự động lên Mạng xã hội

Các sếp có đang mệt mỏi vì phải tốn hàng giờ viết kịch bản, quay dựng video ngắn (TikTok, Reels, Shorts) từ các bài báo, blog hay tài liệu mỗi ngày? Việc sản xuất nội dung thủ công vừa tốn kém thời gian lại khó duy trì tần suất đều đặn.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code (No-code): Tự động lấy nội dung từ bất kỳ URL nào, sử dụng **Google Gemini** để tóm tắt và viết kịch bản cuốn hút, kết hợp **HeyGen** để tạo video avatar AI đọc nội dung, và cuối cùng tự động đẩy video lên các nền tảng mạng xã hội thông qua **Upload-Post**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần quay phim, dựng hình hay thu âm thủ công; chỉ cần thả URL và nhận video hoàn chỉnh.
- **AI thông minh:** Google Gemini tự động phân tích bài viết thành kịch bản 30-45 giây ngắn gọn, kèm mô tả tối ưu hóa cho từng nền tảng.
- **Đa dạng chế độ hiển thị:** Hỗ trợ cả tài khoản HeyGen miễn phí (dạng chia đôi màn hình - split-screen) lẫn tài khoản trả phí (xóa phông nền chuyên nghiệp).
- **Kiểm duyệt linh hoạt:** Có bước `Wait to approve by user` cho phép các sếp xem trước, duyệt hoặc chỉnh sửa video trước khi bấm nút xuất bản.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để chạy được workflow này, các sếp cần chuẩn bị các tài khoản và API keys sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Google Gemini API Key** (cho node `Google Gemini Chat Model`).
- **HeyGen API Key** (Hỗ trợ bản Free/Trial hoặc Paid Plan nếu muốn xóa phông nền).
- **ScreenshotOne API** (https://dash.screenshotone.com/ - Dùng để chụp ảnh/quay màn hình URL làm background video).
- **Upload-Post API** (https://app.upload-post.com - Nền tảng kết nối và đăng video lên các mạng xã hội như TikTok, YouTube, Instagram, Facebook...).
- *(Tùy chọn)* **ElevenLabs** (Nếu muốn dùng giọng đọc cá nhân hóa liên kết trong HeyGen).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã JSON từ nguồn gốc.
- Mở n8n Editor, chọn **Add workflow** -> **Import from File / Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `Google Gemini Chat Model` & `Google Gemini Chat Model1`**: Kết nối credentials `googlePalmApi` của các sếp để AI có thể đọc web và viết kịch bản.
- **Node `Set Input Vars`**: Khai báo các thông số quan trọng:
  - `avatar_id` và `voice_id` lấy từ tài khoản HeyGen của các sếp.
  - `background_video_url` hoặc `background_image_url` (đường dẫn video/hình nền nền tảng).
  - Cấu hình `background_removal: true` (nếu dùng tài khoản HeyGen trả phí để xóa phông) hoặc `false` (nếu dùng bản Free/Trial với dạng chia đôi màn hình).
- **Node `Upload video to all social networks`**: Kết nối API key từ [Upload-Post](https://app.upload-post.com) để chọn các kênh mạng xã hội muốn đăng (TikTok, Reels, X, v.v.).

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** (hoặc dùng `When clicking ‘Execute workflow’`) để test thử với một URL mẫu.
- Sau khi kiểm tra qua bước `Wait to approve by user`, nếu mọi thứ hoàn hảo, các sếp chỉ cần gạt công tắc sang **Active** để hệ thống tự động hóa hoàn toàn.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bước thông báo Telegram/Slack:** Gắn thêm node Telegram ngay sau bước tạo video xong để hệ thống gửi thông báo kèm link preview trực tiếp về điện thoại cho các sếp duyệt thay vì phải mở n8n.
- **Lưu trữ Google Sheets:** Thêm node Google Sheets để lưu lại danh sách các URL đã xử lý, tiêu đề video và trạng thái đăng bài nhằm dễ dàng quản lý kho nội dung.
- **Lên lịch định kỳ:** Thay thế nút `Manual Trigger` bằng `Schedule Trigger` để tự động quét tin tức mới từ các trang báo công nghệ/marketing mỗi sáng và biến chúng thành video tự động.

### 📌 Kết luận
Workflow này là một "vũ khí" cực mạnh cho các nhà sáng tạo nội dung, Marketer và doanh nghiệp muốn phủ sóng thương hiệu đa nền tảng bằng video AI. Hãy thiết lập ngay hôm nay để tối ưu hóa hiệu suất làm việc của các sếp!