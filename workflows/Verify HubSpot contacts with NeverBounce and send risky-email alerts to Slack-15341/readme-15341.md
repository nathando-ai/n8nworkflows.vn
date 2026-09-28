---
title: "🚀 Tự động kiểm tra email HubSpot với NeverBounce và cảnh báo nguy cơ rò rỉ qua Slack"
description: "Workflow n8n tự động hóa việc kiểm tra danh sách liên hệ HubSpot hàng ngày, xác định email nguy cơ và gửi cảnh báo ngay lập tức qua Slack"
slug: "tu-dong-kiem-tra-email-hubspot-neverbounce-slack"
tags: [n8n, automation, no-code, crm, email-verification]
keywords: [n8n workflow, tự động hóa, kiểm tra email, HubSpot, NeverBounce, Slack]
---

# 🚀 Tự động kiểm tra email HubSpot với NeverBounce và cảnh báo nguy cơ rò rỉ qua Slack

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quá trình kiểm tra email nguy cơ
- Giảm thời gian kiểm tra từ hàng giờ xuống chỉ vài phút
- Nhận cảnh báo ngay lập tức khi phát hiện email nguy cơ
- Tăng tính chính xác của danh sách liên hệ HubSpot
- Tiết kiệm chi phí cho các dịch vụ email verification
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản HubSpot với quyền truy cập API
- API Key từ NeverBounce
- Kênh Slack để nhận báo cáo
- Tài khoản n8n đã cài đặt các credentials cần thiết
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Run Daily** (scheduleTrigger):
   - Cấu hình lịch chạy hàng ngày (hoặc theo nhu cầu của bạn)
   - Thiết lập thời gian chạy phù hợp với hoạt động kinh doanh

2. **Get many contacts** (hubspot):
   - Chọn credentials HubSpot của bạn
   - Cấu hình các tham số lấy danh sách liên hệ (có thể lọc theo trạng thái, ngày tạo...)

3. **NeverBounce: Verify Email** (nbEmailVerification):
   - Thêm credentials NeverBounce API Key
   - Có thể cấu hình số lượng email kiểm tra mỗi lần chạy

4. **Hubspot: flag risky contact** (hubspot):
   - Chọn credentials HubSpot
   - Cấu hình mapping trạng thái liên hệ nguy cơ (mặc định là chuyển trạng thái sang "Disqualified")

5. **Slack final audit report** (slack):
   - Thêm credentials Slack
   - Chọn kênh nhận báo cáo cuối cùng

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node lưu log kiểm tra vào Google Sheets để theo dõi lịch sử
- Kết hợp với workflow gửi email thông báo cho các liên hệ nguy cơ
- Cấu hình cảnh báo qua Telegram thay vì Slack
- Thiết lập báo cáo định kỳ gửi qua email

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình kiểm tra email nguy cơ trong danh sách liên hệ HubSpot, giảm thiểu rủi ro liên lạc với email không hợp lệ và tăng hiệu quả hoạt động kinh doanh. Hãy thử ngay và tiết kiệm thời gian quý giá của bạn!