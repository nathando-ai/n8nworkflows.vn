---
title: "🚀 Tự động kiểm tra địa chỉ email hợp lệ cho liên hệ mới trong HighLevel bằng Lob"
description: "Hướng dẫn tự động hóa kiểm tra địa chỉ email hợp lệ cho liên hệ mới trong HighLevel bằng Lob, tiết kiệm thời gian và đảm bảo chính xác dữ liệu"
slug: "tu-dong-kiem-tra-dia-chi-email-hop-le-highlevel-lob"
tags: [n8n, automation, no-code, crm, marketing]
keywords: [n8n workflow, tự động hóa, kiểm tra địa chỉ email, HighLevel, Lob]
---

# 🚀 Tự động kiểm tra địa chỉ email hợp lệ cho liên hệ mới trong HighLevel bằng Lob

[Các sếp] có biết rằng việc quản lý danh sách liên hệ là một trong những công việc quan trọng nhất trong marketing? Tuy nhiên, việc nhập thủ công địa chỉ email và kiểm tra tính hợp lệ của chúng thường tốn thời gian và dễ gây sai sót. Workflow này sẽ giúp các sếp tự động hóa quy trình này một cách hoàn toàn không cần code, đảm bảo dữ liệu luôn chính xác và tiết kiệm thời gian quý giá.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động kiểm tra địa chỉ email mà không cần can thiệp thủ công.
- **Đảm bảo chính xác**: Giảm thiểu sai sót khi nhập liệu thủ công.
- **Tối ưu danh sách liên hệ**: Chỉ giữ lại những địa chỉ email hợp lệ trong hệ thống.
- **Tự động hóa quy trình**: Tích hợp liền mạch với HighLevel để cập nhật trạng thái địa chỉ email.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản HighLevel đã kích hoạt API.
- Tài khoản Lob.com với API key (hướng dẫn tạo tại [đây](https://help.lob.com/account-management/api-keys)).
- Webhook URL từ HighLevel để nhận dữ liệu liên hệ mới.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/2171](https://n8n.io/workflows/2171)
2. Click vào nút "Import" để tải file JSON về máy.
3. Trong n8n Editor, click vào menu "Workflows" → "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "CRM Webhook Trigger"**:
   - Đảm bảo đã cấu hình webhook trong HighLevel để gửi dữ liệu liên hệ mới đến n8n.
   - Kiểm tra lại `path` và `httpMethod` trong node này.

2. **Node "Address Verification"**:
   - Cập nhật credentials của Lob.com (Basic Auth) trong node này.
   - Đảm bảo API key của Lob.com đã được kích hoạt và có quyền truy cập.

3. **Node "Update HighLevel - Deliverable"**:
   - Cập nhật credentials của HighLevel trong node này.
   - Chỉnh sửa các tham số như `Tag` hoặc `Field` để cập nhật trạng thái địa chỉ email hợp lệ.

4. **Node "Update HighLevel - NOT Deliverable"**:
   - Cập nhật credentials của HighLevel trong node này.
   - Chỉnh sửa các tham số như `Tag` hoặc `Field` để cập nhật trạng thái địa chỉ email không hợp lệ.

5. **Node "Switch"**:
   - Kiểm tra logic điều kiện trong node này để đảm bảo chuyển hướng đúng giữa các node cập nhật trạng thái.

#### 3. Kích hoạt ⚡️
1. **Test run dữ liệu mẫu**:
   - Tạo một liên hệ mới trong HighLevel và kiểm tra xem workflow có nhận được dữ liệu và xử lý đúng không.
2. **Bật Active workflow**:
   - Sau khi kiểm tra và đảm bảo workflow hoạt động đúng, bật chế độ Active để workflow chạy tự động khi có liên hệ mới được thêm vào HighLevel.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node gửi thông báo đến Slack hoặc Telegram khi có địa chỉ email không hợp lệ.
- **Lưu log kiểm tra**: Thêm node lưu log kiểm tra địa chỉ email vào Google Sheets hoặc cơ sở dữ liệu để theo dõi lịch sử kiểm tra.
- **Gửi báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo hàng tuần về số lượng địa chỉ email hợp lệ và không hợp lệ.
- **Tích hợp với các dịch vụ khác**: Kết nối với các dịch vụ khác như Mailchimp, SendGrid để tự động thêm hoặc loại bỏ địa chỉ email không hợp lệ.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình kiểm tra địa chỉ email hợp lệ cho liên hệ mới trong HighLevel một cách hiệu quả và chính xác. Bằng cách áp dụng workflow này, các sếp có thể tiết kiệm thời gian, giảm thiểu sai sót và tối ưu danh sách liên hệ trong hệ thống. Hãy áp dụng ngay để nâng cao hiệu quả marketing của doanh nghiệp!