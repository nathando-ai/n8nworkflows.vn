---
title: "💰 Theo dõi chi tiêu từ Telegram đến Google Sheets với GPT-4.1 Mini"
description: "Hướng dẫn tự động hóa theo dõi chi tiêu qua Telegram và Google Sheets với GPT-4.1 Mini - giải pháp tiết kiệm thời gian và chính xác cho cá nhân và doanh nghiệp nhỏ"
slug: "theo-doi-chi-tieu-telegram-google-sheets-gpt-4-1-mini"
tags: [n8n, automation, no-code, telegram, google-sheets, ai, gpt-4]
keywords: [n8n workflow, tự động hóa chi tiêu, telegram bot, google sheets, gpt-4.1 mini, theo dõi tài chính]
---

# 💰 Theo dõi chi tiêu từ Telegram đến Google Sheets với GPT-4.1 Mini

[Đoạn mở đầu: Phân tích nỗi đau thực tế của cá nhân và doanh nghiệp nhỏ khi theo dõi chi tiêu thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Theo dõi chi tiêu chỉ với vài cú nhấn phím trên Telegram
- Chính xác: GPT-4.1 Mini phân tích và cấu trúc dữ liệu chi tiêu một cách chính xác
- Cá nhân hóa: Lưu trữ dữ liệu chi tiêu trong Google Sheets của riêng bạn
- Hoạt động liên tục: Theo dõi chi tiêu bất cứ lúc nào, bất cứ nơi đâu
- Tích hợp dễ dàng: Kết nối với các công cụ tài chính khác trong hệ sinh thái Google
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và một bot token (tạo qua [BotFather](https://t.me/botfather))
- Tài khoản OpenAI với quyền truy cập GPT-4.1 Mini
- Google Sheet với các cột: `Date`, `Amount`, `Currency`, `Category`, `Description`, `SourceMessage`
- Tài khoản n8n (self-hosted hoặc cloud)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/6970)
2. Chọn "Download" để tải file JSON
3. Trong n8n Editor, nhấn "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

**Node Telegram Trigger**:
- Thêm credentials cho Telegram API
- Điền bot token đã tạo từ BotFather

**Node OpenAI Chat Model**:
- Thêm credentials cho OpenAI API
- Chọn model là `gpt-4.1-mini`
- Cấu hình system prompt để trả về JSON với cấu trúc:
```json
{
  "relevant": boolean,
  "expense_record": {
    "date": string,
    "amount": number,
    "currency": string,
    "category": string,
    "description": string,
    "source": string
  },
  "message": string
}
```

**Node Google Sheets**:
- Thêm credentials cho Google Sheets OAuth2 API
- Chọn operation là `append`
- Điền ID của Google Sheet và tên sheet cần ghi dữ liệu

#### 3. Kích hoạt ⚡️
1. Test run với dữ liệu mẫu (ví dụ: "Mua cà phê 50k tại Highlands")
2. Kiểm tra kết quả trên Google Sheet và Telegram
3. Bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thêm hỗ trợ nhiều loại tiền tệ: Cập nhật system prompt để nhận diện và trích xuất các loại tiền tệ khác nhau
- Mở rộng danh mục chi tiêu: Sửa đổi danh sách danh mục trong system prompt
- Theo dõi nhiều người dùng: Thêm cột `username` hoặc `chat ID` vào Google Sheet
- Thêm cảnh báo: Kết nối với Slack, Email hoặc Telegram để cảnh báo khi chi tiêu vượt ngân sách
- Tóm tắt tuần: Sử dụng node cron + truy vấn Google Sheet + gửi tin nhắn Telegram
- Bảng điều khiển trực quan: Kết nối sheet với Looker Studio hoặc Google Data Studio

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện để theo dõi chi tiêu một cách tự động, chính xác và tiện lợi. Với sự kết hợp của Telegram, GPT-4.1 Mini và Google Sheets, các sếp có thể quản lý tài chính cá nhân hoặc của doanh nghiệp nhỏ một cách hiệu quả hơn. Hãy thử ngay và tiết kiệm thời gian quý giá của bạn!