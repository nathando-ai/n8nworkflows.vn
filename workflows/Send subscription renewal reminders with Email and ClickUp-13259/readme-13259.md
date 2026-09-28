---
title: "🚀 Tự động nhắc nhở gia hạn đăng ký bằng Email và ClickUp - Workflow n8n hoàn hảo"
description: "Hướng dẫn chi tiết cách tự động gửi email nhắc nhở gia hạn đăng ký khách hàng qua n8n và ClickUp, tiết kiệm thời gian và nâng cao trải nghiệm khách hàng"
slug: "tu-dong-nhac-nho-gia-han-dang-ky-email-clickup"
tags: [n8n, automation, no-code, crm, email-marketing]
keywords: [n8n workflow, tự động hóa, nhắc nhở gia hạn, ClickUp, email marketing]
---

# 🚀 Tự động nhắc nhở gia hạn đăng ký bằng Email và ClickUp - Workflow n8n hoàn hảo

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi quản lý đăng ký khách hàng thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động gửi email nhắc nhở gia hạn đăng ký cho khách hàng trước ngày hết hạn
- Tiết kiệm thời gian quản lý thủ công
- Nâng cao trải nghiệm khách hàng với thông báo cá nhân hóa
- Nhận báo cáo tổng quan về tình trạng gia hạn đăng ký
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản ClickUp với danh sách đăng ký khách hàng
- Thông tin SMTP để gửi email
- Địa chỉ email gửi và địa chỉ email quản trị
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/13259](https://n8n.io/workflows/13259)
2. Click vào nút "Download" để tải file JSON workflow
3. Trong n8n Editor, click vào menu Workflows > Import from File
4. Chọn file JSON vừa tải về và click "Import"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Set Defaults"**:
   - Thay đổi `listId` bằng ID danh sách ClickUp của bạn
   - Cập nhật `senderEmail` và `adminEmail` với địa chỉ email thực tế

2. **Node "Incoming Request"**:
   - Giữ nguyên cấu hình webhook (path: "subscription-renewal", method: POST)

3. **Node "Filter Expiring & Build Data"**:
   - Điều chỉnh giá trị `daysThreshold` nếu muốn thay đổi ngưỡng nhắc nhở (mặc định 7 ngày)

4. **Node "Send Reminder Email"**:
   - Cấu hình SMTP credentials trong n8n và chọn đúng credentials này

5. **Node "Send Admin Summary"**:
   - Đảm bảo cấu hình SMTP giống với node gửi email nhắc nhở

#### 3. Kích hoạt ⚡️
1. Test run workflow bằng cách gửi request POST đến webhook URL
2. Kiểm tra email nhắc nhở được gửi đến khách hàng
3. Xác nhận báo cáo tổng quan được gửi đến email quản trị
4. Bật Active workflow để chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack**: Thêm node gửi thông báo Slack khi có đăng ký sắp hết hạn
2. **Lưu log**: Mở rộng node "Cleanup Execution" để lưu log các lần chạy
3. **Báo cáo định kỳ**: Thiết lập lịch chạy workflow hàng ngày để nhận báo cáo cập nhật
4. **Nhiều kênh nhắc nhở**: Thêm node gửi SMS nhắc nhở cho khách hàng quan trọng

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình nhắc nhở gia hạn đăng ký, tiết kiệm thời gian và nâng cao trải nghiệm khách hàng. Với cấu hình đơn giản và kết quả rõ ràng, đây là giải pháp hoàn hảo cho bất kỳ doanh nghiệp nào muốn tối ưu hóa quy trình quản lý đăng ký.