---
title: "🚀 Tự động sáng tác Thơ Haiku buổi sáng với OpenRouter AI, Google Docs và Gmail"
description: "Hướng dẫn thiết lập workflow n8n tự động tạo thơ haiku bằng AI mỗi sáng, lưu vào Google Docs và gửi email qua Gmail hoàn toàn miễn phí và tự động."
slug: "tu-dong-sang-tac-tho-haiku-buoi-sang-n8n-openrouter-ai"
tags: [n8n, automation, no-code, openrouter, google-docs, gmail, ai-agent]
keywords: [n8n workflow, tự động hóa n8n, tạo thơ AI, OpenRouter AI, Google Docs automation, Gmail automation]
---

# 🚀 Tự động sáng tác Thơ Haiku mỗi sáng với AI, Google Docs và Gmail

Các sếp có bao giờ muốn bắt đầu ngày mới bằng một làn gió thơ ca tươi mát, nhưng lại quá bận rộn để tự sáng tác? Việc ngồi nghĩ ra những câu thơ chuẩn nhịp 5-7-5 mỗi ngày quả là tốn thời gian. 

Đừng lo! Bài viết này sẽ hướng dẫn các sếp cách dựng một **n8n workflow** tự động hóa 100%: Đúng 7 giờ sáng, AI sẽ tự động "xuất khẩu thành thơ", lưu trữ gọn gàng vào Google Docs và gửi thẳng vào hòm thư Gmail của các sếp. Không cần viết một dòng code phức tạp nào cả!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Khởi đầu ngày mới đầy cảm hứng:** Nhận ngay một bài thơ Haiku độc bản được AI sáng tác riêng cho các sếp vào 7:00 AM mỗi ngày.
- **Lưu trữ tự động:** Tự động tạo file và cập nhật nội dung thơ vào Google Docs, giúp xây dựng "nhật ký thơ ca" theo thời gian.
- **Gửi email chuyên nghiệp:** Thơ được gửi trực tiếp qua Gmail với lời chào buổi sáng ấm áp.
- **Vận hành 24/7:** Chạy hoàn toàn tự động trên n8n, tiết kiệm thời gian và mang lại niềm vui tinh thần mỗi ngày.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu "lên đồ", các sếp cần chuẩn bị sẵn:
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **OpenRouter API Key:** Tài khoản OpenRouter để sử dụng các mô hình AI mạnh mẽ.
- **Google Account:** Để kết nối Google Docs.
- **Gmail Account:** Để gửi email tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này hoặc sử dụng tính năng copy/paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình các node cốt lõi sau:
- **Schedule Trigger:** Mặc định đang cài đặt chạy vào lúc `07:00 AM` mỗi ngày. Các sếp có thể đổi giờ nếu muốn nhận thơ vào khung giờ khác.
- **AI Agent & OpenRouter Chat Model:** Kết nối tài khoản thông qua `OpenRouter API Key`. Tại đây, AI sẽ chịu trách nhiệm sáng tạo các từ khóa theo mùa, danh từ, động từ để ghép thành cấu trúc 5-7-5.
- **Code in JavaScript & Edit Fields:** Các node này nhận dữ liệu từ AI, xử lý định dạng chuẩn nhịp điệu thơ Haiku và thiết lập tiêu đề, thân bài.
- **Create a document & Update a document (Google Docs):** Kết nối tài khoản Google Docs (`googleDocsOAuth2Api`). Các sếp có thể tùy chỉnh Thư mục (Folder ID) lưu trữ file thơ trong Google Drive của mình.
- **Send a message (Gmail):** Kết nối tài khoản Gmail (`gmailOAuth2`) và **nhớ cập nhật địa chỉ email nhận** ở ô người nhận (Recipient) để hệ thống gửi thơ đúng địa chỉ.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để test thử nghiệm dữ liệu mẫu xem thơ có được tạo và email có được bắn đi suôn sẻ không.
- Nếu mọi thứ xanh mướt (success), các sếp chỉ cần gạt công tắc sang **Active** để hệ thống tự động chạy ngầm mỗi ngày!

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ gửi qua Gmail, các sếp có thể nối thêm node Telegram hoặc Slack để bot bắn thơ trực tiếp lên nhóm chat công ty vào mỗi sáng thứ Hai đầu tuần.
- **Lưu vào Notion:** Kết hợp thêm node Notion để tạo một cơ sở dữ liệu (Database) lưu trữ thơ thay vì dùng Google Docs.
- **Đa dạng hóa chủ đề:** Tùy chỉnh Prompt trong AI Agent để thay đổi phong cách thơ (từ lãng mạn, triết lý đến hài hước, động lực làm việc).

### 📌 Kết luận
Một workflow nhỏ nhưng mang lại trải nghiệm tuyệt vời và nụ cười sảng khoái mỗi sáng cho ngày làm việc năng suất. Hãy cài đặt ngay trên hệ thống n8n của các sếp và tận hưởng thành quả nhé! Chúc các sếp thao tác thành công!