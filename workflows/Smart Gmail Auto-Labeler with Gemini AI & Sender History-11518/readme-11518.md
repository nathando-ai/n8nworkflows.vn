---
title: "🚀 Tự động phân loại và gắn nhãn email Gmail thông minh với AI Gemini và lịch sử người gửi"
description: "Workflow n8n tự động phân loại và gắn nhãn email Gmail bằng AI Gemini, giảm thiểu thời gian xử lý email và duy trì sạch sẽ hộp thư đến."
slug: "tu-dong-phan-loai-va-gan-nhan-email-gmail-voi-ai-gemini"
tags: [n8n, automation, no-code, gmail, ai, email-management]
keywords: [n8n workflow, tự động hóa email, quản lý email, ai phân loại email, gmail automation]
---

# 🚀 Tự động phân loại và gắn nhãn email Gmail thông minh với AI Gemini và lịch sử người gửi

[Các sếp] có bao giờ cảm thấy bị ngập lụt bởi hàng trăm email hàng ngày không? Với workflow này, các sếp có thể biến hộp thư đến của mình thành một hệ thống quản lý email không cần chạm tay - hoàn toàn tự động hóa bằng công nghệ AI Gemini của Google.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động xử lý hàng trăm email mỗi ngày mà không cần can thiệp
- **Quản lý hiệu quả**: Phân loại email chính xác dựa trên nội dung và lịch sử người gửi
- **Hộp thư sạch sẽ**: Tự động lưu trữ email sau khi xử lý, giữ hộp thư đến luôn trống
- **Tích hợp AI**: Sử dụng công nghệ Gemini của Google để phân tích và quyết định nhãn hiệu quả
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail với quyền truy cập đầy đủ
- API Key cho Google Gemini AI
- Các nhãn (labels) đã được tạo trong Gmail (Meetings, Inquiries, Notify / Verify, Expenses, Orders / Deliveries, Trash Likely)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/11518](https://n8n.io/workflows/11518)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Click "Import" để hoàn tất quá trình import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Gmail Trigger**:
   - Cấu hình credentials Gmail OAuth2
   - Đảm bảo tài khoản có quyền truy cập đầy đủ vào hộp thư

2. **Google Gemini Chat Model**:
   - Cấu hình credentials Google Palm API
   - Đảm bảo API key có quyền truy cập vào dịch vụ Gemini

3. **Check Label Existence** (Node Code):
   - Cập nhật `labelMap` với các ID nhãn thực tế của bạn
   - Thực hiện theo hướng dẫn trong phần "HOW TO GET YOUR LABEL IDs" trong ghi chú gốc

4. **Convert Label to Label ID** (Node Code):
   - Cập nhật `labelToId` mapping với các ID nhãn thực tế của bạn
   - Thực hiện theo hướng dẫn trong phần "HOW TO GET YOUR LABEL IDs" trong ghi chú gốc

5. **Get Emails By Sender Email** và **Get Emails By Label**:
   - Đảm bảo các tham số `operation` được thiết lập đúng (getAll)

#### 3. Kích hoạt ⚡️
1. Thực hiện test run với email mẫu để kiểm tra workflow hoạt động đúng
2. Sau khi kiểm tra thành công, bật chế độ Active cho workflow
3. Workflow sẽ tự động chạy mỗi phút để kiểm tra email mới

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh nhãn**: Thêm hoặc sửa đổi các nhãn trong Gmail để phù hợp với quy trình làm việc của bạn
2. **Kết hợp với Slack/Teams**: Thêm node để thông báo khi có email mới được xử lý
3. **Lưu log hoạt động**: Thêm node để ghi lại lịch sử xử lý email cho việc theo dõi và báo cáo
4. **Tự động phản hồi**: Kết hợp với node gửi email để tự động trả lời email thông thường

### 📌 Kết luận
Workflow này biến hộp thư đến của bạn thành một hệ thống quản lý email không cần chạm tay. Bằng cách kết hợp công nghệ AI Gemini với lịch sử người gửi, nó tự động phân loại và lưu trữ email một cách hiệu quả. Các sếp chỉ cần thiết lập một lần và sau đó có thể ngồi yên xem email tự động được xử lý - tiết kiệm hàng giờ mỗi ngày!