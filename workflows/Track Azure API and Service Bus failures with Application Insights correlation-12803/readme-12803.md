---
title: "🚀 Theo dõi lỗi Azure API và Service Bus với Application Insights - Workflow n8n"
description: "Hướng dẫn tự động hóa theo dõi lỗi API Azure, Service Bus và ngoại lệ thông qua Application Insights với workflow n8n. Tiết kiệm thời gian gỡ lỗi và tối ưu hóa hiệu suất hệ thống."
slug: "theo-doi-loi-azure-api-service-bus-voi-application-insights"
tags: [n8n, automation, no-code, Azure, DevOps, Application Insights]
keywords: [n8n workflow, tự động hóa, Azure API, Service Bus, Application Insights]
---

# 🚀 Theo dõi lỗi Azure API và Service Bus với Application Insights - Workflow n8n

[Các sếp đang gặp khó khăn khi phải theo dõi thủ công các lỗi API Azure, Service Bus và ngoại lệ trong hệ thống của mình. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình theo dõi, phân tích và báo cáo lỗi một cách hiệu quả.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa toàn bộ quá trình theo dõi lỗi API Azure, Service Bus và ngoại lệ.
- Phân tích và tương quan dữ liệu một cách hiệu quả với operationId.
- Tạo báo cáo chi tiết dưới dạng Markdown và HTML.
- Xuất dữ liệu ra file Excel để dễ dàng chia sẻ và phân tích.
- Tích hợp với webhook để nhận kết quả qua các dịch vụ khác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Azure với quyền truy cập vào Application Insights.
- Application Insights Application ID và Azure AD tenant ID.
- Credentials Azure đã được cấu hình trong n8n.
- Thời gian thực thi (time range) cho truy vấn (24h, 7d, 30d).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/12803).
2. Click vào nút "Download" để tải file JSON.
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Set Configuration**: Cập nhật Application Insights Application ID và Azure AD tenant ID.
- **Query Application Insights**: Đảm bảo các truy vấn KQL được tối ưu hóa cho hệ thống của các sếp.
- **Export to Excel**: Cấu hình đường dẫn lưu file Excel nếu cần xuất dữ liệu.
- **Respond to Webhook**: Cấu hình URL webhook để nhận kết quả nếu cần.

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Bật Active workflow để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Teams để nhận thông báo lỗi ngay lập tức.
- Lưu log các lần chạy workflow để theo dõi lịch sử lỗi.
- Tạo báo cáo định kỳ và gửi qua email để theo dõi hiệu suất hệ thống.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình theo dõi lỗi API Azure, Service Bus và ngoại lệ một cách hiệu quả. Với các tính năng phân tích dữ liệu và tạo báo cáo chi tiết, các sếp có thể tối ưu hóa hiệu suất hệ thống và giảm thời gian gỡ lỗi. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của đội ngũ DevOps!