---
title: "🚀 Xây dựng Dashboard Theo dõi Trễ Chuyến Bay Trực Tuyến với n8n, FlightStats, Google Sheets & Slack"
description: "Tự động hóa việc theo dõi tình trạng trễ chuyến bay từ FlightStats API, lưu trữ vào Google Sheets và gửi cảnh báo tức thì qua Slack khi có sự cố nghiêm trọng."
slug: "live-airport-delay-dashboard-n8n-flightstats-google-sheets-slack"
tags: [n8n, automation, no-code, flightstats, google-sheets, slack, api-integration]
keywords: [n8n workflow, theo dõi chuyến bay, flightstats api, google sheets automation, slack alert, tự động hóa n8n]
---

# 🚀 Xây dựng Dashboard Theo dõi Trễ Chuyến Bay Trực Tuyến với n8n, FlightStats, Google Sheets & Slack

Các sếp làm trong ngành du lịch, logistics, hoặc thường xuyên phải điều phối lịch trình chắc chắn hiểu rõ cảm giác "đau đầu" khi phải cập nhật thủ công tình trạng trễ chuyến bay. Việc kiểm tra liên tục các trang web tra cứu vừa tốn thời gian, vừa dễ bỏ lỡ các thông tin quan trọng dẫn đến việc xử lý khủng hoảng chậm trễ.

Giải pháp là gì? Hãy để **n8n** thay các sếp làm việc đó 24/7 hoàn toàn tự động! Workflow này sẽ kết nối trực tiếp với FlightStats API để lấy dữ liệu trễ chuyến bay theo lịch trình, tự động ghi nhận vào Google Sheets để làm báo cáo, đồng thời lọc và gửi cảnh báo thông minh qua Slack chỉ khi có sự cố nghiêm trọng xảy ra.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Thay vì canh lịch bay thủ công, hệ thống tự kích hoạt theo lịch trình (Cron) mỗi giờ hoặc mỗi ngày.
- **Lưu trữ dữ liệu khoa học**: Mọi thông tin cập nhật từ API được đồng bộ thẳng vào Google Sheets, giúp đội ngũ dễ dàng theo dõi và tra cứu lại lịch sử.
- **Cảnh báo thông minh**: Phân loại mức độ trễ. Chỉ những chuyến bay trễ nghiêm trọng mới kích hoạt tin nhắn báo động qua Slack, tránh làm phiền đội ngũ với các độ trễ nhỏ (thông qua nhánh xử lý `No Action`).
- **Nâng cao chất lượng dịch vụ**: Giúp đội ngũ sales và vận hành chủ động liên hệ khách hàng hoặc điều phối kế hoạch kịp thời.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **FlightStats API Key**: Tài khoản và API key từ nhà cung cấp dữ liệu hàng không FlightStats (hoặc dịch vụ tương đương).
- **Google Sheets Credentials**: Tài khoản Google có quyền tạo và chỉnh sửa file Google Sheets.
- **Slack Bot Token/Webhook**: Token kết nối với Slack Workspace để gửi tin nhắn cảnh báo kênh nội bộ.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này hoặc copy đoạn mã JSON từ nguồn gốc.
- Mở n8n Editor, chọn **Import from File** hoặc dán trực tiếp vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động trơn tru, các sếp cần cấu hình chính xác các node sau:

- **Set Schedule (Cron)**: 
  - Node này quyết định tần suất quét dữ liệu. Các sếp có thể chỉnh thời gian chạy theo giờ (`Hourly`) hoặc theo ngày (`Daily`) tùy theo nhu cầu thực tế của doanh nghiệp.
- **FlightStats API (HTTP Request)**: 
  - Điền Endpoint URL của FlightStats API.
  - Thêm API Key của các sếp vào phần Header Authentication (thường là `AppKey` hoặc `Authorization`).
- **Set Output Data (Google Sheets)**: 
  - Chọn Credentials Google API đã kết nối.
  - Chọn file Google Sheets và Sheet Name cụ thể để hệ thống tự động `append` (thêm dòng mới) dữ liệu chuyến bay vào.
- **Merge API Data (If Node)**: 
  - Thiết lập điều kiện lọc (ví dụ: `delay_minutes > 60` hoặc theo tiêu chí nghiêm trọng của các sếp).
  - Nhánh `true` sẽ đi đến cảnh báo, nhánh `false` sẽ đi qua node bỏ qua.
- **Send Response via Slack**: 
  - Kết nối Slack Credentials.
  - Chọn Channel nhận tin nhắn cảnh báo (ví dụ: `#ops-alerts` hoặc `#flight-updates`) và soạn nội dung thông báo kèm biến dữ liệu từ API.
- **No Action for Minor Delays (NoOp)**: 
  - Node trung gian giữ nguyên trạng thái cho các chuyến bay trễ nhẹ, không cần cấu hình phức tạp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử nghiệm với dữ liệu mẫu xem API có phản hồi tốt và dữ liệu có đẩy vào Google Sheets thành công hay không.
- Sau khi test ngon lành, gạt công tắc sang **Active** để workflow chính thức chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram/Zalo**: Ngoài Slack, các sếp có thể nhân bản nhánh cảnh báo để bắn tin nhắn qua Telegram Bot nếu đội ngũ dùng Telegram làm kênh liên lạc chính.
- **Gửi Email tự động**: Kết hợp thêm node Gmail/SMTP để tự động gửi email thông báo xin lỗi hoặc cập nhật lịch trình cho khách hàng VIP khi phát hiện chuyến bay trễ nghiêm trọng.
- **Lưu log lỗi**: Thêm một nhánh Error Trigger để nếu API FlightStats bị lỗi (timeout hoặc hết quota), hệ thống sẽ gửi cảnh báo về một kênh Slack riêng để kỹ thuật viên xử lý kịp thời.

### 📌 Kết luận
Việc tự động hóa theo dõi trễ chuyến bay không chỉ giúp tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần mà còn nâng tầm chuyên nghiệp cho doanh nghiệp trong mắt khách hàng. Hãy "lên đồ" ngay bộ workflow này trên n8n để tối ưu hóa quy trình vận hành của các sếp nhé!