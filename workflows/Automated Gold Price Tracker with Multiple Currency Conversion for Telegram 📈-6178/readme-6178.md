---
title: "🚀 Theo dõi giá vàng tự động & chuyển đổi đa tiền tệ qua Telegram 📈"
description: "Workflow n8n giúp tự động lấy giá vàng, chuyển đổi sang nhiều đồng tiền và gửi báo cáo qua Telegram mỗi ngày – tiết kiệm thời gian, giảm sai sót và luôn cập nhật dữ liệu chính xác."
slug: "gold-price-tracker-telegram"
tags: [n8n, automation, no-code, crypto, gold, telegram]
keywords: [gold price tracker, n8n workflow, currency conversion, telegram bot, crypto trading]
---

# 🚀 Theo dõi giá vàng tự động & chuyển đổi đa tiền tệ qua Telegram 📈

Bạn đang phải lướt web, copy giá vàng, tính chuyển đổi tiền tệ và gửi tin nhắn cho đồng nghiệp? Thật là mất thời gian và dễ sai sót. Workflow này sẽ tự động thực hiện mọi bước: lấy giá vàng, chuyển đổi sang các đồng tiền bạn quan tâm, chuẩn bị báo cáo và gửi ngay qua Telegram – hoàn toàn không cần code.

:::info[Hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thao tác thủ công, workflow tự động chạy theo lịch.  
- **Độ chính xác cao**: Dữ liệu lấy trực tiếp từ API, tránh sai sót khi copy-paste.  
- **Cá nhân hóa**: Thêm nhiều đồng tiền, điều chỉnh nội dung báo cáo dễ dàng.  
- **Hoạt động liên tục**: Chạy 24/7, gửi báo cáo ngay khi có dữ liệu mới.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Telegram Bot**: Tạo bot qua BotFather, lấy **Telegram API Token** và lưu vào Credentials “telegramApi”.  
- **API giá vàng**: Ví dụ https://api.metals.live/v1/price?metal=gold.  
- **API chuyển đổi tiền tệ**: Ví dụ https://api.exchangerate.host/convert?from=USD&to=EUR.  
- **Danh sách đồng tiền**: Định nghĩa trong node “Set Currency” (ví dụ: USD, EUR, GBP).  
- **N8N Self-hosted**: Đã cài đặt và chạy phiên bản n8n.  
:::

## 🚀 Cách import & Lưu ý khi “lên đồ”

### 1. Import Workflow 📥

1. Tải file JSON từ link gốc: <https://n8n.io/workflows/6178> hoặc sao chép toàn bộ JSON.  
2. Mở n8n Editor → **Import** → **Import from Clipboard** hoặc **Import from File**.  
3. Dán JSON và nhấn **Import**. Workflow sẽ xuất hiện trong danh sách.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên node | Mô tả | Cấu hình cần chỉnh |
|------|----------|-------|---------------------|
| 1 | **Schedule Trigger** | Định kỳ chạy workflow. | Thời gian chạy (ví dụ: 08:00 UTC). |
| 2 | **Report: Prepare** | Viết logic tạo nội dung tin nhắn. | Đảm bảo `{{ $json["goldPrice"] }}` và `{{ $json["converted"] }}` được truyền đúng. |
| 3 | **Send a text message** | Gửi tin nhắn tới Telegram. | Chọn Credentials “telegramApi”, nhập `chatId` (ID nhóm/đối tượng). |
| 4 | **Convert Currency** | Gọi API chuyển đổi tiền tệ. | URL: `https://api.exchangerate.host/convert?from={{$json["currency"]}}&to={{$json["target"]}}&amount={{$json["goldPrice"]}}`. |
| 5 | **Fetch Price** | Lấy giá vàng. | URL: `https://api.metals.live/v1/price?metal=gold`. |
| 6 | **Set Currency** | Định nghĩa danh sách đồng tiền cần chuyển đổi. | Thêm trường `currency` (mảng). |
| 7 | **Merge** | Kết hợp dữ liệu từ các node trước. | Đặt `mode` là “Append” để gộp dữ liệu. |

> **Lưu ý**: Đảm bảo các node “Convert Currency” và “Fetch Price” trả về dữ liệu JSON có cấu trúc đúng, tránh lỗi khi merge.

### 3. Kích hoạt ⚡️

1. **Test run**: Chạy workflow thủ công (Run once) để kiểm tra dữ liệu.  
2. Kiểm tra log, xác nhận tin nhắn được gửi tới Telegram.  
3. Khi mọi thứ ổn, bật **Active** để workflow tự động chạy theo lịch.

## ✍️ Mẹo & gợi ý nâng cao

- **Thêm Slack**: Sử dụng node Slack để gửi báo cáo cùng lúc tới kênh Slack.  
- **Lưu log vào Google Sheets**: Dùng node Google Sheets để ghi lại lịch sử giá vàng và tỷ giá.  
- **Báo cáo định kỳ**: Thêm node “Schedule Trigger” thứ hai để gửi báo cáo tuần/hoặc tháng.  
- **Tùy chỉnh nội dung**: Thêm inline buttons trong Telegram để người dùng chọn đồng tiền muốn xem ngay.  

## 📌 Kết luận

Workflow “Automated Gold Price Tracker with Multiple Currency Conversion for Telegram” giúp các sếp luôn nắm bắt giá vàng và tỷ giá một cách nhanh chóng, chính xác và không tốn công sức. Hãy thử triển khai ngay, điều chỉnh theo nhu cầu và tận hưởng lợi ích của tự động hóa 100% no-code!