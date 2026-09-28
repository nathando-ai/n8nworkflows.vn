---
title: "🎤 Tự động hóa chuyển đổi âm thanh thành văn bản và tóm tắt với Whisper & GPT từ Google Drive sang Notion"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình chuyển đổi âm thanh thành văn bản và tóm tắt nội dung bằng công nghệ AI Whisper và GPT, từ Google Drive sang Notion"
slug: "tu-dong-hoa-chuyen-doi-am-thanh-thanh-van-ban-voi-whisper-gpt"
tags: [n8n, automation, no-code, google-drive, notion, ai, whisper, gpt]
keywords: [n8n workflow, tự động hóa, chuyển đổi âm thanh, tóm tắt nội dung, google drive, notion, ai, whisper, gpt]
---

# 🎤 Tự động hóa chuyển đổi âm thanh thành văn bản và tóm tắt với Whisper & GPT từ Google Drive sang Notion

[Các sếp] có bao giờ phải ngồi hàng giờ để nghe lại các cuộc họp, podcast hay ghi âm để chuyển đổi thành văn bản? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài phút, giúp tiết kiệm thời gian quý giá và tập trung vào những việc quan trọng hơn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa quy trình chuyển đổi âm thanh thành văn bản và tóm tắt nội dung.
- **Chính xác cao**: Sử dụng công nghệ AI Whisper và GPT để đảm bảo độ chính xác cao.
- **Tích hợp liền mạch**: Kết nối trực tiếp với Google Drive và Notion để quản lý nội dung một cách hiệu quả.
- **Hoạt động liên tục**: Workflow chạy tự động 24/7, không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive với quyền truy cập vào thư mục chứa file âm thanh.
- Tài khoản Notion với quyền tạo trang mới.
- API Key từ OpenAI để sử dụng dịch vụ Whisper và GPT.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n, các sếp có thể thực hiện theo các bước sau:

1. Truy cập vào n8n Editor của các sếp.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/6139](https://n8n.io/workflows/6139).
3. Hoặc, các sếp có thể tải file JSON từ link trên và import trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Google Drive Trigger**:
  - Kết nối tài khoản Google Drive của các sếp.
  - Chỉ định thư mục trong Google Drive mà các sếp muốn theo dõi.
  - Cấu hình để tải xuống file âm thanh khi phát hiện file mới.

- **Download file**:
  - Đảm bảo node này được kết nối với Google Drive Trigger để tải xuống file âm thanh.

- **Transcribe a recording**:
  - Cung cấp API Key từ OpenAI để sử dụng dịch vụ Whisper.
  - Đảm bảo node này nhận được file âm thanh từ node Download file.

- **AI Agent**:
  - Node này sẽ xử lý và chuyển đổi văn bản từ node Transcribe a recording.

- **OpenAI Chat Model**:
  - Cung cấp API Key từ OpenAI để sử dụng dịch vụ GPT.
  - Cấu hình node này để nhận văn bản từ node AI Agent.
  - Tạo prompt rõ ràng để GPT tạo ra tóm tắt mong muốn (ví dụ: "Tóm tắt nội dung sau: [văn bản]").

- **Create a page**:
  - Kết nối tài khoản Notion của các sếp.
  - Chỉ định cơ sở dữ liệu hoặc trang trong Notion nơi các sếp muốn tạo trang mới.
  - Ánh xạ kết quả tóm tắt từ node OpenAI Chat Model vào thuộc tính văn bản trong Notion.
  - Tùy chọn: Ánh xạ các thông tin khác như tên file, ngày tải lên vào các thuộc tính khác trong Notion.

#### 3. Kích hoạt ⚡️
- **Test run dữ liệu mẫu**: Các sếp nên thử chạy workflow với một file âm thanh mẫu để đảm bảo mọi thứ hoạt động đúng.
- **Bật Active workflow**: Sau khi kiểm tra và đảm bảo workflow hoạt động đúng, các sếp có thể bật chế độ Active để workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Các sếp có thể thêm node gửi thông báo qua Slack hoặc Telegram khi workflow hoàn thành.
- **Lưu log**: Thêm node lưu log để theo dõi quá trình xử lý và phát hiện lỗi.
- **Gửi báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo tổng hợp hàng tuần hoặc hàng tháng về các file âm thanh đã xử lý.
- **Tích hợp với các công cụ khác**: Kết nối với các công cụ khác như Airtable, Google Sheets để lưu trữ và quản lý dữ liệu một cách hiệu quả.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình chuyển đổi âm thanh thành văn bản và tóm tắt nội dung một cách hiệu quả. Với sự tích hợp liền mạch với Google Drive và Notion, các sếp có thể quản lý nội dung một cách dễ dàng và tiết kiệm thời gian quý giá. Hãy áp dụng ngay workflow này để nâng cao hiệu suất làm việc của các sếp!