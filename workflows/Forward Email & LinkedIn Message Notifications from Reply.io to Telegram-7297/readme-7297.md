---
title: "🚀 Tự động chuyển tiếp thông báo Email & LinkedIn từ Reply.io sang Telegram bằng n8n"
description: "Hướng dẫn cài đặt workflow n8n giúp nhận thông báo tức thì về chiến dịch outreach trên Reply.io (email, LinkedIn) và gửi thẳng vào Telegram cá nhân hoặc nhóm."
slug: "chuyen-tiep-thong-bao-reply-io-sang-telegram-n8n"
tags: [n8n, automation, no-code, reply-io, telegram, crm]
keywords: [n8n workflow, reply.io webhook, telegram bot notification, tu dong hoa crm, sale automation]
---

# 🚀 Tự động chuyển tiếp thông báo Email & LinkedIn từ Reply.io sang Telegram bằng n8n

Các sếp đang chạy các chiến dịch cold email hay outreach trên LinkedIn qua **Reply.io** chắc chắn hiểu được cảm giác mệt mỏi khi cứ phải liên tục mở tab trình duyệt để check xem khách hàng có reply hay tương tác hay không. Bỏ lỡ một tin nhắn phản hồi đồng nghĩa với việc bỏ lỡ một cơ hội chốt sale béo bở!

Giải pháp ở đây là gì? Tự động hóa 100% quy trình này! Bài viết này sẽ hướng dẫn các sếp cách sử dụng một workflow n8n cực kỳ gọn nhẹ (chỉ với 6 nodes) để hứng toàn bộ webhook sự kiện từ Reply.io, lấy thông tin chi tiết khách hàng và bắn ngay thông báo trực quan về Telegram. Không cần code, hoạt động mượt mà 24/7!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Nhận tin tức thì (Real-time):** Ngay khi khách hàng reply email hoặc tương tác LinkedIn trên Reply.io, thông báo sẽ "ting ting" ngay trên Telegram của các sếp.
- **Tiết kiệm thời gian:** Không cần tốn công canh me dashboard của Reply.io hay mở nhiều tab cùng lúc.
- **Tăng tỷ lệ chuyển đổi:** Phản hồi khách hàng nhanh chóng khi họ vừa có hứng thú, tăng cơ hội chốt deal.
- **Linh hoạt cấu hình:** Dễ dàng chuyển hướng thông báo tới chat cá nhân hoặc đẩy thẳng vào nhóm sale của công ty.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đã được cài đặt (Cloud hoặc Self-hosted có hỗ trợ Webhook public URL).
- Tài khoản **Reply.io** kèm theo **API Key**.
- Một **Telegram Bot** (tạo qua `@BotFather`) và **Chat ID** (cá nhân hoặc group chat).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp tiến hành copy mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc import trực tiếp file JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này được chia làm 2 phần chính: **Thiết lập đăng ký (Utility nodes)** và **Xử lý thông báo (Notifications processing)**. Các sếp làm theo các bước sau:

**Phần 1: Tạo Webhook Subscriptions trên Reply.io**
*   **Create subscription (email)** & **Create subscription (linkedin)** (Nodes loại `httpRequest`):
    *   Thêm Reply.io API Key của các sếp vào phần **Header Auth**.
    *   Điền Webhook URL từ node `Update from Reply.io` vào trường dữ liệu `url` trong body của các node này.
    *   *Mẹo:* Chỉ cần chạy thủ công (Execute node) các node này một lần để Reply.io ghi nhận và bắn webhook về n8n.
*   **Get subscriptions** (Node loại `httpRequest`):
    *   Dùng để kiểm tra lại các danh sách subscription đang hoạt động trên Reply.io xem đã chuẩn chỉnh chưa.

**Phần 2: Xử lý và gửi thông báo**
*   **Update from Reply.io** (Node loại `webhook`):
    *   Đây là điểm đầu mối nhận dữ liệu từ Reply.io gửi tới. Hãy đảm bảo n8n của các sếp đang bật Active để nhận request dạng `POST`.
*   **Get person info from Reply.io** (Node loại `httpRequest`):
    *   Thêm Reply.io API Key vào phần Header Auth để lấy thông tin chi tiết về khách hàng vừa tương tác.
*   **Send notification to Telegram** (Node loại `telegram`):
    *   Thêm credentials của Telegram Bot (Telegram API Token).
    *   Điền **Chat ID** nơi muốn nhận thông báo. 
    *   *Lưu ý quan trọng:* Nếu muốn bot bắn tin nhắn vào Telegram Group, các sếp nhớ add bot vào group đó trước nhé!

#### 3. Kích hoạt ⚡️
- Bấm **Execute Node** ở node Webhook và thực hiện một test action trên Reply.io để kiểm tra luồng dữ liệu chạy có mượt không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow chính thức trực chiến 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống outreach chuyên nghiệp hơn, các sếp có thể mở rộng workflow này bằng cách:
- **Tích hợp Google Sheets:** Lưu lại lịch sử khách hàng phản hồi để đội ngũ marketing/sales dễ dàng chăm sóc lại sau này.
- **Chia nhánh thông minh (If/Else Node):** Phân loại thông báo (nếu là Email thì gửi kênh khác, LinkedIn thì gửi kênh khác hoặc phân về từng sale cụ thể dựa trên tên chiến dịch).
- **Gửi cảnh báo qua Slack/Discord:** Ngoài Telegram, các sếp có thể kết hợp bắn thêm một bản sao thông báo vào kênh chat nội bộ của công ty để team cùng nắm bắt.

### 📌 Kết luận
Chỉ với vài phút cài đặt workflow n8n gọn nhẹ này, quy trình chăm sóc lead từ Reply.io của các sếp sẽ được tự động hóa tối đa, không bỏ lỡ bất kỳ cơ hội kinh doanh nào. Chúc các sếp cài đặt thành công và "chốt đơn" mỏi tay!