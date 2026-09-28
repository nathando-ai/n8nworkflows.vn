---
title: "🚀 Tự động tạo video hài ngắn triệu view từ Google Sheets bằng Google Gemini và Wavespeed AI"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa toàn bộ quy trình sản xuất video hài ngắn từ Google Sheets, sử dụng Gemini AI sáng tạo nội dung và Wavespeed AI/Blotato để render, đăng tải lên TikTok, YouTube, Instagram."
slug: "tu-dong-tao-video-hai-ngan-tu-google-sheets-gemini-wavespeed-ai"
tags: [n8n, automation, no-code, ai-video, google-gemini, content-creation]
keywords: [n8n workflow, tạo video tự động, google sheets gemini, wavespeed ai, blotato, auto tiktok youtube]
---

# 🚀 Tự động tạo video hài ngắn triệu view từ Google Sheets bằng Google Gemini và Wavespeed AI

Các sếp có đang chật vật tốn hàng giờ mỗi ngày để nghĩ ý tưởng kịch bản, viết prompt, tạo hình ảnh/video, dựng clip và thủ công đăng lên các nền tảng Reels, TikTok, YouTube Shorts không? Việc sản xuất nội dung video ngắn (Short-form Video) đòi hỏi sự kiên trì và khối lượng công việc khổng lồ, rất dễ khiến team sáng tạo rơi vào trạng thái kiệt sức (burnout).

Giải pháp cho các sếp đây! Workflow n8n siêu cấp này sẽ tự động hóa **100% quy trình sản xuất nội dung đa phương tiện**: Lấy ý tưởng truyện cười/chủ đề từ Google Sheets, sử dụng sức mạnh của **Google Gemini** để sáng tạo kịch bản & prompt chi tiết, gọi API tạo video thông qua **Wavespeed AI**, sau đó tự động xuất bản lên các mạng xã hội (YouTube, TikTok, Instagram, Twitter) thông qua **Blotato** mà không cần động tay chân.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 (đặc biệt khi xử lý các tác vụ render video nặng và có bước `Wait`), các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần tự tay viết kịch bản hay dựng hình ảnh, AI lo từ A-Z.
- **Sản xuất nội dung vô tận:** Tự động lấy nguồn từ Google Sheets hoặc chạy định kỳ theo lịch (Schedule Trigger).
- **Đa nền tảng mượt mà:** Tự động đăng tải (cross-platform) lên YouTube, TikTok, Instagram Reels, và Twitter (X) cùng lúc.
- **Vận hành tự động hoàn toàn:** Tích hợp các node `Wait`, `Get Video Result` để xử lý quá trình render video nặng ngầm mà không làm nghẽn hệ thống.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Khuyên dùng bản self-hosted để không bị giới hạn thời gian chạy timeout).
- **Google Sheets:** File Google Sheets chứa danh sách ý tưởng hoặc truyện cười.
- **Google Gemini API Credentials:** Để cấp quyền cho các node `Gemini Model (Creative)`, `Gemini Model (Scripting)`.
- **Wavespeed AI API / Image-to-Video API:** Tài khoản và API key cho các node HTTP Request tạo video (`Generate Video (Img2Vid)`, `Generate Background Edit`).
- **Blotato Account:** Tài khoản kết nối với node `@blotato/n8n-nodes-blotato.blotato` để tự động đăng bài lên các mạng xã hội.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ n8n.io (Link gốc: [Workflow 13040](https://n8n.io/workflows/13040)).
- Tại giao diện n8n Editor, bấm vào menu **Add workflow** -> **Import from File** (hoặc Copy toàn bộ JSON và Paste trực tiếp vào màn hình workflow).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần chú ý cấu hình các node cốt lõi sau:
- **Schedule Trigger / When clicking ‘Execute workflow’:** Chọn cách kích hoạt workflow (chạy tự động theo lịch hoặc bấm thủ công).
- **Google Sheet Jokes & Google Sheet Past Jokes (googleSheetsTool):** Kết nối tài khoản Google Drive/Sheets của các sếp, trỏ tới đúng file Google Sheet chứa dữ liệu đầu vào.
- **Gemini Model (Creative) & Gemini Model (Scripting) (lmChatGoogleGemini):** Điền API Key của Google Gemini để các Agent (`Creative Video Idea`, `Detailed Video Prompts`) có đủ "trí tuệ" viết kịch bản.
- **Generate Video (Img2Vid) & Get Video Result (httpRequest):** Cấu hình Endpoint API và Header xác thực của nhà cung cấp dịch vụ AI Video (Wavespeed AI). Chú ý các node `Wait` (`Wait for Video Gen`, `Wait for Edit`) để đảm bảo hệ thống chờ video render xong mới lấy kết quả.
- **Youtube, Tiktok, Instagram, Twitter (X) (@blotato/n8n-nodes-blotato.blotato):** Kết nối tài khoản Blotato tương ứng để cấu hình kênh xuất bản video cuối cùng.
- **Save Final URL & Update Status to "DONE" (googleSheets):** Cấu hình ghi lại đường dẫn video hoàn thành và cập nhật trạng thái dòng dữ liệu trên Google Sheets.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** với một vài dòng dữ liệu mẫu trong Google Sheets để test toàn bộ luồng từ tạo kịch bản -> render video -> đăng mạng xã hội.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bước kiểm duyệt (Human-in-the-loop):** Thay vì đăng thẳng lên mạng xã hội, các sếp có thể chèn thêm node gửi thông báo qua Telegram/Slack kèm nút bấm "Phê duyệt" hoặc "Từ chối" trước khi gọi node Blotato đăng bài.
- **Quản lý lịch đăng bài:** Kết hợp thêm node Google Calendar hoặc Database (Airtable/Supabase) để theo dõi lịch trình video đã xuất bản.
- **Tùy biến giọng đọc (Voiceover):** Tích hợp thêm các node gọi API Text-to-Speech (như ElevenLabs) trước bước render video để chèn lồng tiếng tự động vào kịch bản hài.

### 📌 Kết luận
Workflow tạo video ngắn tự động bằng Google Gemini và Wavespeed AI chính là "vũ khí tối thượng" giúp các content creator nhân bản kênh, tiết kiệm hàng chục triệu đồng chi phí nhân sự dựng video thủ công. Hãy import ngay workflow này và tối ưu hóa kênh social của các sếp ngay hôm nay!