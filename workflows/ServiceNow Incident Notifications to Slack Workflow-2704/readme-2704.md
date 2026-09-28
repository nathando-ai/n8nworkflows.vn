---
title: "🚀 Tự động hóa cảnh báo sự cố ServiceNow lên Slack mỗi 5 phút"
description: "Hướng dẫn chi tiết cách tự động hóa việc lấy và thông báo các sự cố mới từ ServiceNow lên Slack mỗi 5 phút, tiết kiệm thời gian và nâng cao hiệu quả quản lý IT."
slug: "tu-dong-hoa-canh-bao-su-co-servicenow-len-slack"
tags: [n8n, automation, no-code, ServiceNow, Slack]
keywords: [n8n workflow, tự động hóa, ServiceNow, Slack, IT Ops]
---

# 🚀 Tự động hóa cảnh báo sự cố ServiceNow lên Slack mỗi 5 phút

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp IT khi phải theo dõi thủ công các sự cố từ ServiceNow và gửi thông báo lên Slack. Giới thiệu workflow như giải pháp tự động hóa hoàn toàn không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Không cần theo dõi thủ công các sự cố mới từ ServiceNow.
- Tăng cường phản ứng: Nhận thông báo tức thì về các sự cố mới trong vòng 5 phút.
- Tăng cường hiệu quả: Các thành viên IT có thể tập trung vào việc xử lý sự cố thay vì theo dõi.
- Tăng cường minh bạch: Tất cả các sự cố đều được ghi lại và thông báo một cách tự động.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản ServiceNow với quyền truy cập API.
- Tài khoản Slack với quyền gửi tin nhắn vào kênh.
- API keys cho cả ServiceNow và Slack.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/2704](https://n8n.io/workflows/2704).
3. Hoặc tải file JSON về và import từ file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **ServiceNow Basic API**: Cần cấu hình credentials với URL của ServiceNow instance và API credentials của bạn.
- **Slack API**: Cần cấu hình credentials với token Slack của bạn.
- **Get Incidents from ServiceNow**: Cần cấu hình query để lấy các sự cố mới trong vòng 5 phút.
- **Post Incident Details to Slack Channel**: Cần cấu hình kênh Slack để gửi thông báo.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack để nhận thông báo qua điện thoại di động.
- Lưu log các sự cố vào Google Sheets hoặc cơ sở dữ liệu để phân tích.
- Gửi báo cáo định kỳ về các sự cố đã xử lý.

### 📌 Kết luận
Workflow này giúp các sếp IT tự động hóa việc theo dõi và thông báo các sự cố từ ServiceNow lên Slack mỗi 5 phút, tiết kiệm thời gian và nâng cao hiệu quả quản lý IT. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của bạn!