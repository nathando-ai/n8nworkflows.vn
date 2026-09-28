---
title: "🚀 Tự động hóa CRM Podium với Claude AI, Google Sheets và Gmail - Workflow n8n hoàn chỉnh"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình CRM Podium bằng workflow n8n kết hợp AI, Google Sheets và Gmail. Tiết kiệm thời gian, tối ưu quy trình bán hàng và theo dõi khách hàng một cách hiệu quả."
slug: "tu-dong-hoa-crm-podium-voi-claude-ai-google-sheets-gmail"
tags: [n8n, automation, no-code, crm, ai, google-sheets, gmail]
keywords: [n8n workflow, tự động hóa crm, podium, ai summarization, google sheets, gmail]
---

# 🚀 Tự động hóa CRM Podium với Claude AI, Google Sheets và Gmail - Workflow n8n hoàn chỉnh

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp đang gặp khó khăn khi quản lý quy trình bán hàng trên Podium CRM một cách thủ công? Bạn muốn tự động hóa việc phân loại tin nhắn, theo dõi giai đoạn khách hàng và gửi email nhắc nhở một cách hiệu quả? Workflow n8n này sẽ giúp các sếp giải quyết tất cả những vấn đề này một cách hoàn toàn tự động, không cần viết code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động phân loại tin nhắn**: AI Claude sẽ phân loại tự động các tin nhắn từ Podium vào các giai đoạn phù hợp trong quy trình bán hàng.
- **Cập nhật tự động giai đoạn khách hàng**: Workflow sẽ tự động cập nhật giai đoạn khách hàng trong Podium dựa trên nội dung tin nhắn.
- **Gửi email nhắc nhở thông minh**: Hệ thống sẽ tự động gửi email nhắc nhở cho các khách hàng có đơn hàng đang chờ xử lý.
- **Báo cáo hàng ngày tự động**: Mỗi sáng, các sếp sẽ nhận được báo cáo tổng hợp về hoạt động bán hàng trong ngày.
- **Bảng điều khiển trực quan**: Dashboard trực quan hiển thị toàn bộ quy trình bán hàng một cách dễ dàng theo dõi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Podium CRM với quyền truy cập API
- Tài khoản Google Cloud với quyền truy cập Google Sheets và Gmail
- API key từ Anthropic để sử dụng Claude AI
- Tài khoản n8n đã được cài đặt và cấu hình
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào trang [n8n.io/workflows/15784](https://n8n.io/workflows/15784)
2. Nhấp vào nút "Download" để tải về file JSON của workflow
3. Trong giao diện n8n, nhấp vào "Import from File" và chọn file JSON vừa tải về
4. Hoặc copy toàn bộ nội dung JSON và dán vào ô "Import from JSON" trong n8n

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Podium Webhook** (Node đầu tiên):
   - Đăng ký webhook trong Podium Developer Console trỏ đến URL của node này
   - Subscribe đến sự kiện `conversation.message.created`

2. **Claude Classify** (Node HTTP Request):
   - Tạo credential cho Anthropic API trong n8n
   - Đảm bảo có đủ credit trong tài khoản Anthropic

3. **Google Sheets** (Các node Google Sheets):
   - Tạo credential Google Sheets OAuth2 trong n8n
   - Thay thế `YOUR_GOOGLE_SHEET_ID` bằng ID của Google Sheet bạn sử dụng
   - Đảm bảo tài khoản có quyền truy cập vào Google Sheet

4. **Podium API** (Các node HTTP Request liên quan đến Podium):
   - Tạo credential OAuth2 cho Podium trong n8n
   - Thay thế các tham số `YOUR_PODIUM_LOCATION_UID`, `YOUR_FUNNEL_STAGE_ATTRIBUTE_UID`, `YOUR_OPP_VALUE_ATTRIBUTE_UID` trong các node Code
   - Thay thế tất cả các `YOUR_*_STAGE_UID` bằng các giá trị UID thực tế trong hệ thống Podium của bạn

5. **Gmail** (Node Email Daily Report):
   - Kết nối credential Gmail OAuth2
   - Thiết lập địa chỉ email nhận báo cáo trong node Gmail

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node quan trọng, nhấp vào nút "Activate" để kích hoạt workflow
2. Thử chạy workflow với dữ liệu mẫu để kiểm tra hoạt động
3. Kiểm tra các node Google Sheets để đảm bảo dữ liệu được ghi đúng
4. Kiểm tra email để đảm bảo báo cáo hàng ngày được gửi đúng

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh quy trình bán hàng**: Các sếp có thể điều chỉnh các giai đoạn trong quy trình bán hàng bằng cách sửa đổi các giá trị trong node Code
2. **Thêm kênh thông báo**: Kết nối với Slack hoặc Telegram để nhận thông báo tức thời về các thay đổi quan trọng
3. **Tích hợp với các công cụ khác**: Kết nối với các công cụ khác như Zapier hoặc Make để mở rộng chức năng của workflow
4. **Tối ưu hóa báo cáo**: Các sếp có thể tùy chỉnh nội dung báo cáo hàng ngày để phù hợp với nhu cầu của doanh nghiệp

### 📌 Kết luận
Workflow n8n này cung cấp giải pháp toàn diện để tự động hóa quy trình CRM Podium, từ phân loại tin nhắn tự động đến gửi email nhắc nhở và báo cáo hàng ngày. Với việc tích hợp AI Claude và Google Sheets, các sếp có thể tối ưu hóa quy trình bán hàng một cách hiệu quả và tiết kiệm thời gian đáng kể. Hãy áp dụng ngay workflow này để nâng cao hiệu suất làm việc của đội ngũ bán hàng!