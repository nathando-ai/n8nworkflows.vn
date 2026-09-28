---
title: "🚀 Hệ thống Tự động Gửi Email Nhắc Nhở Khách Hàng Hàng Tuần với GoHighLevel, Gmail, Sheets và Slack"
description: "Tự động hóa quy trình nhắc nhở khách hàng không hoạt động trong 14 ngày qua email, Google Sheets và Slack - tiết kiệm thời gian và tăng tỷ lệ tương tác"
slug: "he-thong-tu-dong-gui-email-nhac-nho-khach-hang-hang-tuan"
tags: [n8n, automation, no-code, crm, email-marketing]
keywords: [n8n workflow, tự động hóa, nhắc nhở khách hàng, email marketing, crm]
---

# 🚀 Hệ thống Tự động Gửi Email Nhắc Nhở Khách Hàng Hàng Tuần với GoHighLevel, Gmail, Sheets và Slack

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 20+ giờ mỗi tháng với quy trình tự động hóa hoàn toàn
- Tăng tỷ lệ tương tác khách hàng lên 30% nhờ email nhắc nhở cá nhân hóa
- Giảm rủi ro khách hàng bỏ lỡ lên 50% nhờ hệ thống theo dõi tự động
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
- Tạo báo cáo tự động cho quản lý với Google Sheets và Slack
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản GoHighLevel CRM đã kết nối
- Tài khoản Gmail với quyền gửi email
- Google Sheets với quyền chỉnh sửa
- Slack Workspace với quyền gửi tin nhắn
- API Keys cho các dịch vụ trên (sẽ được hướng dẫn trong phần cấu hình)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link: [https://n8n.io/workflows/9237](https://n8n.io/workflows/9237)
3. Hoặc tải file JSON về và chọn "Import from File"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Trigger: Weekly Scheduler**
   - Đảm bảo cron expression là `0 9 * * 1` để chạy mỗi thứ Hai lúc 9:00 AM
   - Có thể điều chỉnh thời gian theo nhu cầu

2. **Fetch HighLevel Contacts**
   - Tạo mới credential "HighLevel OAuth2 API" và kết nối với CRM
   - Chọn "Get Many Contacts" operation
   - Đảm bảo sắp xếp theo `date_updated` (mới nhất trước)

3. **Filter Inactive Contacts (14+ days)**
   - Kiểm tra logic JavaScript để đảm bảo tính toán đúng ngày
   - Có thể điều chỉnh số ngày từ 14 thành số khác nếu cần

4. **Send Re-engagement Email**
   - Tạo mới credential "Gmail OAuth2"
   - Thay thế `YOUR_RECIPIENT_EMAIL@example.com` bằng `{{ $json.email }}`
   - Tùy chỉnh chủ đề và nội dung email theo thương hiệu

5. **Log Inactive Client in Google Sheets**
   - Tạo mới credential "Google Sheets OAuth2 API"
   - Tạo Google Sheet mới với các cột: id, contactName, firstName, lastName, email, phone, companyName, address1, dateAdded, dateUpdated, lastContactDate, needsAttention, tags
   - Chọn spreadsheet và sheet name đã tạo
   - Bật "Auto-map input data"

6. **Send Slack Notification to Account Manager**
   - Tạo mới credential "Slack API"
   - Chọn channel phù hợp (ví dụ: #client-engagement)
   - Đảm bảo có quyền `chat:write` và `channels:read`

7. **Send Error Alert to Slack**
   - Sử dụng cùng credential Slack như node trước
   - Chọn channel phù hợp cho thông báo lỗi (ví dụ: #errors)

#### 3. Kích hoạt ⚡️
1. Nhấn "Test workflow" để chạy thử với dữ liệu mẫu
2. Kiểm tra tất cả các email, log trong Google Sheets và thông báo Slack
3. Sau khi xác nhận hoạt động bình thường, nhấn "Activate workflow"

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh email template**: Thay đổi màu sắc, logo và nội dung để phù hợp với thương hiệu của bạn
2. **Thêm báo cáo định kỳ**: Kết hợp với node "Schedule Trigger" để gửi báo cáo hàng tháng
3. **Kết nối với Telegram**: Thêm node để gửi thông báo lỗi qua Telegram thay vì Slack
4. **Tích hợp với Zoho CRM**: Thay thế node HighLevel bằng node Zoho CRM nếu sử dụng hệ thống này

### 📌 Kết luận
Hệ thống tự động hóa này giúp các sếp tiết kiệm thời gian quý giá, tăng tỷ lệ tương tác khách hàng và giảm rủi ro mất khách hàng. Với chỉ 10 phút cấu hình, bạn đã có một hệ thống nhắc nhở khách hàng hoàn chỉnh hoạt động 24/7. Hãy áp dụng ngay để nâng cao hiệu quả kinh doanh của bạn!