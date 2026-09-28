---
title: "🚀 Tạo Hình Ảnh Từ Văn Bản Bằng Gemini & Telegram - Workflow N8N Tự Động Hóa"
description: "Tự động tạo hình ảnh từ văn bản thông qua Telegram với công nghệ Gemini của Google. Giải phóng thời gian sáng tạo với workflow n8n không cần code."
slug: "tao-hinh-anh-tu-van-ban-bang-gemini-telegram"
tags: [n8n, automation, no-code, telegram, google-gemini]
keywords: [n8n workflow, tự động hóa, tạo hình ảnh, gemini, telegram]
---

# 🚀 Tạo Hình Ảnh Từ Văn Bản Bằng Gemini & Telegram - Workflow N8N Tự Động Hóa

[Các sếp đang mệt mỏi với việc tạo hình ảnh từ văn bản thủ công? Hãy để workflow n8n kết hợp công nghệ Gemini của Google và Telegram giải quyết vấn đề này một cách hoàn hảo!]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tạo hình ảnh chỉ với 1 tin nhắn Telegram
- **Chất lượng cao**: Hình ảnh được tạo từ prompt được tối ưu bởi AI Gemini
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công
- **Tích hợp sẵn**: Kết quả được gửi trực tiếp về Telegram
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot Telegram
- API Key của Google Gemini (Google Palm API)
- Tài khoản n8n đã cài đặt các node cần thiết (telegram, httpRequest, convertToFile, chainLlm, lmChatGoogleGemini, outputParserStructured)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Click vào "Import from URL" và nhập link: [https://n8n.io/workflows/5777](https://n8n.io/workflows/5777)
3. Hoặc copy nội dung JSON từ link trên và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Telegram Trigger**:
   - Cấu hình credentials cho Telegram API
   - Đảm bảo bot Telegram đã được kích hoạt và có quyền gửi tin nhắn

2. **Gemini 2.5 Pro**:
   - Cấu hình credentials cho Google Palm API
   - Đảm bảo API Key có quyền truy cập vào Gemini 2.5 Pro

3. **Generate Image**:
   - Kiểm tra endpoint API của Google Gemini 2.0 Flash
   - Đảm bảo có quyền truy cập và đủ credit để sử dụng API

4. **Send a photo message**:
   - Cấu hình credentials cho Telegram API
   - Đảm bảo bot có quyền gửi hình ảnh

#### 3. Kích hoạt ⚡️
1. Test run với dữ liệu mẫu (ví dụ: "Một con mèo đang ngồi trên một chiếc ghế gỗ cổ")
2. Kiểm tra kết quả trên Telegram
3. Bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack để nhận thông báo khi có hình ảnh mới được tạo
- Lưu log các yêu cầu tạo hình ảnh vào Google Sheets
- Thêm tính năng lưu trữ hình ảnh vào Google Drive
- Tích hợp với các công cụ chỉnh sửa hình ảnh khác để tối ưu kết quả

### 📌 Kết luận
Workflow này mang lại giải pháp hoàn hảo cho các sếp muốn tự động hóa quá trình tạo hình ảnh từ văn bản. Với sự kết hợp của công nghệ Gemini và Telegram, các sếp có thể tạo ra những hình ảnh chất lượng cao chỉ với vài thao tác đơn giản. Hãy thử ngay và giải phóng thời gian sáng tạo của mình!