---
title: "🚨 Workflow n8n Cảnh báo Khẩn cấp cho Trường học: Tự động Thông báo Phụ huynh & Nhân viên Tức thì"
description: "Xây dựng hệ thống cảnh báo khẩn cấp tự động 100% cho trường học với n8n, kết hợp Webhook, Email và Slack để xử lý sự cố nhanh chóng."
slug: "workflow-canh-bao-khan-cap-truong-hoc-n8n"
tags: [n8n, automation, no-code, emergency-alert, education, notification]
keywords: [n8n workflow, cảnh báo khẩn cấp trường học, tự động hóa n8n, webhook slack email, thông báo phụ huynh tự động]
---

# 🚨 Workflow n8n Cảnh báo Khẩn cấp cho Trường học: Tự động Thông báo Phụ huynh & Nhân viên Tức thì

Trong môi trường giáo dục, mỗi giây trong tình huống khẩn cấp đều cực kỳ quý giá. Việc gọi điện thủ công cho từng phụ huynh hay nhắn tin riêng cho từng giáo viên không chỉ tốn thời gian mà còn dễ dẫn đến sai sót, chậm trễ. 

Bài viết này sẽ giới thiệu một giải pháp tự động hóa toàn diện từ **Oneclick AI Squad**: **Workflow Cảnh báo Khẩn cấp cho Trường học**. Hệ thống này giúp kích hoạt và phát đi thông báo khẩn cấp qua nhiều kênh cùng lúc (Email và Slack) chỉ bằng một tín hiệu Webhook duy nhất, đảm bảo không bỏ sót bất kỳ ai.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tốc độ chớp nhoáng:** Gửi hàng loạt thông báo đến phụ huynh và giáo viên chỉ trong vài giây ngay khi có sự cố.
- **Đa kênh đồng bộ:** Tự động hóa việc gửi Email đến phụ huynh/nhân sự và đẩy tin nhắn cảnh báo lên kênh Slack nội bộ để ban điều hành phối hợp xử lý.
- **Bộ lọc thông minh:** Node `Filter Emergency Alerts` giúp phân loại chính xác tình trạng khẩn cấp thật, loại bỏ các tín hiệu nhầm lẫn hoặc thử nghiệm nhờ node `No Action for Inactive`.
- **Vận hành 24/7:** Hoạt động tự động hoàn toàn không cần sự can thiệp thủ công, giảm thiểu tối đa rủi ro hoảng loạn trong các tình huống khủng hoảng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow này "lên đồ" và chạy mượt mà, các sếp cần chuẩn bị sẵn:
1. **Hệ thống n8n:** Đã cài đặt sẵn (Self-hosted trên VPS hoặc n8n Cloud).
2. **Tài khoản SMTP (Email):** Thông tin kết nối SMTP để gửi email tự động (Gmail, SendGrid, Amazon SES,...).
3. **Workspace Slack:** Quyền tích hợp và tạo Bot/App để gửi tin nhắn cảnh báo vào kênh chuyên trách của trường.
4. **Hệ thống nguồn (Source):** Nơi phát ra tín hiệu cảnh báo ban đầu (App của trường, nút bấm phần cứng, hoặc hệ thống IoT tích hợp gọi Webhook).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này hoặc sao chép mã nguồn JSON.
- Trong giao diện n8n Editor, bấm vào menu ở góc trên bên phải, chọn **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import thành công, các sếp cần cấu hình các node cốt lõi sau:

- **Webhook Trigger (`Webhook Trigger`):**
  - Cấu hình phương thức nhận dữ liệu là `POST`.
  - Lấy URL Webhook được cung cấp (`Production URL` hoặc `Test URL`) để tích hợp vào hệ thống nguồn phát tín hiệu khẩn cấp của trường.
- **Bộ lọc khẩn cấp (`Filter Emergency Alerts`):**
  - Thiết lập điều kiện (Conditions) để kiểm tra xem tín hiệu gửi tới có phải là tình trạng khẩn cấp thực sự hay không (ví dụ: `status` bằng `active` hoặc `emergency_level` > 2).
- **Gửi Email cảnh báo (`Send Email Alert`):**
  - Chọn **Credentials** đã kết nối với tài khoản SMTP của trường.
  - Điền tiêu đề, nội dung email cảnh báo và danh sách người nhận (Phụ huynh, Giáo viên, Ban giám hiệu).
- **Gửi Slack cảnh báo (`Send Slack Alert`):**
  - Chọn **Credentials** cho Slack API.
  - Chỉ định kênh (Channel) nội bộ trên Slack sẽ nhận thông báo phối hợp khẩn cấp (ví dụ: `#emergency-response`).
- **Xử lý tín hiệu không khẩn cấp (`No Action for Inactive`):**
  - Node này dùng chuẩn `NoOp` (No Operation), không cần cấu hình gì thêm, dùng để kết thúc luồng khi tín hiệu không đạt điều kiện khẩn cấp.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Node** ở Webhook Trigger và gửi một request mẫu để kiểm tra dữ liệu chạy qua các nhánh.
- Kiểm tra kết quả thực tế trên Email và Slack.
- Gạt công tắc sang **Active** để đưa workflow vào trạng thái vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/SMS:** Mở rộng workflow bằng cách gắn thêm node Telegram hoặc Twilio SMS để gửi tin nhắn văn bản trực tiếp đến điện thoại của giáo viên trực ban.
- **Lưu lịch sử sự cố:** Thêm một node Google Sheets hoặc Notion ở nhánh đầu tiên để ghi lại toàn bộ lịch sử các cảnh báo (thời gian, nội dung, mức độ) phục vụ cho việc kiểm tra và báo cáo sau sự cố.
- **Cá nhân hóa nội dung:** Sử dụng biến từ Webhook để tự động điền tên học sinh, lớp học và địa điểm xảy ra sự cố vào trong nội dung Email và Slack.

### 📌 Kết luận
Workflow Cảnh báo Khẩn cấp cho Trường học là một giải pháp sống còn giúp tối ưu hóa quy trình phản ứng nhanh trong giáo dục. Bằng cách tự động hóa hoàn toàn các thao tác thông báo qua Email và Slack, các sếp có thể yên tâm rằng mọi thông tin quan trọng sẽ được truyền đi chính xác, nhanh chóng và hiệu quả nhất khi có sự cố xảy ra. Hãy áp dụng ngay vào hệ thống của mình nhé!