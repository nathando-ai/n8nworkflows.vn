---
title: "🚀 Tự động hóa chuyển đổi Transcript YouTube thành nội dung chất lượng với AI và Google Sheets"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình chuyển đổi transcript YouTube thành nội dung chất lượng cao bằng công nghệ AI và Google Sheets, tiết kiệm thời gian và nâng cao hiệu suất làm việc."
slug: "tu-dong-hoa-chuyen-doi-transcript-youtube-thanh-noi-dung-chat-luong-voi-ai-va-google-sheets"
tags: [n8n, automation, no-code, content creation, multimodal AI]
keywords: [n8n workflow, tự động hóa nội dung, AI tạo nội dung, Google Sheets, YouTube transcript]
---

# 🚀 Tự động hóa chuyển đổi Transcript YouTube thành nội dung chất lượng với AI và Google Sheets

[Các sếp] có biết rằng việc chuyển đổi transcript YouTube thành nội dung chất lượng thường tốn nhiều thời gian và công sức? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này chỉ trong vài bước đơn giản, giúp tiết kiệm thời gian quý giá và nâng cao hiệu suất làm việc.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quá trình chuyển đổi transcript YouTube thành nội dung chất lượng.
- Nâng cao hiệu suất: Giảm thiểu công việc thủ công, tập trung vào những nhiệm vụ quan trọng hơn.
- Cá nhân hóa nội dung: Sử dụng công nghệ AI để tạo ra nội dung phù hợp với nhu cầu và phong cách của các sếp.
- Hoạt động liên tục: Workflow có thể chạy 24/7, đảm bảo nội dung luôn được cập nhật và sẵn sàng sử dụng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với quyền truy cập vào Google Sheets API.
- API Key từ OpenRouter để sử dụng công nghệ AI.
- Tài khoản YouTube để truy cập transcript của video.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào trang [n8n.io/workflows/9213](https://n8n.io/workflows/9213).
2. Nhấn vào nút "Download" để tải file JSON của workflow.
3. Trong n8n Editor, nhấn vào nút "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Extract YouTube Video ID (Sheets)"**: Cần cấu hình code để trích xuất ID video từ URL YouTube.
- **Node "Fetch Video Transcript Data (Sheets)"**: Cần cấu hình URL và headers để lấy transcript từ YouTube.
- **Node "Parse Transcript Text (Sheets)"**: Cần cấu hình code để phân tích và xử lý transcript.
- **Node "Save Transcript to Sheet"**: Cần cấu hình Google Sheets credentials và tên sheet để lưu transcript.
- **Node "Monitor Google Sheet for URLs"**: Cần cấu hình Google Sheets credentials và tên sheet để theo dõi URL.
- **Node "OpenRouter Chat Model"**: Cần cấu hình API Key từ OpenRouter và prompt để tạo nội dung.
- **Node "Return Transcript Response"**: Cần cấu hình để trả về kết quả cho webhook.
- **Node "Webhook Trigger (Direct Input)"**: Cần cấu hình webhook để nhận dữ liệu đầu vào.
- **Node "Save New Script to Sheet"**: Cần cấu hình Google Sheets credentials và tên sheet để lưu nội dung mới.
- **Node "OpenRouter Chat Model1"**: Cần cấu hình API Key từ OpenRouter và prompt để tạo nội dung.
- **Node "Rewrite The Transcript (webhook)"**: Cần cấu hình chain LLM để viết lại transcript.
- **Node "Rewrite The Transcript (sheets)"**: Cần cấu hình chain LLM để viết lại transcript.
- **Node "Extract YouTube Video ID (Sheets)2"**: Cần cấu hình code để trích xuất ID video từ URL YouTube.
- **Node "Fetch Video Transcript Data (Webhook)"**: Cần cấu hình URL và headers để lấy transcript từ YouTube.
- **Node "Parse Transcript Text (Webhook)"**: Cần cấu hình code để phân tích và xử lý transcript.
- **Node "Parse AI Output Into Headings(sheets)"**: Cần cấu hình code để phân tích và xử lý đầu ra từ AI.
- **Node "Parse AI Output Into Headings (webhook)"**: Cần cấu hình code để phân tích và xử lý đầu ra từ AI.
- **Node "Save New Script to Sheet(webhook)"**: Cần cấu hình Google Sheets credentials và tên sheet để lưu nội dung mới.
- **Node "Save Transcript to Sheet(webhook)"**: Cần cấu hình Google Sheets credentials và tên sheet để lưu transcript.

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình các node, nhấn vào nút "Execute Workflow" để kiểm tra workflow.
2. Kiểm tra kết quả trên Google Sheets để đảm bảo dữ liệu được lưu đúng.
3. Nếu mọi thứ hoạt động tốt, nhấn vào nút "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack hoặc Telegram để nhận thông báo khi workflow hoàn thành.
- Lưu log hoạt động của workflow để theo dõi và phân tích hiệu suất.
- Gửi báo cáo định kỳ về nội dung đã tạo để đánh giá và cải thiện chất lượng.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình chuyển đổi transcript YouTube thành nội dung chất lượng cao, tiết kiệm thời gian và nâng cao hiệu suất làm việc. Hãy áp dụng ngay để trải nghiệm sự tiện lợi và hiệu quả của công nghệ tự động hóa!