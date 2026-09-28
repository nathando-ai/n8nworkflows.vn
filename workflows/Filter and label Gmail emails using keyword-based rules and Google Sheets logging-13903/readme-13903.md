---
title: "🚀 Tự động phân loại và quản lý email Gmail thông minh với n8n và Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động lọc email đến qua từ khóa, phân loại nhãn Gmail thông minh (Outreach, Marketing, Legitimate) và lưu log vào Google Sheets."
slug: "tu-dong-phan-loai-email-gmail-voi-n8n"
tags: [n8n, automation, gmail, google-sheets, ai-summarization]
keywords: [n8n workflow, tự động hóa gmail, lọc email tự động, quản lý email n8n, google sheets logging]
---

# 🚀 Tự động phân loại và quản lý email Gmail thông minh với n8n và Google Sheets

Các sếp có bao giờ cảm thấy ngợp thở mỗi khi mở hộp thư đến (Inbox) với hàng chục, hàng trăm email quảng cáo, chào hàng (cold outreach) và thư rác mỗi ngày? Việc lọc thủ công tốn rất nhiều thời gian và dễ bỏ lỡ các email quan trọng.

Giải pháp ở đây là gì? Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình đọc, phân tích, dán nhãn (label) và lưu vết email vào Google Sheets mà không cần tốn một xu chi phí cho các phần mềm trả phí phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Lọc sạch hộp thư đến ngay khi có email mới ghé thăm nhờ **Gmail Trigger**.
- **Phân loại thông minh**: Tự động nhận diện Cold Outreach, Marketing/Ads, Needs Review và Legitimate dựa trên từ khóa.
- **Tổ chức khoa học**: Tự động gán nhãn Gmail, đánh dấu đã đọc (Mark as Read) và dọn dẹp Inbox.
- **Lưu trữ minh bạch**: Tự động ghi lại log chi tiết vào Google Sheets (Thời gian, Người gửi, Tiêu đề, Phân loại).
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI LÊN ĐỒ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản Google có quyền truy cập **Gmail** và **Google Sheets**.
- Chuẩn bị sẵn 4 nhãn (Labels) trong Gmail: `Cold Outreach`, `Marketing`, `Needs Review`, `Legitimate`.
- Tạo sẵn một Google Sheet với các cột tương ứng để lưu log (Timestamp, Sender, Subject, Classification).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình các node cốt lõi sau:
- **Gmail Trigger & Get a message**: Kết nối tài khoản Gmail của các sếp (OAuth2) để n8n có quyền đọc và quản lý thư.
- **Analyze Email Content (Node Code)**: Nơi chứa logic quét từ khóa trong tiêu đề và nội dung tóm tắt (snippet) của email. Các sếp có thể tùy chỉnh danh sách từ khóa (ví dụ: *sales outreach, partnership opportunity, newsletter, promotion*...) cho phù hợp với nghành nghề của mình.
- **Các node Gmail Actions** (*Label as Outreach, Remove from Inbox, Mark as Read, Label as Legitimate, Label as Needs Review, Label as Marketing/Ads*): Chọn đúng tài khoản Gmail và ánh xạ chính xác tên nhãn (Labels) đã tạo sẵn trong Gmail của các sếp.
- **Log to Spreadsheet (outreach / needs review / legitimate / marketing/Ads)**: Kết nối tài khoản Google Sheets, chọn đúng file Google Sheet và bảng tính (Sheet Name) dùng để lưu log dữ liệu.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một email test để kiểm tra xem hệ thống đã phân loại và log vào Google Sheets chính xác chưa.
- Nếu mọi thứ chạy trơn tru, hãy bật công tắc **Active** góc trên cùng bên phải để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot**: Thêm node Telegram hoặc Slack vào nhánh *Needs Review* hoặc *Cold Outreach* để nhận thông báo ngay lập tức trên điện thoại.
- **Mở rộng AI**: Có thể thay thế hoặc kết hợp node Code phân tích từ khóa bằng OpenAI / Claude Node để AI đọc hiểu ngữ cảnh email sâu sắc hơn.
- **Báo cáo định kỳ**: Tạo thêm một nhánh chạy theo lịch (Cron node) để tổng hợp số liệu từ Google Sheets gửi báo cáo tóm tắt vào cuối tuần.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ mạnh mẽ giúp các sếp tối ưu hóa thời gian quản lý email, giữ cho hộp thư luôn sạch sẽ và không bỏ lỡ bất kỳ cơ hội kinh doanh quan trọng nào. Hãy áp dụng ngay hôm nay nhé!