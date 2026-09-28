---
title: "🚀 Tự động Giám sát và Tự phục hồi AWS EC2 Instances với n8n và Cảnh báo Đa kênh"
description: "Xây dựng hệ thống DevOps tự động hóa 100%: định kỳ kiểm tra sức khỏe AWS EC2, tự động restart khi lỗi và gửi cảnh báo qua WhatsApp, Email kèm theo ghi log Google Sheets."
slug: "giam-sat-tu-phuc-hoi-aws-ec2-instances-n8n"
tags: [n8n, automation, devops, aws, ec2, monitoring, no-code]
keywords: [n8n workflow, tự động hóa aws ec2, monitor ec2 instances, self-healing aws, cảnh báo ec2 qua whatsapp email]
---

# 🚀 Tự động Giám sát và Tự phục hồi AWS EC2 Instances với n8n và Cảnh báo Đa kênh

Các sếp quản lý hạ tầng cloud chắc hẳn đã không ít lần "đứng ngồi không yên" khi các instance AWS EC2 đột ngột gặp sự cố giữa đêm khuya, dẫn đến sập hệ thống và gián đoạn dịch vụ khách hàng. Việc phải thủ công đăng nhập vào AWS Console, kiểm tra và khởi động lại (restart) tốn rất nhiều thời gian và gây thiệt hại lớn. 

Giải pháp được Oneclick AI Squad thiết kế dưới đây sẽ giúp các sếp giải quyết triệt để vấn đề này. Workflow n8n này hoạt động hoàn toàn tự động, đóng vai trò như một kỹ sư trực vận hành 24/7: tự động kiểm tra trạng thái EC2, tự phục hồi (self-healing) khi phát hiện lỗi và bắn thông tin cảnh báo đa kênh ngay lập tức.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 24/7:** Định kỳ quét hệ thống mỗi 5 phút mà không cần con người can thiệp.
- **Tự phục hồi thông minh (Self-Healing):** Tự động thực hiện lệnh khởi động lại (restart) các instance không khỏe mạnh.
- **Cảnh báo đa kênh tức thì:** Gửi thông tin chi tiết qua Email và tin nhắn WhatsApp ngay khi sự cố xảy ra hoặc khi đã xử lý xong.
- **Lưu trữ lịch sử minh bạch:** Tự động ghi log toàn bộ sự cố và hành động khắc phục vào Google Sheets để tiện kiểm tra, báo cáo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Hạ tầng n8n:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **AWS API / Credentials:** Quyền truy cập AWS (AWS IAM Access Key / Secret Key) để gọi các API lấy danh sách EC2, check status và restart instance.
- **Twilio Account:** Tài khoản Twilio để gửi tin nhắn WhatsApp cảnh báo.
- **SMTP Server:** Tài khoản gửi email (Gmail, SendGrid, Amazon SES...).
- **Google Sheets:** Một file Google Sheet được chuẩn bị sẵn để ghi log cảnh báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng mã JSON của workflow từ nền tảng n8n (Link gốc: [n8n Workflow #10348](https://n8n.io/workflows/10348)) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 11 nodes chính. Các sếp cần cấu hình chính xác các thành phần sau:
- **Schedule Trigger:** Cấu hình thời gian chạy định kỳ (mặc định chạy mỗi 5 phút).
- **Get EC2 Instances & Check Instance Status & Restart Instance (HTTP Request nodes):** Cấu hình phương thức xác thực AWS Signature v4 hoặc gọi AWS API thông qua HTTP Request để lấy danh sách instance Production, kiểm tra trạng thái và gửi lệnh restart.
- **Analyze Health Data (Code node):** Xử lý logic kiểm tra thời gian không khỏe mạnh (fail-safe: chỉ hành động khi instance không ổn định trên 10 phút).
- **Check Health Status (IF node):** Phân nhánh xử lý trường hợp instance bình thường hay cần can thiệp tự phục hồi.
- **Send WhatsApp Alert (HTTP Request / Twilio credentials):** Nhập thông tin tài khoản Twilio và số điện thoại nhận cảnh báo.
- **Send Email Alert (Email Send node / SMTP credentials):** Cấu hình thông tin SMTP và email nhận báo cáo chi tiết.
- **Log to AlertsLog Sheet (Google Sheets node):** Kết nối tài khoản Google API, chọn đúng file Google Sheet và bảng tính (Sheet Name) để lưu log với thao tác `appendOrUpdate`.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Test Workflow**) với một instance giả lập hoặc kiểm tra dữ liệu mẫu từ các node HTTP Request.
- Sau khi chắc chắn hệ thống chạy mượt mà, gạt công tắc **Active** để workflow tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram/Slack:** Thay thế hoặc bổ sung node gửi tin nhắn qua Telegram Bot hoặc Slack Webhook để đội ngũ kỹ thuật dễ dàng theo dõi chung trên kênh chat công ty.
- **Bổ sung bảng tổng hợp hàng ngày:** Tạo thêm một nhánh chạy vào cuối ngày để tổng hợp số lượng sự cố EC2 trong ngày gửi vào email tóm tắt cho quản lý.
- **Phân loại mức độ lỗi (Severity):** Tùy biến Code node để phân chia lỗi cảnh báo thành Cảnh báo nhẹ (Warning) hoặc Khẩn cấp (Critical) tùy theo loại ứng dụng đang chạy trên EC2.

### 📌 Kết luận
Việc tự động hóa giám sát và phục hồi hạ tầng AWS EC2 giúp đội ngũ DevOps tiết kiệm hàng giờ kiểm tra thủ công, đồng thời giảm thiểu tối đa thời gian downtime của hệ thống. Hãy "lên đồ" ngay cho hệ thống của các sếp với n8n để vận hành chuyên nghiệp và thảnh thơi hơn!