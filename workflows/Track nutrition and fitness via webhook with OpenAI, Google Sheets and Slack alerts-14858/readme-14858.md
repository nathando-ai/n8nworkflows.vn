---
title: "🚀 Theo dõi dinh dưỡng và thể dục với AI, Google Sheets và cảnh báo Slack"
description: "Tự động hóa theo dõi dinh dưỡng và thể dục thông qua webhook với OpenAI, Google Sheets và cảnh báo Slack. Tiết kiệm thời gian và nhận cảnh báo ngay khi vượt ngưỡng dinh dưỡng."
slug: "theo-doi-dinh-duong-the-duc-voi-ai-google-sheets-slack"
tags: [n8n, automation, no-code, AI, health-tracking]
keywords: [n8n workflow, tự động hóa, theo dõi sức khỏe, OpenAI, Google Sheets, Slack]
---

# 🚀 Theo dõi dinh dưỡng và thể dục với AI, Google Sheets và cảnh báo Slack

[Các sếp] có biết không? Theo dõi dinh dưỡng và thể dục hàng ngày là một công việc cực kỳ tốn thời gian và dễ gây lỗi. Mỗi ngày, các sếp phải ghi chép, tính toán và phân tích hàng tá thông tin về thực phẩm, hoạt động thể chất và chỉ số sức khỏe. Và khi số lượng người dùng tăng lên, công việc này trở nên cực kỳ phức tạp.

Với workflow này, các sếp có thể tự động hóa hoàn toàn quá trình theo dõi sức khỏe của mình. Workflow này sẽ nhận dữ liệu từ người dùng thông qua webhook, phân tích thông tin bằng trí tuệ nhân tạo (AI) của OpenAI, lưu trữ dữ liệu trong Google Sheets và gửi cảnh báo qua Slack khi phát hiện các vấn đề sức khỏe.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa quá trình theo dõi sức khỏe, giảm thiểu công việc thủ công.
- **Nhận cảnh báo ngay lập tức**: Nhận thông báo qua Slack khi vượt ngưỡng dinh dưỡng hoặc phát hiện rủi ro sức khỏe.
- **Dữ liệu chính xác**: Lưu trữ và cập nhật dữ liệu sức khỏe trong Google Sheets, đảm bảo tính chính xác và dễ dàng truy cập.
- **Theo dõi liên tục**: Hệ thống hoạt động liên tục 24/7, không bị gián đoạn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets đã được cấu hình với các cột: Phone, Calories, Protein, Risk Count, Daily Calorie Limit.
- API Key của OpenAI để sử dụng mô hình AI.
- Tài khoản Slack để nhận cảnh báo.
- Webhook để nhận dữ liệu từ người dùng (có thể từ ứng dụng hoặc chatbot).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và nhập URL: `https://n8n.io/workflows/14858`.
3. Hoặc, tải file JSON từ [đây](https://n8n.io/workflows/14858) và import vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Receive User Input"**:
   - Cấu hình webhook với đường dẫn `diet-input`.
   - Ví dụ: `http://your-n8n-instance.com/webhook/diet-input`.

2. **Node "Fetch User Data" và "Update User Data"**:
   - Chọn credentials `googleSheetsOAuth2Api`.
   - Điền ID của Google Sheet và tên của Sheet.

3. **Node "AI Model (GPT)"**:
   - Chọn credentials `openAiApi`.
   - Chọn mô hình `gpt-4.1-mini`.

4. **Node "Alert: Calorie Limit Exceeded", "Alert: Health Risk" và "Alert: Critical Health Issue"**:
   - Chọn credentials `slackApi`.
   - Cấu hình kênh Slack để nhận cảnh báo.

5. **Node "Daily Reset Trigger"**:
   - Cấu hình lịch trình hàng ngày để reset dữ liệu hàng ngày.

#### 3. Kích hoạt ⚡️
1. Kiểm tra workflow bằng cách gửi dữ liệu mẫu thông qua webhook.
2. Bật workflow để hoạt động liên tục.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm các node để gửi cảnh báo qua Telegram hoặc các kênh khác.
- **Lưu log**: Thêm node để lưu log các hoạt động quan trọng.
- **Gửi báo cáo định kỳ**: Cấu hình gửi báo cáo sức khỏe hàng tuần hoặc hàng tháng qua email.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình theo dõi sức khỏe, tiết kiệm thời gian và nhận cảnh báo ngay khi phát hiện các vấn đề sức khỏe. Hãy áp dụng ngay để nâng cao hiệu quả theo dõi sức khỏe của mình!