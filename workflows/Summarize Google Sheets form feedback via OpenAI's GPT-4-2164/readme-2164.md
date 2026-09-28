---
title: "🚀 Tự động hóa tổng hợp phản hồi Google Form bằng GPT-4 và gửi email báo cáo"
description: "Hướng dẫn chi tiết cách tự động hóa việc tổng hợp phản hồi Google Form bằng OpenAI GPT-4, chuyển đổi sang HTML và gửi email báo cáo một cách hoàn toàn không cần code."
slug: "tu-dong-hoa-tong-hop-phan-hoi-google-form-bang-gpt-4"
tags: [n8n, automation, no-code, google-forms, openai, gpt-4]
keywords: [n8n workflow, tự động hóa, google forms, openai, gpt-4, báo cáo tự động]
---

# 🚀 Tự động hóa tổng hợp phản hồi Google Form bằng GPT-4 và gửi email báo cáo

[Các sếp đang gặp khó khăn khi phải tổng hợp hàng trăm phản hồi từ Google Form một cách thủ công. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ việc lấy dữ liệu, tổng hợp bằng trí tuệ nhân tạo đến gửi báo cáo qua email chỉ trong vài bước đơn giản.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc tổng hợp dữ liệu thủ công.
- Nhận báo cáo tổng hợp chất lượng cao từ OpenAI GPT-4.
- Tự động hóa hoàn toàn quy trình báo cáo định kỳ.
- Giảm thiểu lỗi do nhập liệu thủ công.
- Có thể tích hợp với các hệ thống khác trong doanh nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets và Google Forms đã được thiết lập.
- Tài khoản OpenAI với API key để truy cập GPT-4.
- Tài khoản Gmail để gửi email báo cáo.
- File Google Sheets mẫu đã được chia sẻ với tài khoản Google của bạn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấp vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/2164](https://n8n.io/workflows/2164).
3. Hoặc bạn có thể tải file JSON từ link trên và import trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get Google Sheets records"**:
   - Chọn credentials là "googleSheetsOAuth2Api".
   - Nhập ID của Google Sheet của bạn (có thể lấy từ URL của Google Sheet).
   - Chọn tên của Sheet cần lấy dữ liệu (thường là "Form Responses 1" nếu sử dụng Google Forms).

2. **Node "Summarize via GPT model"**:
   - Chọn credentials là "openAiApi".
   - Đảm bảo đã chọn "chat" trong trường "resource".
   - Cập nhật prompt trong trường "prompt" để phù hợp với nhu cầu tổng hợp của bạn. Ví dụ:
     ```
     You are a helpful assistant that analyzes feedback from a Google Form. Your task is to summarize the feedback for each question in the form. The feedback is provided as JSON arrays. For each question, provide a summary of the feedback, highlighting the most common themes and any notable positive or negative feedback.
     ```

3. **Node "Send via Gmail"**:
   - Chọn credentials là "gmailOAuth2".
   - Cập nhật địa chỉ email người nhận.
   - Tùy chỉnh tiêu đề và nội dung email theo nhu cầu của bạn.

#### 3. Kích hoạt ⚡️
1. Nhấp vào nút "Test workflow" để kiểm tra dữ liệu mẫu.
2. Sau khi kiểm tra thành công, nhấp vào nút "Activate workflow" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Để xử lý các form dài hoặc có nhiều phản hồi, hãy cân nhắc chia nhỏ các câu hỏi và chạy workflow nhiều lần.
- Bạn có thể thêm node "Schedule Trigger" để tự động chạy workflow theo lịch trình định kỳ.
- Tích hợp với Slack hoặc Telegram để nhận thông báo khi workflow hoàn thành.
- Lưu trữ các báo cáo đã gửi trong Google Drive để theo dõi lịch sử.

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa hoàn toàn quy trình tổng hợp phản hồi Google Form và gửi báo cáo chỉ trong vài bước đơn giản. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả làm việc của bạn!