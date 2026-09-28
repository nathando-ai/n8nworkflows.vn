---
title: "🚀 Tự động hóa tổng kết tài liệu Google Docs & PDF bằng GPT-4 và gửi đến Slack/Email"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình tổng kết nội dung tài liệu Google Docs và PDF bằng AI GPT-4, sau đó gửi kết quả đến Slack hoặc Email - hoàn toàn không cần code."
slug: "tu-dong-hoa-tong-ket-tai-lieu-google-docs-pdf-gpt4-slack-email"
tags: [n8n, automation, no-code, AI, Google Workspace]
keywords: [n8n workflow, tự động hóa, AI tổng kết, Google Docs, PDF, Slack, Email]
---

# 🚀 Tự động hóa tổng kết tài liệu Google Docs & PDF bằng GPT-4 và gửi đến Slack/Email

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải đọc và tóm tắt hàng chục tài liệu Google Docs và PDF mỗi ngày? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này chỉ trong vài bước đơn giản, giúp tiết kiệm thời gian quý giá và tập trung vào những công việc quan trọng hơn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động tổng kết tài liệu mà không cần can thiệp thủ công.
- **Chính xác cao**: Sử dụng công nghệ AI GPT-4 để đảm bảo nội dung tóm tắt chất lượng.
- **Tích hợp đa nền tảng**: Gửi kết quả đến Slack hoặc Email tùy theo nhu cầu.
- **Hoạt động liên tục**: Workflow chạy tự động 24/7, không bỏ lỡ bất kỳ tài liệu nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace (Google Drive, Google Docs)
- Tài khoản Slack (nếu muốn gửi kết quả đến Slack)
- Tài khoản Gmail (nếu muốn gửi kết quả đến Email)
- API Key từ OpenAI (để sử dụng GPT-4)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của các sếp, hãy làm theo các bước sau:

1. Truy cập vào n8n Editor của các sếp.
2. Nhấn vào nút **"Import from URL"** và dán link sau đây vào ô nhập liệu:
   ```
   https://n8n.io/workflows/8645
   ```
3. Hoặc các sếp có thể tải file JSON workflow từ [đây](https://n8n.io/workflows/8645) và import trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần chú ý cấu hình các node quan trọng sau:

- **File Created (Google Drive Trigger)**: Cấu hình để theo dõi thư mục chứa tài liệu cần tổng kết.
  - Chọn **"Google Drive OAuth2 API"** làm credentials.
  - Chọn chế độ **"every minute"** để theo dõi thay đổi liên tục.
  - Chọn thư mục cần theo dõi bằng cách nhập **ID thư mục** hoặc **URL thư mục**.

- **Check Document Type (If)**: Node này sẽ kiểm tra loại tài liệu (Google Docs hoặc PDF).
  - Điều kiện: `Mime type contains application/vnd.google-apps` để phân biệt giữa Google Docs và PDF.

- **Get a document (Google Docs)**: Node này sẽ lấy nội dung của tài liệu Google Docs.
  - Chọn **"Google Docs OAuth2 API"** làm credentials.
  - Chọn **"get"** làm operation.

- **Download PDF (Google Drive)**: Node này sẽ tải xuống file PDF từ Google Drive.
  - Chọn **"Google Drive OAuth2 API"** làm credentials.
  - Chọn **"download"** làm operation.

- **Convert to Text (Extract from File)**: Node này sẽ chuyển đổi nội dung PDF thành văn bản.
  - Chọn **"pdf"** làm operation.

- **OpenAI Chat Model**: Node này sẽ sử dụng GPT-4 để tổng kết nội dung.
  - Chọn **"OpenAI API"** làm credentials.
  - Chọn model **"gpt-4.1-mini"** (hoặc model khác phù hợp).

- **Send message to Slack Channel (Slack)**: Node này sẽ gửi kết quả tổng kết đến kênh Slack.
  - Chọn **"Slack OAuth2 API"** làm credentials.
  - Nhập thông tin kênh Slack cần gửi.

- **Email the Summary (Gmail)**: Node này sẽ gửi kết quả tổng kết đến Email.
  - Chọn **"Gmail OAuth2"** làm credentials.
  - Nhập địa chỉ Email người nhận.

#### 3. Kích hoạt ⚡️
Sau khi cấu hình xong, các sếp cần thực hiện các bước sau:

1. **Test run dữ liệu mẫu**: Chạy workflow với một tài liệu mẫu để kiểm tra kết quả.
2. **Bật Active workflow**: Sau khi đảm bảo workflow hoạt động đúng, bật chế độ **"Active"** để workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tùy chỉnh prompt**: Các sếp có thể chỉnh sửa prompt trong node **Doc Summarizer** để phù hợp với nhu cầu cụ thể của mình.
- **Lưu log**: Thêm node **Sticky Note** để lưu lại lịch sử tổng kết.
- **Thông báo định kỳ**: Sử dụng node **Schedule Trigger** để gửi báo cáo tổng kết định kỳ.
- **Kết hợp với Telegram**: Thay thế node Slack bằng node Telegram để nhận thông báo trên ứng dụng này.

### 📌 Kết luận
Workflow **"Summarize Google Docs & PDFs with GPT-4 and Send to Slack or Email"** giúp các sếp tự động hóa toàn bộ quá trình tổng kết tài liệu, tiết kiệm thời gian và nâng cao hiệu suất làm việc. Với chỉ vài bước cấu hình đơn giản, các sếp có thể triển khai workflow này ngay lập tức và tận hưởng lợi ích từ công nghệ AI. Hãy áp dụng ngay và trải nghiệm sự khác biệt!