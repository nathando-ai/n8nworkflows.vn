---
title: "🚀 Tạo video sản phẩm 360 độ tự động từ ảnh tĩnh với Google Veo 3 và Telegram"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình biến một bức ảnh sản phẩm đơn lẻ thành video 360 độ điện ảnh bằng Google Veo 3 và gửi thẳng qua Telegram bot."
slug: "tao-video-san-pham-360-do-voi-veo-3-va-telegram"
tags: [n8n, automation, google-veo, telegram, ai-video, content-creation]
keywords: [n8n workflow, tao video 360 do, google veo 3, telegram bot ai, vertex ai automation]
---

# 🚀 Tạo video sản phẩm 360 độ tự động từ ảnh tĩnh với Google Veo 3 và Telegram

Các sếp đang kinh doanh thương mại điện tử, thời trang hay agency làm nội dung có thấy mệt mỏi khi cứ phải thuê dựng hình 3D hoặc dùng phần mềm phức tạp chỉ để tạo một video xoay 360 độ cho sản phẩm không? Việc này tốn rất nhiều thời gian và chi phí nhân sự.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n siêu cấp tối ưu này! Chỉ với một tấm ảnh chụp sản phẩm gửi qua Telegram Bot, hệ thống sẽ tự động xác thực Google Cloud, gọi model AI đình đám **Google Veo 3**, render video 360 độ điện ảnh và trả kết quả ngược lại cho khách hàng hoặc đội ngũ kinh doanh chỉ sau vài phút. 100% tự động, không cần code tay!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Biến ảnh 2D thành video 360 độ cinematic chỉ bằng một tin nhắn Telegram.
- **Tiết kiệm chi phí khủng:** Không cần thuê Studio dựng hình 3D hay tool render đắt đỏ.
- **Trải nghiệm mượt mà:** Hệ thống tự động kiểm tra định dạng ảnh, xử lý Auth qua JWT an toàn và cơ chế Polling thông minh báo tiến độ liên tục.
- **Vận hành không gián đoạn:** Tích hợp sẵn cơ chế xử lý lỗi timeout và thông báo trực quan qua Telegram.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** (Self-hosted hoặc Cloud).
- **Telegram Bot Token:** Tạo qua `@BotFather`.
- **Google Cloud Project:** Đã bật **Vertex AI API** và được cấp quyền truy cập preview Veo 3.
- **Google Sheets:** Chứa thông tin Service Account Key của Google Cloud (`client_email`, `private_key`, `project_id`, `scope`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp tiến hành copy toàn bộ mã JSON của workflow này, sau đó mở n8n Editor, chọn **Add workflow** -> **Import from JSON** và dán vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy trơn tru, các sếp chú ý cấu hình kỹ các node sau:

- **Telegram Trigger** & Các node Telegram (`Send Timeout Error`, `Download Image`, `Send Validation Error`, `Send Processing Message`, `Send Conversion Error`, `Send Video to User`): 
  - Kết nối với **Telegram API Credentials** của bot mà các sếp đã tạo.
- **1. Get Service Account Details** (Google Sheets Node):
  - Kết nối tài khoản Google Sheets.
  - Điền chính xác **Sheet ID** chứa thông tin Service Account Google Cloud của các sếp (các cột bắt buộc: `client_email`, `private_key`, `project_id`, `scope`).
- **3. Get Access Token** & **6. Call Vertex AI Veo 3** (HTTP Request Nodes):
  - Kiểm tra lại Endpoint URL của Vertex AI phù hợp với Region project GCP của các sếp.
  - Đảm bảo prompt tạo chuyển động góc quay 360 độ (orbit camera prompt) trong node chuẩn bị payload đã đúng ý đồ.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử gửi một bức ảnh sản phẩm có độ phân giải từ 480px trở lên vào Bot Telegram của các sếp để test.
- Nếu mọi thứ xanh mướt, hãy bật nút **Active** để đưa vào vận hành thực tế 24/7!

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ dữ liệu khách hàng:** Thêm một node Google Sheets hoặc Airtable sau bước gửi video để lưu lại thông tin user Telegram và lịch sử tạo video nhằm quản lý chiến dịch marketing.
- **Tích hợp thông báo nội bộ:** Gắn thêm node Telegram/Slack để bắn thông báo về channel nội bộ của team khi có khách hàng vừa tạo thành công một video sản phẩm mới.
- **Tối ưu thời gian chờ:** Tinh chỉnh thời gian ở node `Wait 2 Minutes` và giới hạn số lần lặp polling ở node `Check Timeout` tùy thuộc vào tốc độ render thực tế của model Veo trên GCP.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ lợi hại cho các team sáng tạo nội dung và thương mại điện tử muốn ứng dụng AI đa phương thức (Multimodal AI) vào quy trình kinh doanh thực tế. Hãy triển khai ngay hôm nay để tối ưu hóa hiệu suất làm việc và mang lại trải nghiệm wow cho khách hàng của các sếp nhé!