---
title: "🔄 [Tự động hóa CRM] Đồng bộ liên hệ giữa Mailchimp và Pipedrive - Workflow n8n hoàn chỉnh"
description: "Hướng dẫn chi tiết cách tự động đồng bộ danh sách liên hệ giữa Mailchimp và Pipedrive thông qua workflow n8n. Tiết kiệm thời gian và tránh sai sót khi cập nhật thông tin khách hàng."
slug: "tu-dong-hoa-dong-bo-lien-he-mailchimp-pipedrive-n8n"
tags: [n8n, automation, no-code, crm, marketing]
keywords: [n8n workflow, tự động hóa crm, đồng bộ liên hệ, mailchimp, pipedrive]
---

# 🔄 [Tự động hóa CRM] Đồng bộ liên hệ giữa Mailchimp và Pipedrive - Workflow n8n hoàn chỉnh

[Các sếp đang làm việc với nhiều hệ thống CRM như HubSpot, Salesforce... thường gặp khó khăn khi phải thủ công đồng bộ danh sách liên hệ giữa các nền tảng này. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình đồng bộ liên hệ giữa Mailchimp và Pipedrive thông qua n8n, tiết kiệm thời gian và tránh sai sót khi cập nhật thông tin khách hàng.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động đồng bộ thông tin liên hệ giữa Mailchimp và Pipedrive mà không cần can thiệp thủ công.
- **Chính xác cao**: Tránh sai sót khi cập nhật thông tin khách hàng giữa các nền tảng.
- **Tích hợp liền mạch**: Dữ liệu khách hàng luôn đồng bộ giữa CRM và hệ thống email marketing.
- **Hoạt động liên tục**: Workflow chạy tự động 24/7, không cần giám sát.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Mailchimp với API key và List ID.
- Tài khoản Pipedrive với API key.
- Tài khoản CRM nguồn (HubSpot, Salesforce...) có khả năng gửi webhook.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io](https://n8n.io) và đăng nhập vào tài khoản của bạn.
2. Nhấn vào nút **"Import from URL"** và dán link workflow: [https://n8n.io/workflows/13225](https://n8n.io/workflows/13225).
3. Hoặc tải file JSON về và import thủ công qua **"Import from File"**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Incoming Contact Webhook**:
   - Cấu hình URL webhook trong CRM nguồn trỏ đến endpoint được tạo bởi node này.
   - Ví dụ: `https://your-n8n-instance.com/webhook/crm-contact-sync`.

2. **Fetch Contact Details (Source CRM)**:
   - Thêm credentials cho CRM nguồn (HubSpot, Salesforce...).
   - Cấu hình endpoint API để lấy thông tin chi tiết của liên hệ.

3. **Pipedrive Nodes**:
   - Thêm credentials Pipedrive cho tất cả các node liên quan đến Pipedrive.
   - Kiểm tra và điều chỉnh các trường dữ liệu trong node **"Determine Existence & Prepare Data"** nếu cần.

4. **Mailchimp Nodes**:
   - Thêm API key Mailchimp và cấu hình List ID cho các node liên quan.
   - Kiểm tra và điều chỉnh các trường dữ liệu trong node **"Build Mailchimp Payload"** nếu cần.

#### 3. Kích hoạt ⚡️
1. **Test run dữ liệu mẫu**:
   - Gửi một liên hệ mẫu từ CRM nguồn để kiểm tra toàn bộ quy trình.
   - Kiểm tra kết quả trên Pipedrive và Mailchimp để đảm bảo dữ liệu được đồng bộ chính xác.

2. **Bật Active workflow**:
   - Sau khi kiểm tra thành công, nhấn nút **"Activate"** để workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node gửi thông báo thành công/lỗi qua Slack hoặc Telegram để theo dõi quá trình đồng bộ.
- **Lưu log**: Thêm node lưu log các hoạt động đồng bộ để kiểm tra lại sau này.
- **Gửi báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo tổng hợp các liên hệ đã được đồng bộ mỗi ngày.
- **Mở rộng cho nhiều CRM**: Sử dụng node **"Split Contacts"** để xử lý dữ liệu từ nhiều CRM nguồn khác nhau.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình đồng bộ liên hệ giữa Mailchimp và Pipedrive, tiết kiệm thời gian và tránh sai sót khi cập nhật thông tin khách hàng. Hãy áp dụng ngay để nâng cao hiệu quả làm việc của đội ngũ marketing và bán hàng!