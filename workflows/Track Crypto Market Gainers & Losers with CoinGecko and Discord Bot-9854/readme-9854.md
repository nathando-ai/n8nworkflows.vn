---
title: "🚀 Theo dõi Top Crypto Gainers & Losers với CoinGecko và Discord Bot"
description: "Tự động hóa theo dõi thị trường crypto hàng ngày với workflow n8n, gửi báo cáo tự động lên Discord. Tiết kiệm thời gian và nhận thông tin chính xác ngay lập tức."
slug: "theo-doi-crypto-gainers-losers-coingecko-discord"
tags: [n8n, automation, crypto, discord, no-code]
keywords: [n8n workflow, tự động hóa crypto, discord bot, theo dõi thị trường, CoinGecko]
---

# 🚀 Theo dõi Top Crypto Gainers & Losers với CoinGecko và Discord Bot

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các nhà đầu tư crypto khi phải theo dõi thủ công hàng chục đồng tiền trên nhiều trang web khác nhau. Giới thiệu workflow như giải pháp tự động hóa hoàn toàn không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Nhận báo cáo hàng ngày về top 20 đồng tăng/giảm giá trị nhất trong 24h
- Thông tin được tổng hợp từ CoinGecko - nguồn dữ liệu đáng tin cậy
- Tự động gửi thông báo lên Discord với định dạng dễ đọc
- Tiết kiệm thời gian theo dõi thủ công hàng giờ
- Nhận cảnh báo sớm về xu hướng thị trường
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Discord và quyền tạo webhook
- API Key từ CoinGecko (miễn phí)
- Kiến thức cơ bản về Discord webhook
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/9854)
2. Click vào nút "Copy Workflow" để sao chép JSON
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã copy

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Fetch Page 1" đến "Fetch Page 7"**:
   - Thêm header "x-cg-demo-api-key" với giá trị là API Key của bạn từ CoinGecko
   - Đảm bảo URL API là `https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=250&page=1&sparkline=false&price_change_percentage=24h`

2. **Node "Send Gainers Update" và "Send Losers Update"**:
   - Tạo Discord webhook và điền vào trường "Webhook URL"
   - Tùy chỉnh nội dung thông báo theo sở thích

3. **Node "Schedule Trigger"**:
   - Thiết lập thời gian chạy workflow hàng ngày (ví dụ: 8:00 sáng mỗi ngày)

#### 3. Kích hoạt ⚡️
1. Click vào nút "Test Workflow" để kiểm tra dữ liệu mẫu
2. Sau khi xác nhận hoạt động tốt, click vào nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node "Email" để nhận báo cáo qua email thay vì Discord
- Kết hợp với workflow khác để theo dõi thêm các chỉ số kỹ thuật
- Thiết lập cảnh báo khi giá của một đồng cụ thể vượt ngưỡng nhất định
- Tạo bảng tổng hợp trên Google Sheets để lưu trữ lịch sử dữ liệu

### 📌 Kết luận
Workflow này giúp các nhà đầu tư crypto tiết kiệm thời gian đáng kể trong việc theo dõi thị trường. Bằng cách tự động hóa quá trình thu thập và phân tích dữ liệu, các sếp có thể tập trung vào chiến lược đầu tư thay vì phải theo dõi thủ công hàng giờ. Hãy thử ngay và nâng cấp chiến lược đầu tư của bạn với công nghệ tự động hóa!