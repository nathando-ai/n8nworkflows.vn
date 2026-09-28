---
title: "💸 Tự động hóa quản lý chi tiêu bằng giọng nói Siri + AI + Google Sheets"
description: "Hướng dẫn chi tiết cách tự động ghi nhận và quản lý chi tiêu qua giọng nói Siri, tích hợp AI và Google Sheets để tiết kiệm thời gian và tối ưu hóa tài chính cá nhân."
slug: "tu-dong-hoa-quan-ly-chi-tieu-bang-giong-noi-siri-ai-google-sheets"
tags: [n8n, automation, no-code, personal-productivity, ai-chatbot]
keywords: [n8n workflow, tự động hóa, quản lý chi tiêu, Siri, Google Sheets, AI]
---

# 💸 Tự động hóa quản lý chi tiêu bằng giọng nói Siri + AI + Google Sheets

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải ghi chép chi tiêu hàng ngày một cách thủ công? Với workflow này, các sếp có thể quản lý tài chính cá nhân một cách hoàn toàn tự động chỉ bằng giọng nói thông qua Siri, kết hợp với sức mạnh của trí tuệ nhân tạo và Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Ghi nhận chi tiêu chỉ bằng giọng nói Siri, không cần nhập tay.
- **Quản lý tài chính cá nhân**: Tích hợp với Google Sheets để lưu trữ và phân tích dữ liệu chi tiêu.
- **Tự động hóa thông minh**: AI phân tích yêu cầu và trả về dữ liệu cấu trúc hóa.
- **Tích hợp đa nền tảng**: Hoạt động liền mạch giữa iOS và các dịch vụ đám mây.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets API đã kích hoạt.
- Tài khoản OpenRouter API để sử dụng mô hình AI.
- Ứng dụng Shortcuts trên iOS.
- Kiến thức cơ bản về cấu hình webhook trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [n8n.io/workflows/6033](https://n8n.io/workflows/6033) để tải file JSON của workflow.
2. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON đã tải về.
3. Hoặc copy/paste nội dung JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node Webhook (Recieve)**:
   - Đảm bảo đường dẫn webhook là duy nhất và bảo mật (không nên để đường dẫn mặc định).
   - Ví dụ: `https://your-n8n-domain/webhook/siri-finance`.

2. **Node AI Agent**:
   - Cấu hình credentials cho OpenRouter API.
   - Đảm bảo sử dụng mô hình phù hợp (ví dụ: `google/gemini-2.0-flash-lite-001`).

3. **Node Google Sheets**:
   - Cấu hình credentials cho Google Sheets OAuth2.
   - Điền đúng ID của Google Sheet và tên của sheet cần ghi dữ liệu.

4. **Node Code (FormatInput và FormatOutput)**:
   - Kiểm tra và điều chỉnh mã JavaScript nếu cần thiết để xử lý dữ liệu đầu vào và đầu ra.

#### 3. Kích hoạt ⚡️
1. **Test run dữ liệu mẫu**:
   - Gửi một yêu cầu POST đến webhook với dữ liệu mẫu để kiểm tra toàn bộ chuỗi xử lý.
   - Ví dụ dữ liệu mẫu:
     ```json
     {
       "text": "Ghi nhận chi tiêu $50 cho bữa sáng"
     }
     ```

2. **Bật Active workflow**:
   - Sau khi kiểm tra và đảm bảo workflow hoạt động đúng, bật chế độ Active để workflow chạy tự động khi có yêu cầu.

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**: Thêm node để gửi thông báo chi tiêu qua Slack hoặc Telegram.
2. **Lưu log hoạt động**: Thêm node để ghi log các yêu cầu và phản hồi để theo dõi hoạt động của workflow.
3. **Gửi báo cáo định kỳ**: Tự động gửi báo cáo chi tiêu hàng tuần hoặc hàng tháng qua email.
4. **Tích hợp với các dịch vụ khác**: Kết nối với các dịch vụ tài chính khác như QuickBooks hoặc Xero để đồng bộ dữ liệu.

### 📌 Kết luận
Workflow này mang lại giải pháp toàn diện cho việc quản lý chi tiêu cá nhân thông qua giọng nói Siri, kết hợp với sức mạnh của AI và Google Sheets. Các sếp có thể tự động hóa quy trình ghi nhận và quản lý chi tiêu một cách hiệu quả, tiết kiệm thời gian và tối ưu hóa tài chính cá nhân. Hãy áp dụng ngay để trải nghiệm sự tiện lợi và hiệu quả của tự động hóa!