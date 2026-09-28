---
title: "🚀 Tự động tạo Reels thuyết âm mưu 24s từ X (Twitter) với Grok-4, Gemini và Veo 3.0 trên n8n"
description: "Khám phá workflow n8n siêu khủng giúp tự động hóa hoàn toàn quy trình sáng tạo video Reels ngắn chủ đề thuyết âm mưu từ mạng xã hội X, tích hợp AI đa phương thức."
slug: "tao-reels-thuyet-am-muu-tu-dong-n8n-grok-gemini-veo"
tags: [n8n, automation, ai-video, content-creation, google-gemini, telegram]
keywords: [n8n workflow, tạo video tự động, grok-4, google gemini, veo 3.0, telegram bot automation]
---

# 🚀 Tự động tạo Reels thuyết âm mưu 24s từ X (Twitter) với Grok-4, Gemini và Veo 3.0

Việc sản xuất nội dung video ngắn (Reels, TikTok, Shorts) theo các chủ đề hot như "thuyết âm mưu" đòi hỏi lượng thời gian khổng lồ để nghiên cứu ý tưởng, viết kịch bản, thu âm giọng đọc, tạo video AI và dựng hình. Nếu làm thủ công, các sếp có khi mất cả tiếng đồng hồ cho một video ngắn 24 giây.

Hôm nay, tui xin giới thiệu một siêu phẩm workflow n8n (tác giả *Koulikas Giannis - Coreflow Automation*) với **62 nodes** tích hợp AI đa phương thức (Multimodal AI), giúp các sếp biến các bài đăng trên X (Twitter) thành một video Reels hoàn chỉnh chỉ trong vài phút, hoàn toàn tự động 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow khủng 62 nodes này chạy mượt mà, không bị timeout giữa chừng, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Từ khâu lấy ý tưởng trên X, viết kịch bản, tạo giọng đọc Text-to-Speech, render video AI bằng Veo đến dựng phim tự động.
- **Bắt trend cực nhanh:** Khai thác nội dung viral từ mạng xã hội X để chuyển hóa thành video ngắn thu hút hàng triệu view.
- **Tiết kiệm 95% thời gian:** Không cần đụng tay vào các công cụ edit phức tạp như Premiere hay CapCut.
- **Nhận kết quả trực tiếp:** Video hoàn chỉnh được gửi thẳng về Telegram bot cá nhân để các sếp tải xuống đăng ngay.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **n8n Instance:** Đã cài đặt n8n (phiên bản cập nhật mới hỗ trợ LangChain nodes).
- **API Keys / Credentials:**
  - **Google Gemini & DeepSeek API Key:** Dành cho các node AI (`Google Gemini Chat Model`, `DeepSeek Chat Model1`, `Story writer`).
  - **Grok API Key (X/Twitter AI):** Để phân tích và xử lý nội dung từ Grok-4.
  - **Text-to-Speech (TTS) & Video Generation API:** Các node HTTP Request kết nối dịch vụ tạo giọng đọc và video Veo 3.0.
  - **Google Cloud Storage (GCS):** Tài khoản lưu trữ cloud để chứa các file audio và video tạm thời (`Upload to Cloud Storage 1`, `Video Hook Upload`...).
  - **Creatomate API:** Dùng để dựng và render video tự động ở bước cuối (`Merge - Creatomate`).
  - **Telegram Bot Token:** Để gửi video hoàn thiện về chat Telegram của các sếp (`Send a video`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow này.
- Vào giao diện n8n Editor, chọn **Add workflow** -> **Import from JSON** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Vì đây là một workflow phức tạp với 62 nodes, các sếp cần chú ý cấu hình kỹ các nhóm sau:
- **Nhóm AI & LLM (`Story writer`, `Generate Hook Prompt`, v.v.):** Kết nối đúng Credentials của Gemini và DeepSeek. Đảm bảo các model được chọn tương thích (ví dụ: `Google Gemini Chat Model`, `DeepSeek Chat Model1`).
- **Nhóm X / Grok API (`Grok 4`, `Grok Prompt`):** Điền chính xác Endpoint và Token xác thực cho API của Grok-4.
- **Nhóm Lưu trữ (`Upload to Cloud Storage Hook`, `Video Segment 1 Upload`...):** Cấu hình Google Cloud Storage Bucket credentials để workflow có quyền đẩy file audio và video lên mây.
- **Nhóm Dựng video (`Creatomate HTTP Body`, `Merge - Creatomate`):** Cấu hình template ID và API key của Creatomate để hệ thống ghép nối các segment video và audio lại với nhau chuẩn xác 24 giây.
- **Node cuối cùng (`Send a video`):** Điền `Chat ID` Telegram của các sếp để nhận thành phẩm nóng hổi.

#### 3. Kích hoạt ⚡️
- Bấm nút **Manual Trigger** để test chạy thử (Test Run) với một dữ liệu mẫu.
- Theo dõi log chạy qua các node `Wait`, `Rendering....`, `done?` để đảm bảo không bị lỗi kết nối API.
- Khi mọi thứ mượt mà, bật công tắc **Active** góc trên bên phải để workflow sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng nguồn dữ liệu:** Thay vì dùng `Manual Trigger`, các sếp có thể đổi thành node kích hoạt theo lịch (Cron/Schedule Trigger) mỗi ngày quét 3 bài top trending trên X để làm video tự động.
- **Đa kênh phân phối:** Mở rộng workflow bằng cách gắn thêm node đăng video tự động lên TikTok, YouTube Shorts và Facebook Reels ngay sau node Telegram.
- **Lưu log quản lý:** Thêm node Google Sheets để lưu lại tiêu đề kịch bản, link video GCS nhằm dễ dàng tra cứu lịch sử nội dung đã sản xuất.

### 📌 Kết luận
Workflow tạo Reels thuyết âm mưu tự động này là một "vũ khí tối tân" giúp các nhà sáng tạo nội dung tối ưu hóa hiệu suất sản xuất video ngắn bằng AI. Hãy thiết lập ngay hôm nay để bứt phá lượng tương tác trên các nền tảng mạng xã hội!