---
title: "🚀 Tự động hóa nâng cấp prompt AI với Multi-Agent Refinement"
description: "Hướng dẫn tự động hóa nâng cấp prompt cơ bản thành prompt chuyên nghiệp với workflow n8n sử dụng Gemini và Groq AI"
slug: "tu-dong-hoa-nang-cap-prompt-ai"
tags: [n8n, automation, no-code, ai, google-sheets]
keywords: [n8n workflow, tự động hóa, prompt engineering, ai, google sheets]
---

# 🚀 Tự động hóa nâng cấp prompt AI với Multi-Agent Refinement

[Các sếp] có bao giờ phải mất hàng giờ để chỉnh sửa và tối ưu các prompt cho AI không? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình nâng cấp prompt cơ bản thành prompt chuyên nghiệp, hoàn chỉnh với cấu trúc rõ ràng và các biến đầu vào có thể tái sử dụng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quá trình nâng cấp prompt trong vài giây
- **Chất lượng cao**: Nhận được prompt chuyên nghiệp với cấu trúc rõ ràng và các biến đầu vào có thể tái sử dụng
- **Theo dõi dễ dàng**: Tất cả các phiên bản prompt và quá trình chỉnh sửa được lưu trữ trong Google Sheets
- **Tích hợp dễ dàng**: Kết nối với các công cụ khác như Telegram để nhận thông báo kết quả
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets đã tạo theo hướng dẫn
- API keys cho:
  - Google Sheets OAuth2
  - Telegram API
  - Groq API
  - Google Palm API (Gemini)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/7067)
2. Chọn "Download" để tải file JSON
3. Trong n8n Editor, chọn "Import from File" và tải file JSON đã tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Google Sheets Trigger** và **Create/Update Modified Prompt** nodes:
   - Thay thế `Document ID` bằng ID của Google Sheets của bạn
   - Đảm bảo Google Sheets có 2 tab: `Main Sheet` và `Modified Prompt Sheet` với cấu trúc cột như hướng dẫn

2. **Qwen3 - PM** node:
   - Kiểm tra và cập nhật credentials cho Groq API
   - Đảm bảo model `qwen/qwen3-32b` đang hoạt động

3. **Gemini - PM** node:
   - Kiểm tra và cập nhật credentials cho Google Palm API
   - Đảm bảo API key còn hạn sử dụng

4. **Send Success Message To User** và **Send Exceed Limits Error** nodes:
   - Cập nhật `Chat ID` với ID chat Telegram của bạn (tùy chọn)

5. **Loop Over Items** node:
   - Điều chỉnh batch size nếu cần thiết

#### 3. Kích hoạt ⚡️
1. Thêm prompt thử nghiệm vào tab `Main Sheet` của Google Sheets
2. Chạy workflow thủ công để kiểm tra
3. Kiểm tra kết quả trong tab `Modified Prompt Sheet`
4. Bật chế độ tự động hóa bằng cách kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp với Slack**: Thay thế node Telegram bằng node Slack để nhận thông báo
2. **Lưu log chi tiết**: Thêm node để lưu log chi tiết của quá trình xử lý
3. **Gửi báo cáo định kỳ**: Thiết lập workflow để gửi báo cáo tổng hợp hàng ngày
4. **Tối ưu hóa chi phí**: Thiết lập cảnh báo khi sử dụng API gần giới hạn

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình nâng cấp prompt AI, tiết kiệm thời gian và đảm bảo chất lượng cao. Với cấu hình đơn giản và kết quả rõ ràng, đây là công cụ lý tưởng cho các chuyên gia nội dung và nhà phát triển AI.