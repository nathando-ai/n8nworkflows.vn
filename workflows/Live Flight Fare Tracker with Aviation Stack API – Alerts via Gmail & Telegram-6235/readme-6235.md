---
title: "🚀 Tự động theo dõi giá vé máy bay với AviationStack API và cảnh báo qua Gmail, Telegram"
description: "Hướng dẫn xây dựng workflow n8n tự động săn vé máy bay giá rẻ, theo dõi biến động giá vé qua AviationStack API và gửi cảnh báo tức thì qua Gmail, Telegram."
slug: "theo-doi-gia-ve-may-bay-aviation-stack-gmail-telegram"
tags: [n8n, automation, aviation-stack, api, telegram, gmail]
keywords: [n8n workflow, theo dõi giá vé máy bay, aviation stack api, tự động hóa n8n, cảnh báo giá vé telegram gmail]
---

# 🚀 Tự động theo dõi giá vé máy bay với AviationStack API & Cảnh báo qua Gmail, Telegram

Các sếp có bao giờ đau đầu vì việc theo dõi giá vé máy bay cho các chuyến đi công tác hoặc du lịch? Việc phải tra cứu thủ công mỗi ngày trên các trang web đặt vé vừa tốn thời gian, lại rất dễ bỏ lỡ các đợt giảm giá sốc (flash sale). 

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n **Live Flight Fare Tracker**. Workflow này sẽ tự động hóa 100% quy trình: lấy dữ liệu chuyến bay thời gian thực từ AviationStack API, so sánh với lịch sử giá cũ trên Google Sheets, và bắn tin nhắn cảnh báo ngay lập tức qua Gmail hoặc Telegram khi có biến động giá.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 săn vé mà không sợ gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 24/7:** Không cần canh me thủ công, hệ thống tự động kiểm tra định kỳ theo lịch trình.
- **Bắt trọn cơ hội giá rẻ:** Nhận thông báo tức thì khi giá vé giảm sâu hoặc tăng đột biến để chớp thời cơ đặt vé.
- **Đa kênh thông báo:** Nhận alert linh hoạt qua cả Gmail (bản đẹp HTML) và Telegram (nhanh gọn trên điện thoại).
- **Lưu trữ lịch sử minh bạch:** Theo dõi biến động giá qua Google Sheets và ghi log chi tiết mọi hoạt động cảnh báo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **AviationStack API Key**: Đăng ký tài khoản miễn phí tại [aviationstack.com](https://aviationstack.com/) để lấy API key lấy thông tin chuyến bay.
- **Tài khoản Google Sheets**: Chuẩn bị sẵn một Google Sheet chứa dữ liệu lịch sử giá vé chuyến bay (ví dụ: tuyến JFK - LAX).
- **Gmail Credentials**: Kết nối tài khoản Gmail qua OAuth2 để gửi email.
- **Telegram Bot Token & Chat ID**: Tạo Bot qua `@BotFather` để gửi tin nhắn cảnh báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor, hoặc import file JSON tải từ trang chủ n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Schedule Trigger**: Thiết lập khoảng thời gian chạy (ví dụ: chạy mỗi 6 tiếng hoặc 1 lần/ngày tùy nhu cầu).
- **Fetch Flight Data (HTTP Request)**: 
  - Điền Endpoint của AviationStack API.
  - Cung cấp `httpQueryAuth` credentials chứa API Key của các sếp.
  - Điều chỉnh tham số route (ví dụ: tuyến bay JFK đi LAX).
- **Previous flight data (Google Sheets)**: 
  - Chọn Google Account credentials.
  - Trỏ tới file Google Sheet và Sheet Name lưu trữ dữ liệu giá vé lịch sử của các sếp.
- **Code**: Kiểm tra logic so sánh giữa `current_fare` (giá hiện tại) và `previous_fare` (giá cũ). Các sếp có thể tinh chỉnh ngưỡng phần trăm thay đổi (ví dụ: giảm $\ge 10\%$ hoặc tăng $\ge 15\%$) để kích hoạt cảnh báo.
- **Send a message (Gmail)**: Cấu hình Gmail OAuth2 credentials, thêm email nhận thông báo.
- **Telegram**: Cấu hình Telegram API credentials (Bot Token) và điền Chat ID nhóm hoặc cá nhân nhận tin nhắn.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để chạy thử thủ công với dữ liệu mẫu, kiểm tra xem luồng dữ liệu chạy qua các node có báo xanh (thành công) hay không.
- Sau khi test ngon lành, gạt công tắc sang **Active** để hệ thống tự động hoạt động ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin:** Tích hợp thêm node Slack hoặc Zalo ZNS để nhận thông báo đa nền tảng cùng lúc.
- **Lưu log vào Database:** Thay vì chỉ ghi log trong function node, các sếp có thể đẩy log chi tiết vào một bảng Google Sheets riêng hoặc Notion để phân tích xu hướng giá vé theo mùa.
- **Mở rộng tuyến bay:** Nhân bản luồng HTTP Request để theo dõi nhiều tuyến bay yêu thích cùng lúc (VD: SGN - HAN, HAN -DAD).

### 📌 Kết luận
Workflow **Live Flight Fare Tracker** là một trợ thủ đắc lực giúp các sếp tiết kiệm tối đa chi phí đi lại, không bỏ lỡ bất kỳ cơ hội săn vé rẻ nào. Hãy setup ngay hôm nay để tối ưu hóa công việc cá nhân hoặc tích hợp vào hệ thống doanh nghiệp của mình nhé! Chúc các sếp cài đặt thành công!