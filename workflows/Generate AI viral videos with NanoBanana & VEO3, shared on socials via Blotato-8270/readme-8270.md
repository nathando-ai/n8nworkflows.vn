---
title: "🚀 Tự động hóa tạo video AI viral với NanoBanana, VEO3 và đăng tải đa nền tảng qua Blotato"
description: "Hướng dẫn xây dựng hệ thống n8n tự động hoàn toàn: Nhận ý tưởng từ Telegram, tạo ảnh AI với NanoBanana, render video bằng VEO3 và tự động phát hành lên các mạng xã hội qua Blotato."
slug: "tu-dong-hoa-tao-video-ai-viral-nanobanana-veo3-blotato"
tags: [n8n, automation, ai-video, blotato, telegram, google-sheets]
keywords: [n8n workflow, tạo video ai, nanobanana, veo3, blotato, tự động hóa mạng xã hội, telegram bot]
keywords: [n8n workflow, tạo video ai, nanobanana, veo3, blotato, tự động hóa mạng xã hội, telegram bot]
---

# 🚀 Tự động hóa tạo video AI viral với NanoBanana, VEO3 và Blotato

Các sếp có bao giờ cảm thấy mệt mỏi khi phải tốn hàng giờ đồng hồ lên ý tưởng, thiết kế hình ảnh, render video và sau đó lại chật vật copy-paste thủ công lên từng nền tảng mạng xã hội (TikTok, YouTube, Facebook, Instagram...) chưa? Việc này không chỉ ngốn thời gian mà còn làm giảm năng suất sáng tạo nội dung.

Đừng lo, bài toán đó sẽ được giải quyết triệt để với workflow n8n cực kỳ mạnh mẽ này do chuyên gia **Dr. Firas** thiết kế. Đây là hệ thống tự động hóa **100% không cần code**, kết hợp giữa sức mạnh của các mô hình AI đỉnh cao (OpenAI GPT-4o, NanoBanana, VEO3) và công cụ phân phối nội dung đa nền tảng **Blotato**, giúp các sếp sản xuất và phát hành video viral chỉ từ một tin nhắn Telegram đơn giản!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, xử lý các tác vụ nặng như gọi API AI và render video mà không bị gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn trình (End-to-End):** Từ ý tưởng thô trên Telegram đến khi video hoàn thiện được đăng tải lên hàng loạt mạng xã hội mà không cần can thiệp thủ công.
- **Tiết kiệm 95% thời gian:** Không còn cảnh loay hoay cắt ghép video hay đăng bài từng kênh một.
- **Cá nhân hóa nội dung thông minh:** Ứng dụng AI (OpenAI GPT-4o) để viết kịch bản viral, tối ưu caption phù hợp với từng nền tảng.
- **Quản lý tập trung:** Toàn bộ dữ liệu, prompt, trạng thái xử lý được lưu trữ và cập nhật tự động trên Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU]
- **Tài khoản n8n:** Đã bật tính năng cài đặt Community Nodes.
- **Tài khoản Blotato:** Đăng ký tài khoản Blotato (gói Pro trở lên để dùng API) và lấy API Key tại `Settings > API > Generate API Key`.
- **Tài khoản OpenAI:** API Key để sử dụng các node GPT-4o và OpenAI Vision.
- **Telegram Bot:** Tạo bot qua BotFather để nhận tin nhắn đầu vào và gửi thông báo video.
- **Google Sheets & Google Drive:** 
  - Copy [Google Sheet mẫu tại đây](https://docs.google.com/spreadsheets/d/1FutmZHblwnk36fp59fnePjONzuJBdndqZOCuRoGWSmY/edit?usp=sharing).
  - Chuẩn bị một Google Drive Folder (cài đặt chế độ **Public** - ai có link đều có thể truy cập để AI và hệ thống đọc/ghi file).
- **NanoBanana & VEO3 API:** Tài khoản và thông tin xác thực để gọi API tạo ảnh/video.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cấp hoặc copy toàn bộ JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào menu 3 chấm ở góc trên bên phải -> Chọn **Import from File / Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 41 nodes được chia thành 5 bước chính (dựa trên các ghi chú trên canvas):

- **Bật Community Nodes:** Vào n8n Settings, đảm bảo đã bật "Verified Community Nodes", sau đó tìm và cài đặt node **Blotato** (`@blotato/n8n-nodes-blotato.blotato`).
- **Cấu hình Credentials:** 
  - Tạo và liên kết các tài khoản: `blotatoApi`, `openAiApi`, `telegramApi`, `googleSheetsOAuth2Api`, `googleDriveOAuth2Api`, và `httpHeaderAuth` cho NanoBanana/VEO3.
- **STEP 1 — Collect Idea & Image (`Telegram Trigger: Receive Video Idea`, `Google Sheets: Log Image & Caption`):** Kết nối Telegram Bot token của các sếp và trỏ Google Sheets node tới file Google Sheet mẫu đã chuẩn bị.
- **STEP 2 — Create Image with NanoBanana (`NanoBanana: Create Image`, `Wait for Image Edit`):** Điền endpoint API và Header xác thực của NanoBanana để hệ thống tự động tạo ảnh gốc làm nền tảng cho video.
- **STEP 3 — Generate Video Ad Script (`AI Agent: Generate Video Script`, `OpenAI Chat Model`):** Kiểm tra lại prompt và model `gpt-4.1-mini` để đảm bảo AI sinh kịch bản chuẩn xác.
- **STEP 4 — Generate Video with VEO3 (`Generate Video with VEO3`, `Wait for VEO3 Rendering`, `Download Video from VEO3`):** Cấu hình đúng API endpoint của VEO3 để render video từ ảnh và kịch bản đã tạo.
- **STEP 5 — Auto-Post to All Platforms (`Upload Video to BLOTATO`, `Youtube`, `Tiktok`, `Facebook`, `Instagram`, `Linkedin`, `Twitter (X)`, v.v.):** Kết nối credential Blotato cho tất cả các node mạng xã hội để hệ thống tự động phân phối video sau khi render xong.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một ý tưởng/hình ảnh mẫu qua Telegram Bot để test thử toàn bộ quy trình.
- Kiểm tra kết quả trên Google Sheets, Telegram và các nền tảng mạng xã hội.
- Nếu mọi thứ chạy mượt mà, gạt công tắc sang **Active** để hệ thống chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Tích hợp thêm node Slack hoặc Discord để đội ngũ nội dung nhận thông báo ngay khi video được render xong thay vì chỉ dùng Telegram.
- **Lưu trữ backup:** Thêm bước tự động lưu bản sao video vào một thư mục riêng trên Google Drive để dễ dàng tái sử dụng.
- **Báo cáo định kỳ:** Tạo thêm một nhánh chạy hàng tuần để tổng hợp số lượng video đã sản xuất và gửi báo cáo thống kê qua email hoặc Telegram.

### 📌 Kết luận
Workflow tự động hóa tạo video AI viral với NanoBanana, VEO3 và Blotato là một "vũ khí tối thượng" giúp các cá nhân và doanh nghiệp tối ưu hóa quy trình sản xuất nội dung đa nền tảng. Hãy bắt tay vào cài đặt ngay hôm nay để giải phóng sức lao động và bùng nổ tương tác trên mạng xã hội các sếp nhé!