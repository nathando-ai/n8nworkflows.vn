---
title: "🚀 Theo dõi hiệu suất hỗ trợ từ Zendesk & Freshdesk với Google Sheets, Slack & Gmail"
description: "Tự động hóa theo dõi hiệu suất hỗ trợ khách hàng từ hai nền tảng Zendesk và Freshdesk, tính toán các chỉ số quan trọng và gửi báo cáo hàng tuần qua Slack và Email."
slug: "theo-doi-hieu-suat-ho-tro-zendesk-freshdesk-voi-sheets-slack-gmail"
tags: [n8n, automation, no-code, Zendesk, Freshdesk, Google Sheets, Slack, Gmail]
keywords: [n8n workflow, tự động hóa, theo dõi hiệu suất hỗ trợ, Zendesk, Freshdesk, Google Sheets, Slack, Gmail]
---

# 🚀 Theo dõi hiệu suất hỗ trợ từ Zendesk & Freshdesk với Google Sheets, Slack & Gmail

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải theo dõi hiệu suất hỗ trợ khách hàng từ nhiều nền tảng khác nhau. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code để tập trung vào công việc quan trọng hơn.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quá trình theo dõi hiệu suất hỗ trợ từ hai nền tảng Zendesk và Freshdesk.
- Tính toán tự động các chỉ số quan trọng như SLA, tỷ lệ giải quyết, thời gian phản hồi trung bình.
- Nhận báo cáo hàng tuần qua Slack và Email với giao diện chuyên nghiệp.
- Theo dõi các chỉ số quan trọng trong Google Sheets để phân tích lịch sử.
- Nhận cảnh báo tức thời khi các chỉ số vượt ngưỡng cho phép.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Zendesk và Freshdesk với quyền truy cập API.
- Tài khoản Google với quyền truy cập Google Sheets API.
- Tài khoản Slack với quyền gửi tin nhắn vào kênh.
- Tài khoản Gmail để gửi email báo cáo.
- Google Sheets đã tạo sẵn để lưu trữ dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào trang [n8n.io/workflows/8814](https://n8n.io/workflows/8814)
2. Click vào nút "Download" để tải file JSON của workflow.
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Weekly Trigger"**:
   - Cấu hình lịch chạy hàng tuần (mặc định là 20:00 mỗi tuần).

2. **Node "Fetch Tickets From Zendesk"**:
   - Thêm credentials Zendesk API.
   - Cấu hình các tham số cần thiết như trạng thái vé (open, pending, solved, closed).

3. **Node "Fetch Tickets From Freshdesk"**:
   - Thêm credentials Freshdesk API.
   - Cấu hình các tham số cần thiết như trạng thái vé (Open, Pending, Resolved, Closed).

4. **Node "Log KPIs in Google Sheets"**:
   - Thêm credentials Google Sheets API.
   - Cập nhật ID của Google Sheet và tên của sheet cần ghi dữ liệu.

5. **Node "Send Slack Alert"**:
   - Thêm credentials Slack API.
   - Cập nhật tên kênh Slack để gửi cảnh báo.

6. **Node "Send Weekly Email"**:
   - Thêm credentials Gmail API.
   - Cập nhật địa chỉ email người nhận báo cáo hàng tuần.

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Bật Active workflow để chạy tự động hàng tuần.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với các công cụ khác như Telegram để nhận cảnh báo tức thời.
- Lưu log chi tiết các hoạt động vào Google Sheets để theo dõi lịch sử.
- Gửi báo cáo định kỳ hàng tháng hoặc hàng quý bằng cách điều chỉnh node "Weekly Trigger".
- Tích hợp với các công cụ khác như Power BI để tạo báo cáo trực quan hơn.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình theo dõi hiệu suất hỗ trợ khách hàng từ hai nền tảng Zendesk và Freshdesk. Với các báo cáo hàng tuần qua Slack và Email, các sếp có thể dễ dàng theo dõi và quản lý hiệu suất hỗ trợ khách hàng một cách hiệu quả. Hãy áp dụng ngay để tiết kiệm thời gian và tập trung vào công việc quan trọng hơn!