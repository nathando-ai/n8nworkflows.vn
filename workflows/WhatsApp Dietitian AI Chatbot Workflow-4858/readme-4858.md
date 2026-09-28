---
title: "🍽️ Tự động hóa Chatbot Chuyên Gia Dinh Dưỡng trên WhatsApp với AI"
description: "Hướng dẫn tự động hóa hoàn toàn quá trình tư vấn dinh dưỡng qua WhatsApp bằng công nghệ AI Gemini của Google, giúp tiết kiệm thời gian và cá nhân hóa trải nghiệm cho người dùng."
slug: "tu-dong-hoa-chatbot-dinh-duong-whatsapp-ai"
tags: [n8n, automation, no-code, whatsapp, ai]
keywords: [n8n workflow, tự động hóa, chatbot dinh dưỡng, whatsapp ai, google gemini]
---

# 🍽️ Tự động hóa Chatbot Chuyên Gia Dinh Dưỡng trên WhatsApp với AI

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quá trình tư vấn dinh dưỡng qua WhatsApp
- Cá nhân hóa trải nghiệm người dùng với các câu trả lời chính xác và chi tiết
- Tiết kiệm thời gian cho chuyên gia dinh dưỡng
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
- Tích hợp công nghệ AI tiên tiến của Google Gemini
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WhatsApp Business API
- API Key của Google Gemini
- Môi trường n8n đã được cài đặt và cấu hình
- Kiến thức cơ bản về sử dụng n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào menu "Workflows" ở góc trái
3. Chọn "Import from URL" và nhập link: [https://n8n.io/workflows/4858](https://n8n.io/workflows/4858)
4. Hoặc bạn có thể tải file JSON về và chọn "Import from File"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Google Gemini Chat Model"**:
   - Cấu hình credentials cho Google Gemini
   - Điền API Key của bạn vào trường tương ứng

2. **Node "WhatsApp Message Received"**:
   - Cấu hình credentials cho WhatsApp Business API
   - Đảm bảo đã kích hoạt webhook và cung cấp URL callback chính xác

3. **Node "Structured Output Parser"**:
   - Cấu hình schema đầu ra mong muốn cho các câu trả lời của chatbot
   - Điều chỉnh các trường dữ liệu theo nhu cầu cụ thể của bạn

4. **Node "Check if message contains image"**:
   - Cấu hình điều kiện để phân biệt giữa tin nhắn văn bản và hình ảnh
   - Điều chỉnh logic nếu cần xử lý các loại tin nhắn khác

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, hãy test workflow với một số tin nhắn mẫu
2. Kiểm tra xem các node xử lý tin nhắn văn bản và hình ảnh có hoạt động đúng không
3. Khi đã kiểm tra thành công, nhấn nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với hệ thống quản lý khách hàng (CRM) để lưu trữ thông tin người dùng
2. Thêm tính năng lưu log các cuộc trò chuyện để phân tích sau này
3. Tích hợp với hệ thống thanh toán để cung cấp dịch vụ trả phí
4. Thêm tính năng gửi báo cáo định kỳ về hoạt động của chatbot

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện để tự động hóa quá trình tư vấn dinh dưỡng qua WhatsApp bằng công nghệ AI tiên tiến. Với việc tích hợp Google Gemini, chatbot có thể cung cấp các câu trả lời chính xác và chi tiết, giúp cải thiện trải nghiệm người dùng và tiết kiệm thời gian cho chuyên gia dinh dưỡng. Hãy áp dụng ngay để nâng cao hiệu quả kinh doanh của bạn!