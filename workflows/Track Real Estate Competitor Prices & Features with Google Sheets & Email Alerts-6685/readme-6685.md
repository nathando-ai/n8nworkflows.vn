---
title: "🏠 Theo dõi giá và tính năng của đối thủ bất động sản với Google Sheets & Email Alerts"
description: "Hướng dẫn tự động hóa theo dõi giá và tính năng của đối thủ bất động sản bằng n8n, Google Sheets và email alerts. Tiết kiệm thời gian và nhận thông báo tức thì về thay đổi giá."
slug: "theo-doi-gia-tinh-nang-doi-thu-bat-dong-san"
tags: [n8n, automation, no-code, bat-dong-san, google-sheets]
keywords: [n8n workflow, tự động hóa bất động sản, theo dõi giá nhà, email alerts, google sheets]
---

# 🏠 Theo dõi giá và tính năng của đối thủ bất động sản với Google Sheets & Email Alerts

[Các sếp đang làm việc trong lĩnh vực bất động sản chắc hẳn đã gặp khó khăn khi phải theo dõi giá và tính năng của các đối thủ liên tục. Việc này không chỉ tốn thời gian mà còn dễ bỏ sót những thay đổi quan trọng. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình theo dõi, nhận thông báo tức thì về thay đổi giá và lưu trữ dữ liệu một cách chuyên nghiệp.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần theo dõi thủ công, nhận thông báo tức thì.
- **Chính xác**: Dữ liệu được lưu trữ và phân tích một cách chuyên nghiệp.
- **Cá nhân hóa**: Thiết lập ngưỡng giá và nhận thông báo chỉ khi có thay đổi đáng kể.
- **Hoạt động liên tục**: Workflow chạy tự động theo lịch trình đã đặt.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets API đã được kích hoạt.
- Tài khoản email (SMTP) để gửi thông báo.
- URL API của đối thủ bất động sản (hoặc dữ liệu mẫu để test).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào "Import from URL" và dán link: [https://n8n.io/workflows/6685](https://n8n.io/workflows/6685).
3. Hoặc tải file JSON về và import từ máy tính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Cron**: Thiết lập lịch chạy workflow (ví dụ: hàng giờ).
- **Fetch Competitor Data**: Cập nhật URL API của đối thủ bất động sản.
- **Log to Google Sheets**: Cấu hình Google Sheets API credentials và tên sheet.
- **Check Price Change**: Thiết lập ngưỡng giá để nhận thông báo (ví dụ: thay đổi > 5%).
- **Send Alert Email**: Cấu hình SMTP credentials và nội dung email.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Thêm Slack hoặc WhatsApp notifications để nhận thông báo đa kênh.
- Lưu log chi tiết hơn vào Google Sheets (ví dụ: timestamp, tên đối thủ).
- Tự động hóa báo cáo định kỳ với Google Data Studio.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và nhận thông báo tức thì về thay đổi giá của đối thủ bất động sản. Hãy áp dụng ngay để nâng cao hiệu quả kinh doanh!