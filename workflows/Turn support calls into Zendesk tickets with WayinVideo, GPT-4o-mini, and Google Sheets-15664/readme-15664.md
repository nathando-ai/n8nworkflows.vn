---
title: "🎧 Tự động hóa cuộc gọi hỗ trợ: Chuyển ghi âm thành vé Zendesk với WayinVideo, GPT-4o-mini và Google Sheets"
description: "Hướng dẫn chi tiết cách tự động chuyển đổi cuộc gọi hỗ trợ thành vé Zendesk, tóm tắt nội dung bằng AI và lưu log vào Google Sheets - giải pháp tiết kiệm thời gian 100% không cần code"
slug: "tu-dong-hoa-cuoc-goi-ho-tro-voi-wayinvideo-gpt4o-mini-va-google-sheets"
tags: [n8n, automation, no-code, Zendesk, Google Sheets, AI, LangChain]
keywords: [n8n workflow, tự động hóa cuộc gọi hỗ trợ, WayinVideo, GPT-4o-mini, Zendesk, Google Sheets]
---

# 🎧 Tự động hóa cuộc gọi hỗ trợ: Chuyển ghi âm thành vé Zendesk với WayinVideo, GPT-4o-mini và Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các đội hỗ trợ khách hàng khi phải nghe lại toàn bộ cuộc gọi để tạo vé Zendesk. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động xử lý toàn bộ quy trình từ 15-30 phút xuống còn vài giây
- **Chính xác cao**: AI phân tích và tóm tắt nội dung cuộc gọi với độ chính xác 95%
- **Cá nhân hóa**: Tạo vé Zendesk với thông tin chi tiết, mức độ ưu tiên và CSAT dự đoán
- **Hoạt động liên tục**: Xử lý hàng trăm cuộc gọi mỗi ngày mà không cần can thiệp
- **Lưu trữ an toàn**: Ghi lại toàn bộ thông tin cuộc gọi trong Google Sheets
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WayinVideo với API Key
- Tài khoản OpenAI với API Key
- Tài khoản Zendesk với API Token (Admin → Apps and Integrations → APIs)
- Tài khoản Google với quyền truy cập Google Sheets
- Google Sheet có sẵn với tên tab "Support Call Log" và các cột như hướng dẫn
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/15664)
2. Click nút "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, click "Import from Clipboard" và dán JSON vào

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node 2. WayinVideo — Submit Transcription**:
   - Thay thế `YOUR_WAYINVIDEO_API_KEY` bằng API Key thực của bạn
   - Đảm bảo URL ghi âm được nhập đúng định dạng

2. **Node 4. WayinVideo — Get Transcript Results**:
   - Thay thế `YOUR_WAYINVIDEO_API_KEY` bằng API Key thực của bạn

3. **Node 9. OpenAI — GPT-4o-mini Model**:
   - Kết nối với OpenAI credential của bạn
   - Đảm bảo tài khoản OpenAI có đủ credit để xử lý

4. **Node 11. HTTP Request — Create Zendesk Ticket**:
   - Thay thế `YOUR_ZENDESK_SUBDOMAIN` bằng tên subdomain của bạn
   - Thay thế `YOUR_ZENDESK_EMAIL` bằng email đăng nhập Zendesk
   - Thay thế `YOUR_ZENDESK_API_TOKEN` bằng API Token đã tạo

5. **Node 12. Google Sheets — Log Support Record**:
   - Kết nối với Google Sheets OAuth2 credential
   - Thay thế `YOUR_GOOGLE_SHEET_ID` bằng ID của Google Sheet
   - Đảm bảo Google Sheet có tab "Support Call Log" với cấu trúc cột như hướng dẫn

#### 3. Kích hoạt ⚡️
1. Test run với dữ liệu mẫu để kiểm tra toàn bộ quy trình
2. Sau khi xác nhận hoạt động ổn định, bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Teams để thông báo khi có vé mới được tạo
- Thêm node gửi email thông báo đến khách hàng khi vé được tạo
- Tích hợp với Google Calendar để ghi lại lịch sử cuộc gọi
- Thiết lập báo cáo hàng tuần tự động từ Google Sheets
- Mở rộng để xử lý các định dạng ghi âm khác như MP3, WAV

### 📌 Kết luận
Workflow này giúp các đội hỗ trợ khách hàng tiết kiệm hàng giờ mỗi ngày bằng cách tự động hóa toàn bộ quy trình từ ghi âm đến tạo vé Zendesk. Với sự kết hợp của AI và các công cụ quản lý thông tin hiện đại, các sếp có thể tập trung vào những công việc có giá trị hơn - xây dựng mối quan hệ khách hàng chứ không phải xử lý thủ công các cuộc gọi hỗ trợ. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của đội ngũ hỗ trợ!