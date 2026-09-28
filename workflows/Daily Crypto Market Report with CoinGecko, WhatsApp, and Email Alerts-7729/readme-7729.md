---
title: "🚀 Tự Động Báo Cáo Thị Trường Crypto Hàng Ngày Qua WhatsApp & Email"
description: "Workflow n8n tự động lấy dữ liệu CoinGecko, phân tích biến động top 100 coin và gửi báo cáo chuyên sâu qua WhatsApp & Email mỗi ngày."
slug: "bao-cao-crypto-hang-ngay-coin-gecko"
tags: [n8n, crypto, coingecko, whatsapp, email-automation]
keywords: [n8n workflow crypto, tự động hóa báo cáo coin, coin gecko api n8n, gửi tin nhắn whatsapp tự động, theo dõi thị trường crypto]
---

# 🚀 Tự Động Báo Cáo Thị Trường Crypto Hàng Ngày Qua WhatsApp & Email

Thị trường Crypto biến động với tốc độ chóng mặt. Việc phải mở app, kiểm tra từng đồng coin, so sánh giá và tự động viết báo cáo gửi cho team hoặc khách hàng mỗi sáng là một gánh nặng lớn, dễ gây sai sót và mất thời gian.

Workflow **Daily Crypto Market Report** này giải quyết triệt để vấn đề đó. Nó hoạt động như một "trợ lý phân tích thị trường" tự động 100%, không cần code. Mỗi ngày, nó sẽ tự động quét dữ liệu từ CoinGecko, lọc ra những đồng coin có biến động mạnh nhất trong 24h qua, định dạng báo cáo chuyên nghiệp và gửi ngay vào điện thoại (WhatsApp) và hộp thư (Email) của bạn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 1-2 giờ mỗi ngày:** Không cần thủ công kiểm tra giá hay viết báo cáo.
- **Chính xác tuyệt đối:** Dữ liệu lấy trực tiếp từ API CoinGecko, loại bỏ lỗi con người.
- **Đa kênh thông báo:** Nhận báo cáo đồng thời qua WhatsApp (nhanh, tiện) và Email (chuyên nghiệp, lưu trữ).
- **Cá nhân hóa nội dung:** Báo cáo được định dạng sẵn, dễ đọc, tập trung vào biến động lớn nhất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Đã cài đặt và chạy (Self-hosted hoặc Cloud).
2. **API Key CoinGecko:** Đăng ký miễn phí tại [CoinGecko API](https://www.coingecko.com/en/api) (Plan Free có giới hạn request, đủ dùng cho báo cáo hàng ngày).
3. **Tài khoản WhatsApp Business API:** Cần có số điện thoại đã xác thực và credentials API (thường qua các provider như Twilio, 360dialog, hoặc Meta Cloud API).
4. **Tài khoản Email (SMTP):** Thông tin máy chủ SMTP (ví dụ: Gmail, Outlook, hoặc dịch vụ email doanh nghiệp) để gửi báo cáo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from URL** hoặc **Import from File**.
3. Dán link gốc: `https://n8n.io/workflows/7729` hoặc tải file JSON và import.
4. Workflow sẽ hiện ra với 8 nodes chính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Các sếp cần click vào từng node và cấu hình như sau:

**1. Node: `Set Configuration Variables` (Loại: Set)**
:::note[Cấu hình thông tin liên hệ]
Đây là nơi các sếp điền thông tin nhận báo cáo.
- **WhatsApp Number:** Điền số điện thoại nhận tin nhắn (định dạng quốc tế, ví dụ: `84912345678`).
- **Email Address:** Điền địa chỉ email nhận báo cáo.
- **API Key CoinGecko:** (Nếu workflow yêu cầu ở đây) Hoặc có thể điền trực tiếp ở node HTTP Request.
:::

**2. Node: `Fetch Crypto Data from CoinGecko` (Loại: HTTP Request)**
- **Method:** GET
- **URL:** Kiểm tra URL gọi API CoinGecko. Thường là `https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1&sparkline=false&price_change_percentage=24h`.
- **Headers:** Nếu dùng API Key, thêm header `x-cg-demo-api-key` với giá trị là API Key của bạn.

**3. Node: `Process Crypto Movements` (Loại: Code)**
- Node này xử lý dữ liệu thô từ CoinGecko, sắp xếp lại theo mức biến động 24h (tăng/giảm mạnh nhất).
- **Lưu ý:** Nếu muốn thay đổi số lượng coin hiển thị (ví dụ: top 10 thay vì top 5), các sếp có thể chỉnh logic trong đoạn code JavaScript ở đây.

**4. Node: `Format WhatsApp Message` (Loại: Code)**
- Node này tạo nội dung tin nhắn WhatsApp thân thiện, có emoji, dễ đọc trên mobile.
- **Mẹo:** Các sếp có thể chỉnh sửa template string trong code để thêm logo, link website, hoặc thay đổi cách trình bày (ví dụ: thêm bảng giá chi tiết).

**5. Node: `Format Email Content` (Loại: Code)**
- Node này tạo nội dung email chuyên nghiệp, có thể bao gồm HTML table để hiển thị đẹp hơn.
- **Lưu ý:** Kiểm tra phần `subject` để đặt tiêu đề email hấp dẫn (ví dụ: "📊 Báo cáo Crypto 24h: BTC tăng 5%...").

**6. Node: `Send Email Alert` (Loại: Email Send)**
- **Credentials:** Chọn credentials SMTP đã tạo trước đó.
- **From:** Email người gửi.
- **To:** Lấy từ node `Set Configuration Variables`.
- **Subject & Message:** Lấy từ node `Format Email Content`.

**7. Node: `Send message` (Loại: WhatsApp)**
- **Credentials:** Chọn credentials WhatsApp API đã tạo.
- **To:** Lấy số điện thoại từ node `Set Configuration Variables`.
- **Message:** Lấy nội dung từ node `Format WhatsApp Message`.

**8. Node: `Daily Crypto Trigger` (Loại: Cron)**
- Mặc định chạy lúc **00:00 UTC**.
- **Lưu ý quan trọng:** UTC 00:00 = **07:00 sáng giờ Việt Nam (GMT+7)**. Nếu muốn nhận báo cáo lúc 8h sáng, các sếp cần chỉnh Cron Expression thành `0 1 * * *` (tức là 01:00 UTC).

#### 3. Kích hoạt ⚡️
1. Click **Test Workflow** để chạy thử với dữ liệu mẫu.
2. Kiểm tra xem có nhận được tin nhắn WhatsApp và Email không.
3. Nếu ổn, bật **Active** để workflow chạy tự động hàng ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Telegram:** Thay thế hoặc bổ sung node Telegram để gửi báo cáo qua kênh Telegram (rất phổ biến trong cộng đồng Crypto).
- **Lọc theo Coin cụ thể:** Thay vì top 100, các sếp có thể sửa node `Fetch Crypto Data` để chỉ lấy dữ liệu của BTC, ETH, SOL... và gửi cảnh báo khi giá vượt ngưỡng nhất định.
- **Lưu lịch sử vào Google Sheets:** Thêm node Google Sheets để lưu lại dữ liệu giá hàng ngày, giúp phân tích xu hướng dài hạn.
- **Gửi báo cáo tuần/tháng:** Tạo thêm workflow khác với Cron Trigger chạy vào Chủ nhật hoặc ngày 1 hàng tháng, tổng hợp dữ liệu từ Google Sheets để gửi báo cáo tổng kết.

### 📌 Kết luận
Workflow **Daily Crypto Market Report** là công cụ không thể thiếu cho bất kỳ ai theo dõi thị trường Crypto. Với sự kết hợp giữa dữ liệu chính xác từ CoinGecko và khả năng đa kênh thông báo qua WhatsApp & Email, các sếp sẽ luôn cập nhật thông tin nhanh chóng, chuyên nghiệp và tiết kiệm tối đa thời gian. Hãy import và cấu hình ngay hôm nay để bắt đầu tự động hóa quy trình theo dõi thị trường của bạn!