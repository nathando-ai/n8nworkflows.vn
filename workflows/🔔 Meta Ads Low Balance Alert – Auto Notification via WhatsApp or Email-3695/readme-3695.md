---
title: "🔔 Meta Ads Low Balance Alert – Tự động cảnh báo khi tài khoản quảng cáo sắp hết tiền qua WhatsApp/Email"
description: "Giải pháp tự động hóa hoàn toàn không cần code để theo dõi số dư tài khoản Meta Ads và nhận cảnh báo ngay khi số dư thấp, giúp các sếp quản lý quảng cáo hiệu quả hơn."
slug: "meta-ads-low-balance-alert-whatsapp-email"
tags: [n8n, automation, no-code, marketing, meta-ads]
keywords: [n8n workflow, tự động hóa, meta ads, cảnh báo số dư, email, whatsapp]
---

# 🔔 Meta Ads Low Balance Alert – Tự động cảnh báo khi tài khoản quảng cáo sắp hết tiền qua WhatsApp/Email

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Khi quản lý nhiều tài khoản quảng cáo Meta Ads, các sếp thường phải theo dõi số dư tài khoản hàng ngày để tránh tình trạng quảng cáo bị dừng đột ngột. Việc này tốn thời gian và dễ bỏ sót. Workflow này sẽ tự động kiểm tra số dư tài khoản Meta Ads định kỳ và gửi cảnh báo qua WhatsApp hoặc Email ngay khi số dư thấp hơn ngưỡng cài đặt.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Không cần theo dõi số dư tài khoản hàng ngày.
- Chính xác: Nhận cảnh báo ngay khi số dư thấp, tránh tình trạng quảng cáo bị dừng đột ngột.
- Cá nhân hóa: Cài đặt ngưỡng cảnh báo theo nhu cầu của từng tài khoản.
- Hoạt động liên tục: Workflow chạy tự động định kỳ, không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Meta Ads với quyền truy cập API.
- Tài khoản Google Workspace để gửi Email thông qua Gmail.
- Tài khoản WhatsApp Business API (nếu muốn gửi cảnh báo qua WhatsApp).
- Google Sheets để lưu trữ dữ liệu số dư tài khoản.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/3695).
2. Nhấn nút "Download" để tải file JSON.
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Meta Ads**: Cấu hình API credentials và endpoint để lấy thông tin số dư tài khoản.
  - Điền `Account ID` và `Access Token` từ tài khoản Meta Ads.
  - Endpoint mẫu: `https://graph.facebook.com/v18.0/act_{Account_ID}/insights?fields=account_id,account_name,account_currency,balance&access_token={Access_Token}`.
- **Google Sheets**: Cấu hình Google Sheets credentials và chỉ định Sheet ID, tên Sheet để lưu trữ dữ liệu số dư.
  - Điền `Sheet ID` và `Sheet Name` từ Google Sheets.
- **Gmail**: Cấu hình Gmail credentials để gửi Email cảnh báo.
  - Điền `Email Address` và `Password` từ tài khoản Gmail.
- **WhatsApp**: Cấu hình WhatsApp Business API credentials để gửi cảnh báo qua WhatsApp.
  - Điền `Phone Number ID` và `Access Token` từ tài khoản WhatsApp Business API.
- **Schedule Trigger**: Cài đặt thời gian chạy workflow định kỳ (ví dụ: hàng ngày lúc 8h sáng).
  - Điền `Cron Expression` để chỉ định thời gian chạy (ví dụ: `0 8 * * *` để chạy hàng ngày lúc 8h sáng).

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
- Bật Active workflow để chạy tự động định kỳ.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận cảnh báo qua các kênh khác.
- Lưu log cảnh báo vào Google Sheets để theo dõi lịch sử số dư tài khoản.
- Gửi báo cáo định kỳ về số dư tài khoản qua Email để quản lý hiệu quả hơn.

### 📌 Kết luận
Workflow này giúp các sếp quản lý tài khoản Meta Ads hiệu quả hơn bằng cách tự động cảnh báo khi số dư thấp. Hãy áp dụng ngay để tiết kiệm thời gian và tránh rủi ro quảng cáo bị dừng đột ngột.