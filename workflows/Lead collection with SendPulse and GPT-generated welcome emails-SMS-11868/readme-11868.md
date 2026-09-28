---
title: "🚀 Tự động hóa thu thập Lead và gửi Email/SMS chào mừng cá nhân hóa bằng SendPulse và GPT"
description: "Hướng dẫn xây dựng workflow n8n tích hợp SendPulse và OpenAI GPT để tự động thu thập thông tin khách hàng, phân loại danh sách và gửi tin nhắn chào mừng qua Email/SMS."
slug: "tu-dong-hoa-thu-thap-lead-sendpulse-gpt"
tags: [n8n, automation, no-code, sendpulse, openai, lead-nurturing]
keywords: [n8n workflow, sendpulse automation, openai gpt email sms, tu dong hoa lead, chao mung khach hang ai]
---

# 🚀 Tự động hóa thu thập Lead và gửi Email/SMS chào mừng cá nhân hóa bằng SendPulse và GPT

Các sếp có bao giờ cảm thấy quá tải khi vừa phải nhập liệu thông tin khách hàng mới đăng ký từ website, vừa phải ngồi nghĩ và soạn từng nội dung email hay tin nhắn SMS chào mừng sao cho thật chuyên nghiệp và cá nhân hóa chưa? Việc làm thủ công này không chỉ ngốn rất nhiều thời gian mà còn dễ dẫn đến độ trễ, khiến khách hàng "nguội lạnh".

Giải pháp ở đây chính là **workflow n8n tự động hóa 100%**: Ngay khi có khách hàng đăng ký qua form trên website, hệ thống sẽ tự động xác thực token SendPulse, kiểm tra và phân loại danh sách liên lạc (mailing list), sử dụng AI (OpenAI GPT) để soạn thảo nội dung email/SMS chào mừng cực kỳ thu hút, sau đó gửi đi lập tức mà không cần sự can thiệp thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tốc độ phản hồi tức thì:** Khách hàng nhận được email/SMS chào mừng ngay trong tích tắc sau khi đăng ký.
- **Cá nhân hóa thông minh:** Sử dụng OpenAI GPT-4.1-mini để tạo nội dung chào mừng phù hợp riêng cho từng khách hàng, tăng tỷ lệ tương tác.
- **Tự động quản lý danh sách:** Hệ thống tự động kiểm tra và đồng bộ thông tin khách hàng vào đúng danh sách email hoặc số điện thoại trên SendPulse.
- **Hoạt động 24/7 không nghỉ:** Loại bỏ hoàn toàn các tác vụ thủ công lặp đi lặp lại, giúp đội ngũ sales & marketing tập trung vào chốt đơn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Tài khoản SendPulse** kèm theo *Client ID* và *Client Secret* để lấy API token.
- **OpenAI API Key** cấu hình cho mô hình chat.
- **Một Data Table trên n8n** dùng để lưu trữ và cache access token của SendPulse.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ JSON của workflow từ nguồn cung cấp và dán trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:
- **Node `Workflow Configuration` (Loại: Set):** Điền các biến cấu hình quan trọng bao gồm SendPulse Client ID, Client Secret, `mailingListWithEmails`, `mailingListWithPhones`, `senderName`, `senderEmail`, `smsSender`, `routeCountryCode`, và `routeType`.
- **Node `Save Token to Storage` & `Get Token from Storage` (Loại: Data Table):** Tạo trước một Data Table tên là `tokens` với 3 cột: `hash` (string), `accessToken` (string), và `tokenExpiry` (string) để quản lý việc cache token SendPulse, tránh gọi API liên tục.
- **Node `OpenAI Chat Model` (Loại: lmChatOpenAi):** Nhập OpenAI API Key và chọn model mong muốn (khuyến nghị `gpt-4.1-mini`).
- **Node `New Customer Registration` (Loại: Webhook):** Cấu hình endpoint webhook với path `customer-registration` và phương thức `POST` để trỏ form trên website về đây.

#### 3. Kích hoạt ⚡️
- Thực hiện một lượt **Test run** bằng cách gửi dữ liệu mẫu qua Webhook để kiểm tra luồng xử lý từ SendPulse đến OpenAI.
- Sau khi test thành công, bật công tắc **Active** để workflow chính thức vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo nội bộ:** Kết nối thêm node Telegram hoặc Slack ở cuối workflow để bắn thông báo về team mỗi khi có một Lead mới đăng ký thành công.
- **Lưu trữ dữ liệu mở rộng:** Bổ sung node Google Sheets hoặc Airtable để lưu trữ toàn bộ lịch sử lead phục vụ cho các chiến dịch remarketing sau này.
- **Xử lý lỗi (Error Handling):** Thêm Error Trigger workflow để nhận cảnh báo ngay lập tức nếu API SendPulse hoặc OpenAI gặp sự cố gián đoạn.

### 📌 Kết luận
Workflow tích hợp SendPulse và OpenAI GPT này chính là chìa khóa giúp doanh nghiệp tự động hóa khâu chăm sóc khách hàng ban đầu một cách chuyên nghiệp và thông minh nhất. Hãy cài đặt ngay hôm nay để tối ưu hóa tỷ lệ chuyển đổi lead cho hệ thống của các sếp!