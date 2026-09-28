---
title: "🚀 Tự động nhận thông báo Telegram khi nội dung website thay đổi bằng n8n"
description: "Hướng dẫn cài đặt workflow n8n giúp theo dõi sự thay đổi nội dung website tự động 24/7 và gửi cảnh báo ngay lập tức qua Telegram."
slug: "thong-bao-thay-doi-noi-dung-website-telegram-n8n"
tags: [n8n, automation, no-code, website-monitoring, telegram, web-scraping]
keywords: [n8n workflow, theo dõi thay đổi website, thông báo telegram, tự động hóa n8n, giám sát website]
---

# 🚀 Tự động nhận thông báo Telegram khi nội dung website thay đổi với n8n

Các sếp có bao giờ phải F5 liên tục một trang web quan trọng để chờ cập nhật giá sản phẩm, tin tức tuyển dụng, hay thông báo mới không? Việc này vừa tốn thời gian, vừa cực kỳ mệt mỏi. 

Đừng lo, bài toán đó sẽ được giải quyết triệt để với workflow n8n **"Message on website content changed in Telegram"** do tác giả *MC Naveen* thiết kế. Workflow này sẽ tự động crawl nội dung website định kỳ, so sánh sự thay đổi và bắn tin báo cáo thẳng vào Telegram cho các sếp ngay khi có biến động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Không cần thủ công kiểm tra website mỗi ngày.
- **Cảnh báo chớp nhoáng:** Nhận tin nhắn Telegram ngay lập tức khi trang web có thay đổi nội dung.
- **Hoạt động không nghỉ:** Chạy ngầm 24/7 nhờ cơ chế lịch trình (Cron) tự động.
- **Lọc nhiễu thông minh:** Chỉ thông báo khi thực sự có sự khác biệt về nội dung so với lần kiểm tra trước.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một server n8n đã được cài đặt sẵn sàng.
- Tài khoản **Telegram Bot** (lấy Bot Token qua `@BotFather`) và Chat ID của các sếp hoặc nhóm Telegram cần nhận tin.
- URL của trang web cần theo dõi nội dung.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON từ link gốc hoặc tạo mới workflow và copy/paste cấu trúc 7 nodes vào n8n Editor của mình. Workflow bao gồm các thành phần chính: **Cron** (Lịch chạy), **HTTP Request / HTTP Request1** (Lấy dữ liệu web), **Wait** (Độ trễ), **IF** (So sánh điều kiện), **Telegram1** (Gửi tin nhắn) và **NoOp** (Node rỗng giữ luồng).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần chú ý cấu hình các node cốt lõi sau:
- **Cron:** Thiết lập tần suất muốn kiểm tra website (Ví dụ: Chạy mỗi giờ, mỗi ngày hoặc mỗi 30 phút).
- **HTTP Request & HTTP Request1:** Điền URL của website các sếp muốn theo dõi nội dung vào phần tham số request.
- **IF:** Cấu hình điều kiện so sánh dữ liệu cũ và dữ liệu mới trả về từ các HTTP Request để phát hiện sự thay đổi.
- **Telegram1:** Chọn **Credentials** là tài khoản Telegram API của sếp, sau đó điền `Chat ID` và soạn nội dung thông báo tùy chỉnh (Ví dụ: *"Cảnh báo! Website [URL] vừa có thay đổi nội dung!"*).

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để test thử nghiệm xem luồng dữ liệu có chạy trơn tru hay không.
- Nếu mọi thứ xanh mướt, hãy gạt công tắc sang **Active** để bật chế độ tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Slack/Discord:** Ngoài Telegram, các sếp có thể nối thêm node Slack để bắn thông báo đa kênh cho đội ngũ cùng nắm bắt.
- **Lưu lịch sử vào Google Sheets:** Thêm node Google Sheets để ghi lại nhật ký mỗi lần website thay đổi phục vụ việc tra cứu về sau.
- **Sử dụng AI tóm tắt nội dung:** Kết hợp thêm các node AI (như OpenAI) để phân tích xem đoạn nội dung nào trên web vừa thay đổi và tóm tắt ngắn gọn vào tin nhắn Telegram.

### 📌 Kết luận
Chỉ với vài phút thiết lập workflow n8n đơn giản, các sếp đã sở hữu ngay một "trợ lý ảo" giám sát website chuyên nghiệp, không bỏ sót bất kỳ biến động quan trọng nào. Lên đồ và áp dụng ngay thôi nào!