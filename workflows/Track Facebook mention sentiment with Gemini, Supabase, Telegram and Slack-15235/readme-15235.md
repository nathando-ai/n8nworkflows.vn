---
title: "🚀 Theo dõi cảm xúc nhắc đến Facebook với Gemini, Supabase, Telegram và Slack"
description: "Tự động hóa theo dõi và phân tích cảm xúc nhắc đến Facebook, lưu trữ dữ liệu và gửi cảnh báo qua Telegram/Slack - giải pháp toàn diện cho quản lý tương tác khách hàng"
slug: "theo-doi-cam-xuc-facebook-gemini-supabase-telegram-slack"
tags: [n8n, automation, no-code, social media, ai]
keywords: [n8n workflow, tự động hóa, phân tích cảm xúc, facebook, gemini, supabase]
---

# 🚀 Theo dõi cảm xúc nhắc đến Facebook với Gemini, Supabase, Telegram và Slack

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp đang gặp khó khăn khi phải theo dõi và phản hồi các nhắc đến trên Facebook một cách thủ công. Các nhắc đến tích cực và tiêu cực cần được xử lý khác nhau, nhưng quy trình thủ công dễ gây lỗi và không hiệu quả. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình từ theo dõi đến cảnh báo, giúp tiết kiệm thời gian và nâng cao trải nghiệm khách hàng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động phân tích cảm xúc và chủ đề từ các nhắc đến Facebook
- Lưu trữ dữ liệu nhắc đến trong Supabase để theo dõi và báo cáo
- Gửi cảnh báo tức thời qua Telegram cho nhắc đến tích cực
- Thông báo ngay lập tức qua Slack cho nhắc đến tiêu cực hoặc có từ khóa quan trọng
- Xử lý lỗi và gửi cảnh báo khi lưu trữ dữ liệu thất bại
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Facebook App và Page đã được cấu hình webhook
- API Key từ Google Gemini
- Dự án Supabase với bảng mentions đã được tạo
- Bot Telegram và Chat ID để nhận thông báo
- Kết nối Slack với channel đã chọn
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [workflow gốc](https://n8n.io/workflows/15235)
2. Click vào nút "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Facebook Mention Received**:
   - Cấu hình credentials cho Facebook App và Page
   - Đảm bảo webhook đã được kích hoạt cho sự kiện nhắc đến

2. **Sentiment & Topic Analysis**:
   - Thêm credentials cho Google Gemini API
   - Cấu hình prompt để trả về JSON có cấu trúc: {sentiment: string, topic: string, confidence: number}

3. **Clean AI Response**:
   - Kiểm tra và điều chỉnh code để chuẩn hóa đầu ra từ Gemini thành định dạng JSON nhất quán

4. **Store Mention (Supabase)**:
   - Thêm credentials cho Supabase API
   - Cấu hình các tham số: URL, Service Role Secret, tên bảng (ví dụ: mentions)
   - Đảm bảo bảng có các cột: id, content, sentiment, topic, confidence, timestamp

5. **Telegram (Positive Mention)**:
   - Thêm credentials cho Telegram Bot
   - Cấu hình chat ID để nhận thông báo

6. **Storage Failure (Telegram)**:
   - Sử dụng cùng credentials với node Telegram trước đó
   - Cấu hình chat ID để nhận cảnh báo lỗi

7. **Keyword & Critical Detection**:
   - Cập nhật danh sách từ khóa quan trọng trong code (ví dụ: refund, bug, cancel, slow)

8. **Slack (Critical Mention)**:
   - Thêm credentials cho Slack API
   - Chọn channel phù hợp để nhận cảnh báo

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra toàn bộ workflow
2. Kích hoạt workflow bằng cách nhấn nút "Active"

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để gửi báo cáo hàng ngày tổng hợp các nhắc đến tích cực/tiêu cực
- Kết hợp với workflow khác để tự động trả lời nhắc đến tích cực
- Cấu hình cảnh báo đa kênh (ví dụ: gửi cả Telegram và Slack cho nhắc đến quan trọng)
- Thêm phân tích chủ đề nâng cao bằng cách sử dụng các model AI khác

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc theo dõi và quản lý tương tác khách hàng trên Facebook. Bằng cách tự động hóa quy trình phân tích cảm xúc, lưu trữ dữ liệu và cảnh báo, các sếp có thể tập trung vào các nhiệm vụ quan trọng hơn và nâng cao trải nghiệm khách hàng. Hãy thử ngay và tối ưu hóa quy trình quản lý tương tác của bạn!