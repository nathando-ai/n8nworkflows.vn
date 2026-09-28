---
title: "🏡 Tự động hóa xử lý yêu cầu bất động sản: Nhận tin nhắn SMS cá nhân hóa + AI đánh giá khách hàng tiềm năng"
description: "Workflow n8n tự động hóa quy trình xử lý yêu cầu bất động sản từ Zillow, Realtor.com, Facebook Lead Ads... bằng cách gửi SMS cá nhân hóa và đưa khách hàng vào chuỗi đánh giá AI"
slug: "tu-dong-hoa-xu-ly-yeu-cau-bat-dong-san"
tags: [n8n, automation, no-code, bat-dong-san, sms-marketing, ai-chatbot]
keywords: [n8n workflow, tự động hóa bất động sản, sms cá nhân hóa, ai đánh giá khách hàng, lead nurturing]
---

# 🏡 Tự động hóa xử lý yêu cầu bất động sản: Nhận tin nhắn SMS cá nhân hóa + AI đánh giá khách hàng tiềm năng

[Các sếp bất động sản đang gặp khó khăn khi phải xử lý hàng trăm yêu cầu từ các nền tảng như Zillow, Realtor.com, Facebook Lead Ads... một cách thủ công. Mỗi yêu cầu cần được xử lý riêng biệt, gửi SMS cá nhân hóa và đưa vào chuỗi đánh giá khách hàng tiềm năng. Workflow này giúp tự động hóa toàn bộ quy trình này một cách hoàn toàn không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động xử lý hàng trăm yêu cầu mỗi ngày mà không cần can thiệp thủ công.
- **Cá nhân hóa cao**: Gửi SMS chứa thông tin chính xác về bất động sản mà khách hàng quan tâm.
- **Đánh giá khách hàng hiệu quả**: Sử dụng AI để đánh giá khách hàng tiềm năng một cách tự động.
- **Hoạt động liên tục**: Workflow chạy 24/7 mà không cần giám sát.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Aloware với API token.
- Số điện thoại được cấu hình trong Aloware để gửi SMS.
- Chuỗi đánh giá khách hàng tiềm năng đã được tạo trong Aloware.
- Nền tảng nguồn lead (Zillow, Realtor.com, Facebook Lead Ads...) có thể gửi dữ liệu đến webhook.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấn vào nút "Import from URL" và dán link sau: `https://n8n.io/workflows/15020`
3. Hoặc bạn có thể tải file JSON từ [đây](https://n8n.io/workflows/15020) và import thủ công.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Property Inquiry Received (Webhook)**:
  - Đảm bảo webhook URL được cấu hình đúng trong nguồn lead của bạn.
  - Kiểm tra lại phương thức HTTP (POST) và đường dẫn (`property-inquiry`).

- **Normalize Inquiry Data (Set)**:
  - Cấu hình các biến để chuẩn hóa dữ liệu đầu vào (tên khách hàng, địa chỉ bất động sản, giá, MLS#...).

- **Aloware: Create Contact with Property Details (HTTP Request)**:
  - Cấu hình credentials với `ALOWARE_API_TOKEN`.
  - Điền URL endpoint của Aloware để tạo liên hệ mới.
  - Kiểm tra các tham số đầu vào (tên khách hàng, địa chỉ bất động sản, giá, MLS#...).

- **Aloware: Send Property Inquiry SMS (HTTP Request)**:
  - Cấu hình credentials với `ALOWARE_API_TOKEN` và `ALOWARE_LINE_PHONE`.
  - Điền URL endpoint của Aloware để gửi SMS.
  - Kiểm tra nội dung SMS và các biến động (tên khách hàng, địa chỉ bất động sản, giá...).

- **Aloware: Enroll in AI Buyer Qualification Sequence (HTTP Request)**:
  - Cấu hình credentials với `ALOWARE_API_TOKEN` và `ALOWARE_SEQUENCE_ID`.
  - Điền URL endpoint của Aloware để đăng ký chuỗi đánh giá khách hàng tiềm năng.
  - Kiểm tra các tham số đầu vào (ID khách hàng, ID chuỗi đánh giá...).

#### 3. Kích hoạt ⚡️
- **Test run dữ liệu mẫu**: Gửi một yêu cầu bất động sản mẫu để kiểm tra toàn bộ workflow.
- **Bật Active workflow**: Sau khi kiểm tra thành công, bật workflow để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node để thông báo khi có yêu cầu mới hoặc khi khách hàng được đánh giá.
- **Lưu log**: Thêm node để lưu log các yêu cầu và kết quả xử lý.
- **Gửi báo cáo định kỳ**: Tạo báo cáo hàng ngày/hàng tuần về số lượng yêu cầu, số lượng khách hàng được đánh giá, tỷ lệ chuyển đổi...
- **Tích hợp với CRM khác**: Kết nối với các hệ thống CRM khác như HubSpot, Salesforce để lưu trữ thông tin khách hàng.

### 📌 Kết luận
Workflow này giúp các sếp bất động sản tự động hóa toàn bộ quy trình xử lý yêu cầu bất động sản, từ nhận yêu cầu đến gửi SMS cá nhân hóa và đưa khách hàng vào chuỗi đánh giá AI. Với việc tự động hóa này, các sếp có thể tập trung vào các hoạt động quan trọng hơn và tăng hiệu quả kinh doanh. Hãy áp dụng ngay để thấy kết quả ngay lập tức!