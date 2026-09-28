---
title: "🚀 Tự động xác thực email liên hệ HubSpot với Hunter.io trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động quét danh bạ HubSpot, kiểm tra độ hợp lệ của email bằng Hunter.io và cập nhật kết quả sạch sẽ, giúp tối ưu chiến dịch sales."
slug: "tu-dong-xac-thuc-email-hubspot-hunter-io"
tags: [n8n, automation, no-code, sales, hubspot, hunter-io, email-validation]
keywords: [n8n workflow, xác thực email, hubspot automation, hunter.io n8n, tự động hóa sales]
---

# 🚀 Tự động xác thực email liên hệ HubSpot với Hunter.io

Các sếp làm sales hay marketing chắc chắn đã từng đau đầu vì tỷ lệ email bounce (thư trả về) quá cao, làm hỏng danh tiếng tên miền gửi mail và lãng phí thời gian của đội ngũ. Việc kiểm tra thủ công từng email trên HubSpot là bất khả thi với danh sách hàng nghìn khách hàng.

Giải pháp ở đây là gì? Workflow n8n này sẽ tự động hóa 100% quy trình: lấy danh bạ từ **HubSpot**, chuyển sang **Hunter.io** để kiểm tra tính hợp lệ của email, cập nhật ngược lại kết quả vào CRM và gửi thông báo, giúp các sếp sở hữu một data sạch bong kin kít mà không tốn một giọt mồ hôi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Lọc sạch email rác:** Loại bỏ ngay lập tức các email ảo, email chết hoặc domain không tồn tại trước khi chạy chiến dịch outreach.
- **Tự động đồng bộ 2 kết quả:** Trạng thái xác thực của Hunter.io được ghi nhận trực tiếp vào các trường dữ liệu tùy chỉnh (custom fields) trên HubSpot.
- **Tránh vượt ngưỡng Rate Limit:** Tích hợp node chờ thông minh giúp quy trình chạy mượt mà, không bị chặn API.
- **Hoạt động liên tục:** Giúp đội ngũ sales tập trung chốt deal thay vì ngồi check data thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **HubSpot** kèm quyền truy cập API/App Token.
- Tài khoản **Hunter.io** kèm API Key để sử dụng tính năng Email Verifier.
- Tài khoản **SMTP** (hoặc dịch vụ gửi mail tương đương) nếu muốn nhận email thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow (hoặc tải file từ nguồn gốc) và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 8 nodes chính được cấu hình mạch lạc. Các sếp cần chú ý cấu hình các phần sau:

- **Node HubSpot (Search):** Cần kết nối tài khoản thông qua `hubspotAppToken`. Cấu hình điều kiện tìm kiếm các contact cần kiểm tra email.
- **Node Loop Over Items (Split In Batches):** Giúp chia nhỏ danh sách contact thành từng batch nhỏ để xử lý tuần tự, tránh quá tải hệ thống.
- **Node Hunter (Email Verifier):** Sử dụng `hunterApi` để thực hiện gọi API kiểm tra độ tin cậy của địa chỉ email.
- **Node Wait:** Giữ nguyên độ trễ khoảng 1 giây giữa các lần gọi API để tránh chạm trán giới hạn rate limit của Hunter.io.
- **Node Add Hunter Details (Contact) (HTTP Request):** Dùng để đẩy thông tin kết quả check từ Hunter ngược trở lại HubSpot. *(Lưu ý: Các sếp nhớ tạo các Custom Fields tương ứng trên HubSpot trước khi chạy, ví dụ: `hunter_status`, `hunter_score`...)*
- **Node Send Email:** Cấu hình thông tin SMTP để nhận báo cáo hoặc thông báo khi workflow hoàn tất.

#### 3. Kích hoạt ⚡️
- Nhấn nút **‘Test workflow’** trên node `When clicking ‘Test workflow’` để chạy thử với một vài dữ liệu mẫu.
- Kiểm tra kết quả trên HubSpot và email cá nhân.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thay vì chỉ gửi email thông báo, các sếp có thể gắn thêm node Telegram/Slack để bắn tin nhắn báo cáo ngay lập tức khi hoàn tất việc check hàng nghìn contact.
- **Lưu Log vào Google Sheets:** Thêm một node Google Sheets để lưu lại lịch sử mỗi lần check email nhằm phục vụ việc kiểm toán (audit) về sau.
- **Chạy định kỳ (Cron):** Thay thế node `Manual Trigger` bằng `Schedule Trigger` để tự động quét danh bạ HubSpot mỗi tuần/mỗi tháng một lần.

### 📌 Kết luận
Một data sạch là nền tảng của mọi chiến dịch Sales thành công. Với workflow n8n kết hợp HubSpot và Hunter.io này, các sếp hoàn toàn có thể tự động hóa toàn bộ khâu kiểm tra chất lượng dữ liệu chỉ trong vài nốt nhạc. Chúc các sếp cài đặt thành công và "chốt đơn" mỏi tay!