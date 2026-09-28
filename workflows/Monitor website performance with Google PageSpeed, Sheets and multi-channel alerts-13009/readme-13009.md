---
title: "🚀 Tự động giám sát hiệu suất website với Google PageSpeed, Google Sheets và Cảnh báo đa kênh"
description: "Hướng dẫn xây dựng workflow n8n tự động kiểm tra tốc độ website bằng PageSpeed Insights, lưu log vào Google Sheets và gửi cảnh báo qua Discord, Gmail, Rapiwa."
slug: "tu-dong-giam-sat-hieu-suat-website-google-pagespeed-sheets"
tags: [n8n, automation, no-code, google-pagespeed, google-sheets, discord, monitoring]
keywords: [n8n workflow, giám sát hiệu suất website, Google PageSpeed Insights, tự động hóa n8n, cảnh báo đa kênh]
---

# 🚀 Tự động giám sát hiệu suất website với Google PageSpeed, Google Sheets và Cảnh báo đa kênh

Các sếp có đang đau đầu vì website bỗng nhiên chậm chạp, ảnh hưởng trực tiếp đến trải nghiệm người dùng và tỷ lệ chuyển đổi, nhưng lại chỉ phát hiện ra khi khách hàng phàn nàn? Việc kiểm tra tốc độ website thủ công hàng ngày bằng công cụ Google PageSpeed Insights không chỉ tốn thời gian mà còn rất dễ bỏ quên.

Được phát triển bởi **SpaGreen Creative**, workflow n8n mạnh mẽ này sẽ giải quyết triệt để vấn đề trên. Nó tự động hóa 100% quy trình: định kỳ quét hiệu suất hàng loạt URL từ Google Sheets, phân tích điểm số, lưu trữ lịch sử dữ liệu và lập tức bắn cảnh báo đa kênh qua **Discord, Gmail và Rapiwa** nếu website gặp sự cố hoặc đạt hiệu suất kém. Không cần viết code phức tạp, các sếp chỉ cần "lắp ráp" và cho chạy!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Lên lịch kiểm tra định kỳ hàng ngày/hàng tuần mà không cần sự can thiệp thủ công.
- **Giám sát hàng loạt:** Theo dõi đồng thời danh sách dài các URL website từ một bảng Google Sheets duy nhất.
- **Cảnh báo đa kênh tức thì:** Nhận thông báo ngay lập tức qua Discord, Gmail hoặc Rapiwa khi điểm số PageSpeed rớt dưới ngưỡng cho phép.
- **Lưu trữ dữ liệu minh bạch:** Tự động ghi nhận toàn bộ lịch sử điểm số và thời gian kiểm tra vào Google Sheets để dễ dàng theo dõi xu hướng (trend).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Google Account:** Tài khoản Google Sheets chứa danh sách các URL cần test và file lưu kết quả.
- **Google PageSpeed API Key:** (Tùy chọn nhưng khuyến nghị để tăng giới hạn request).
- **Kênh thông báo:** 
  - Discord Webhook/Bot.
  - Gmail Credentials (hoặc tài khoản gửi mail).
  - Tài khoản Rapiwa (cho thông báo qua WhatsApp/SMS/Chat tùy chỉnh).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy trực tiếp mã JSON, sau đó dán vào giao diện n8n Editor của các sếp (chọn **Import from File** hoặc **Paste Workflow**).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chuẩn xác các node cốt lõi sau:

- **Schedule Trigger:** Thiết lập lịch chạy tự động (ví dụ: chạy mỗi ngày 1 lần vào lúc 8h sáng).
- **Get Data Form Sheet:** Kết nối tài khoản Google Sheets của các sếp, trỏ tới file chứa danh sách URL website cần kiểm tra.
- **PageSpeed Test & PageSpeed Test2 (HTTP Request):** Cấu hình gọi API của Google PageSpeed Insights. Các sếp có thể gắn thêm `key=YOUR_GOOGLE_PAGESPEED_API_KEY` để tránh bị giới hạn request (Rate Limit).
- **Process Results & Code (Calculate Days):** Các node xử lý dữ liệu bằng Javascript giúp lọc, tính toán điểm số Performance, SEO, Accessibility, Best Practices từ kết quả JSON trả về.
- **Loop Over Items & Limit (10):** Giúp chia nhỏ danh sách URL thành các batch (lô) nhỏ kết hợp node **Wait 10s** để tránh bị Google chặn do gọi quá nhiều request cùng lúc.
- **If3 / If (check empty response):** Kiểm tra điều kiện điểm số hoặc phản hồi lỗi để quyết định có bắn thông báo hay không.
- **Send a message (Discord), Rapiwa, Send a message2 (Gmail):** Điền thông tin kênh nhận cảnh báo (Webhook URL của Discord, cấu hình Gmail gửi đi, API token của Rapiwa).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử với một vài dữ liệu mẫu từ Google Sheets.
- Kiểm tra kết quả trả về trong Google Sheets và các kênh thông báo.
- Nếu mọi thứ xanh mướt, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram/Slack:** Ngoài Discord và Gmail, các sếp có thể clone node thông báo để bắn thêm tin nhắn vào nhóm Telegram nội bộ của công ty.
- **Báo cáo tuần tự động:** Tạo thêm một nhánh chạy vào cuối tuần để tổng hợp điểm trung bình các website gửi vào email cho sếp lớn.
- **Chia ngưỡng cảnh báo:** Thiết lập điều kiện màu sắc (Đỏ/Vàng/Xanh) dựa trên điểm số PageSpeed để phân loại mức độ nghiêm trọng của lỗi.

### 📌 Kết luận
Việc kiểm tra tốc độ website chưa bao giờ dễ dàng và tự động đến thế với sự kết hợp giữa n8n, Google PageSpeed và Google Sheets. Hãy áp dụng ngay workflow này để tối ưu hóa thời gian quản trị hệ thống và đảm bảo website của các sếp luôn đạt phong độ đỉnh cao!