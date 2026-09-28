---
title: "🚀 Tự động gửi Email trực tiếp từ Obsidian tích hợp Gmail qua n8n"
description: "Hướng dẫn chi tiết cách cấu hình workflow n8n để gửi ghi chú Obsidian kèm file đính kèm qua Gmail chỉ với vài cú click, tự động xử lý YAML metadata."
slug: "gui-email-tu-obsidian-qua-gmail-n8n"
tags: [n8n, automation, obsidian, gmail, productivity, webhook]
keywords: [n8n workflow, obsidian to email, gửi email từ obsidian, gmail automation n8n, obsidian post webhook]
---

# 🚀 Tự động gửi Email trực tiếp từ Obsidian tích hợp Gmail qua n8n

Các sếp có đang sử dụng Obsidian để ghi chép và thấy phiền phức khi mỗi lần muốn gửi ghi chú (kèm hình ảnh hoặc tài liệu) cho khách hàng hoặc đồng nghiệp lại phải copy-paste thủ công sang Gmail không? Việc này vừa tốn thời gian, lại dễ làm gián đoạn mạch tư duy.

Giải pháp ở đây là tự động hóa 100%! Workflow n8n này sẽ giúp các sếp bắn thẳng ghi chú từ Obsidian qua Gmail chỉ bằng một câu lệnh, thậm chí tự động nhận diện metadata từ YAML Frontmatter và đính kèm file mượt mà.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tốc độ thần tốc**: Gửi email trực tiếp từ ứng dụng ghi chú yêu thích mà không cần mở trình duyệt hay ứng dụng mail.
- **Cấu hình thông minh**: Tự động bóc tách người nhận (To, CC, BCC), tiêu đề, tên người gửi thông qua YAML Frontmatter ngay trong note.
- **Đính kèm tự động**: Xử lý mượt mà các file/hình ảnh đính kèm trong note thông qua mã hóa Base64 và chuyển đổi nhị phân.
- **Phản hồi tức thì**: Workflow tự động gửi thông báo trạng thái thành công và ghi nhận lịch sử ngay dưới chân note trong Obsidian.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n instance** (Self-hosted hoặc Cloud).
- **Tài khoản Gmail** đã được kết nối thông qua Credentials (OAuth2) trong n8n.
- **Obsidian** cài sẵn plugin **Post Webhook**.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tạo một workflow mới trong n8n của các sếp, sau đó copy toàn bộ JSON của workflow *Send Emails via Gmail from Obsidian* và paste trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần chú ý cấu hình kỹ các node sau để hệ thống chạy trơn tru:

- **Webhook**: Lấy URL endpoint được cung cấp tại node này và dán vào phần cài đặt của plugin *Obsidian Post Webhook* trên Obsidian.
- **Email With Attachments & Email Without Attachments**: Kết nối với tài khoản Gmail của các sếp (chọn `gmailOAuth2` credentials). Node này sẽ tự động phân nhánh tùy thuộc vào việc note của các sếp có file đính kèm hay không (`Check if attachments exist`).
- **Convert Attachment to File**: Đảm bảo thông số `operation` được cấu hình là `toBinary` để hệ thống hiểu và đóng gói file đính kèm chính xác.
- **Respond to Obsidian & Test Successfull**: Các node phản hồi giúp gửi kết quả ngược lại cho Obsidian để append (nối) trạng thái vào cuối note.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** trong n8n để chuyển sang chế độ chờ tín hiệu (Listening).
- Mở một note bất kỳ trên Obsidian, sử dụng tổ hợp phím `Ctrl/Cmd + P`, tìm lệnh gửi Webhook và test thử.
- Sau khi test thành công, gạt nút **Active** trên góc phải màn hình để bật workflow chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack**: Bổ sung thêm một node thông báo qua Telegram hoặc Slack để đội ngũ quản lý biết khi nào có một báo cáo quan trọng vừa được gửi đi từ Obsidian.
- **Lưu lịch sử gửi**: Kết hợp thêm node Google Sheets hoặc Airtable để lưu lại log danh sách các email đã được gửi tự động từ Obsidian.
- **Hẹn giờ gửi**: Thay vì kích hoạt ngay lập tức qua webhook, các sếp có thể kết hợp với các công cụ quản lý Task để lên lịch gửi báo cáo định kỳ.

### 📌 Kết luận
Việc tự động hóa quy trình gửi email từ Obsidian không chỉ giúp tiết kiệm hàng giờ thao tác thủ công mỗi tuần mà còn xây dựng một hệ sinh thái làm việc cực kỳ chuyên nghiệp và liền mạch. Cài đặt ngay hôm nay để tối ưu hóa năng suất cá nhân và doanh nghiệp các sếp nhé!