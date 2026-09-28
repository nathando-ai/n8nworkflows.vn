---
title: "🍽️ [Tự động hóa] Theo dõi lượng calo thực phẩm qua Telegram với GPT-4 Vision & Google Sheets"
description: "Hướng dẫn chi tiết cách tự động phân tích lượng calo từ ảnh thực phẩm qua Telegram, lưu kết quả vào Google Sheets và nhận thông báo ngay lập tức"
slug: "tu-dong-hoa-theo-doi-luong-calo-thuc-pham-qua-telegram-voi-gpt-4-vision-va-google-sheets"
tags: [n8n, automation, no-code, telegram, google-sheets, ai, gpt-4]
keywords: [n8n workflow, tự động hóa, telegram, google sheets, gpt-4 vision, phân tích calo thực phẩm]
---

# 🍽️ Tự động hóa theo dõi lượng calo thực phẩm qua Telegram với GPT-4 Vision & Google Sheets

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải chụp ảnh món ăn, ghi chép lượng calo thủ công và cập nhật vào bảng tính Google Sheets? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình chỉ trong vài bước đơn giản!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần chụp ảnh và ghi chép thủ công
- **Chính xác cao**: Sử dụng trí tuệ nhân tạo GPT-4 Vision phân tích chính xác
- **Liên tục theo dõi**: Dữ liệu tự động cập nhật vào Google Sheets
- **Nhận thông báo tức thì**: Kết quả phân tích được gửi ngay qua Telegram
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot Telegram
- Tài khoản Google với quyền truy cập vào Google Sheets
- API key từ OpenAI (cho GPT-4 Vision)
- Google Sheets đã tạo sẵn với cấu trúc phù hợp
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/7006)
2. Click vào nút "Use workflow" và chọn "Import into n8n"
3. Hoặc copy toàn bộ JSON workflow và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Telegram Trigger**:
   - Cấu hình credentials cho Telegram API
   - Đảm bảo bot Telegram đã được thêm vào nhóm chat

2. **Download Telegram Image**:
   - Đảm bảo bot có quyền tải xuống file từ Telegram

3. **GPT-4 Vision Analyze**:
   - Cấu hình credentials cho OpenAI API
   - Đảm bảo tài khoản OpenAI có đủ credit để sử dụng GPT-4 Vision

4. **Log to Google Sheet**:
   - Cấu hình credentials cho Google API
   - Chỉnh sửa ID của Google Sheet và tên sheet cần ghi dữ liệu
   - Đảm bảo cấu trúc cột trong sheet phù hợp với dữ liệu đầu ra

5. **Send GPT Result**:
   - Đảm bảo bot có quyền gửi tin nhắn trong nhóm chat

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Bật Active workflow để chạy liên tục

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để gửi báo cáo hàng ngày về lượng calo tiêu thụ
- Kết hợp với các dịch vụ khác như Slack hoặc Email để nhận thông báo
- Tạo biểu đồ tự động trong Google Sheets để trực quan hóa dữ liệu
- Thêm chức năng nhắc nhở uống nước khi lượng calo tiêu thụ cao

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc theo dõi lượng calo hàng ngày. Với sự kết hợp của trí tuệ nhân tạo và tự động hóa, các sếp có thể dễ dàng duy trì chế độ ăn uống lành mạnh mà không cần phải làm thủ công. Hãy thử ngay và trải nghiệm sự tiện lợi của tự động hóa!