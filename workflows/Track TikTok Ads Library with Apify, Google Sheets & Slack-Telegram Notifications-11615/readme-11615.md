---
title: "🚀 Theo dõi quảng cáo TikTok với Apify, Google Sheets & Thông báo Slack/Telegram"
description: "Tự động theo dõi quảng cáo TikTok của đối thủ, lưu vào Google Sheets và nhận thông báo ngay khi có quảng cáo mới xuất hiện"
slug: "theo-doi-quang-cao-tiktok-voi-apify-google-sheets-slack-telegram"
tags: [n8n, automation, no-code, apify, google-sheets, slack, telegram]
keywords: [n8n workflow, tự động hóa, theo dõi quảng cáo, tiktok, apify, google sheets, slack, telegram]
---

# 🚀 Theo dõi quảng cáo TikTok với Apify, Google Sheets & Thông báo Slack/Telegram

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải theo dõi thủ công các quảng cáo TikTok của đối thủ không? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình theo dõi, lưu trữ và thông báo về các quảng cáo mới một cách hoàn toàn không cần code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần theo dõi thủ công mỗi ngày
- **Chính xác**: Lấy dữ liệu trực tiếp từ TikTok thông qua Apify
- **Cá nhân hóa**: Theo dõi đối thủ hoặc từ khóa cụ thể
- **Hoạt động liên tục**: Nhận thông báo ngay khi có quảng cáo mới
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Apify và API key
- Tài khoản Google và Google Sheets API credentials
- Tài khoản Slack/Telegram (tùy chọn)
- ID của đối thủ TikTok (advertiserID) hoặc từ khóa tìm kiếm
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/11615)
2. Click vào nút "Import" và chọn "Import from URL"
3. Dán link workflow vào ô nhập liệu
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Set Parameters** (Node đầu tiên):
   - Điền các tham số cần theo dõi:
     - Target Country (mã ISO 3166 của quốc gia)
     - Date From/Date To (ngày bắt đầu và kết thúc theo dõi)
     - Advertiser name hoặc keyword (tên đối thủ hoặc từ khóa tìm kiếm)
     - Advertiser ID (nếu có)
     - Limit (giới hạn số lượng quảng cáo cần lấy)

2. **Get TT Ads through Apify**:
   - Chọn credentials Apify API
   - Đảm bảo đã cài đặt đúng actor TikTok Ads Scraper

3. **Read existing IDs & Append or update row in sheet**:
   - Chọn credentials Google Sheets OAuth2 API
   - Điền chính xác Spreadsheet ID và Sheet Name
   - Đảm bảo cấu trúc cột trong Google Sheets phù hợp với dữ liệu đầu ra

4. **Send a message (Slack) & Send a text message (Telegram)**:
   - Chọn credentials tương ứng
   - Điền chính xác Channel ID (Slack) hoặc Chat ID (Telegram)
   - Tùy chỉnh nội dung thông báo theo nhu cầu

#### 3. Kích hoạt ⚡️
1. Click vào nút "Activate" trên node "Schedule Trigger"
2. Chọn tần suất chạy (ví dụ: hàng ngày lúc 9h sáng)
3. Click "OK" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để lưu log hoạt động vào Google Sheets
- Kết hợp với workflow khác để phân tích dữ liệu quảng cáo
- Thiết lập nhiều đối thủ hoặc từ khóa khác nhau trong cùng một workflow
- Tạo báo cáo định kỳ về xu hướng quảng cáo của đối thủ

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian quý giá trong việc theo dõi quảng cáo TikTok. Với khả năng tự động hóa hoàn toàn và thông báo tức thì, các sếp có thể tập trung vào các chiến lược quan trọng hơn. Hãy thử ngay và bắt đầu theo dõi đối thủ của mình một cách hiệu quả!