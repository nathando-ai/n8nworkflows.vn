---
title: "🚨 Hệ thống cảnh báo khẩn cấp an toàn phụ nữ tự động với GPT-4o-mini, Telegram và Google Sheets"
description: "Tự động hóa cảnh báo khẩn cấp an toàn phụ nữ bằng n8n: Nhận thông báo từ webhook, xử lý bằng AI, gửi Telegram và lưu Google Sheets - Giải pháp 100% không cần code"
slug: "he-thong-canh-bao-khan-cap-an-toan-phu-nu"
tags: [n8n, automation, no-code, ai, telegram, google-sheets]
keywords: [n8n workflow, tự động hóa an toàn phụ nữ, cảnh báo khẩn cấp, ai agent, google maps]
---

# 🚨 Hệ thống cảnh báo khẩn cấp an toàn phụ nữ tự động với GPT-4o-mini, Telegram và Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của phụ nữ khi gặp tình huống khẩn cấp. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phản ứng tức thì**: Cảnh báo được gửi ngay khi nhận được thông báo khẩn cấp
- **Thông tin rõ ràng**: AI tự động định dạng thông báo dễ đọc với emoji
- **Lưu trữ an toàn**: Tất cả sự kiện được ghi lại trong Google Sheets
- **Tích hợp hoàn hảo**: Kết nối liền mạch với các dịch vụ hiện có
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI (để sử dụng GPT-4o-mini)
- Bot Telegram và ID nhóm chat
- Google Sheets với quyền truy cập API
- Ứng dụng hoặc nút bấm gửi thông báo khẩn cấp
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/14359](https://n8n.io/workflows/14359)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên
4. Hoàn tất import và mở workflow trong Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Receive Emergency Alert" (webhook)**:
   - Đảm bảo đường dẫn webhook là duy nhất và bảo mật
   - Kiểm tra cấu hình HTTP Method là POST

2. **Node "OpenAI Chat Model" (lmChatOpenAi)**:
   - Thêm credentials OpenAI
   - Xác nhận model đang sử dụng là gpt-4o-mini

3. **Node "Send Alert to Telegram Group" (telegram)**:
   - Thêm credentials Telegram Bot
   - Cập nhật chatId với ID nhóm chat của bạn

4. **Node "Log Incident to Google Sheets" (googleSheets)**:
   - Thêm credentials Google Sheets OAuth2
   - Cập nhật documentId với ID bảng tính của bạn
   - Đảm bảo bảng tính có các cột: Name, Phone, Location, Timestamp

#### 3. Kích hoạt ⚡️
1. Kiểm tra cấu hình bằng cách gửi dữ liệu mẫu:
```json
{
  "name": "Nguyễn Thị A",
  "phone": "0123456789",
  "lat": 21.028511,
  "lng": 105.804817
}
```
2. Kích hoạt workflow bằng cách nhấn nút "Active" ở góc trên bên phải

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi email thông báo cho các cơ quan chức năng
- Kết nối với hệ thống GPS để cập nhật vị trí thời gian thực
- Thiết lập cảnh báo tự động khi không nhận được phản hồi trong thời gian nhất định
- Tích hợp với hệ thống quản lý sự cố để theo dõi và xử lý

### 📌 Kết luận
Hệ thống cảnh báo khẩn cấp an toàn phụ nữ này giúp các sếp:
- Giảm thiểu thời gian phản ứng
- Tăng tính chính xác của thông báo
- Tạo hồ sơ lưu trữ đầy đủ cho các trường hợp khẩn cấp
- Tích hợp liền mạch với các hệ thống hiện có

Hãy áp dụng ngay để nâng cao khả năng bảo vệ an toàn cho phụ nữ trong cộng đồng của bạn!