---
title: "🤖 Tự động hóa Slack với AI Chatbot - Hướng dẫn n8n chi tiết"
description: "Hướng dẫn tạo AI Chatbot trong Slack bằng n8n. Tự động hóa tương tác với slash commands, tiết kiệm thời gian và nâng cao trải nghiệm người dùng."
slug: "tao-ai-chatbot-slack-bang-n8n"
tags: [n8n, automation, no-code, slack, ai]
keywords: [n8n workflow, tự động hóa Slack, AI chatbot, slash commands, n8n automation]
---

# 🤖 Tạo AI Chatbot trong Slack bằng n8n - Hướng dẫn chi tiết

[Các sếp đang gặp khó khăn khi phải trả lời các câu hỏi lặp lại trong Slack thủ công. Với workflow này, các sếp có thể tạo một AI Chatbot hoàn toàn tự động hóa để xử lý các slash commands, tiết kiệm thời gian và nâng cao trải nghiệm người dùng.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn các câu hỏi lặp lại trong Slack
- Tiết kiệm thời gian xử lý các yêu cầu thủ công
- Nâng cao trải nghiệm người dùng với phản hồi tức thì
- Tích hợp AI để cung cấp thông tin chính xác và hữu ích
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Slack với quyền tạo slash commands
- API Key của OpenAI để sử dụng mô hình ngôn ngữ
- Kiến thức cơ bản về n8n và cấu hình webhook
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và nhập link: https://n8n.io/workflows/2905
3. Hoặc tải file JSON về và chọn "Import from File"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node Webhook**:
   - Điểm danh: Webhook
   - Cấu hình: Giữ nguyên path và HTTP Method là POST
   - Lưu ý: Sau khi import, bạn cần copy URL của webhook này để cấu hình trong Slack slash command

2. **Node Switch**:
   - Điểm danh: Switch
   - Cấu hình: Thêm các điều kiện để xử lý các slash commands khác nhau
   - Ví dụ: `/help`, `/info`, `/support`...

3. **Node Basic LLM Chain**:
   - Điểm danh: Basic LLM Chain
   - Cấu hình: Kết nối với node OpenAI Chat Model
   - Lưu ý: Đảm bảo prompt được thiết lập rõ ràng cho từng loại câu hỏi

4. **Node OpenAI Chat Model**:
   - Điểm danh: OpenAI Chat Model
   - Cấu hình:
     - Chọn model: gpt-4o-mini (hoặc model khác phù hợp)
     - Thêm API Key của OpenAI
   - Lưu ý: Đảm bảo tài khoản OpenAI có đủ credit để sử dụng

5. **Node Send a Message**:
   - Điểm danh: Send a Message
   - Cấu hình:
     - Thêm Slack credentials
     - Thiết lập channel hoặc người nhận
   - Lưu ý: Đảm bảo bot có quyền gửi tin nhắn trong Slack

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, thực hiện test run với dữ liệu mẫu
2. Kiểm tra kết quả trong Slack để đảm bảo bot hoạt động đúng
3. Bật Active workflow để bắt đầu sử dụng

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node lưu log để theo dõi các tương tác của người dùng
- Kết hợp với Slack App để tạo các slash commands chuyên dụng
- Thiết lập báo cáo định kỳ về các tương tác của bot
- Tích hợp với các dịch vụ khác như Google Sheets để lưu trữ dữ liệu
- Sử dụng các mô hình AI khác như Claude hoặc Gemini cho đa dạng hóa phản hồi

### 📌 Kết luận
Workflow này cung cấp giải pháp hoàn chỉnh để tự động hóa tương tác trong Slack bằng AI Chatbot. Với các bước cấu hình đơn giản và hiệu quả, các sếp có thể triển khai ngay lập tức để nâng cao trải nghiệm người dùng và tiết kiệm thời gian xử lý các yêu cầu thủ công. Hãy thử ngay và thấy sự khác biệt trong cách làm việc của bạn!