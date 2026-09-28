---
title: "🔗 Weekly Website Link Checker with Slack Alerts for Broken URLs"
description: "Tự động kiểm tra liên kết hỏng hàng tuần và thông báo qua Slack với workflow n8n đơn giản, tiết kiệm thời gian và nâng cao độ tin cậy của trang web."
slug: "weekly-website-link-checker-with-slack-alerts"
tags: [n8n, automation, no-code, devops, slack]
keywords: [n8n workflow, tự động hóa, kiểm tra liên kết, devops, slack alerts]
---

# 🔗 Weekly Website Link Checker with Slack Alerts for Broken URLs

[Các sếp đang gặp khó khăn khi phải kiểm tra thủ công hàng trăm liên kết trên trang web hàng tuần. Với workflow này, các sếp có thể tự động hóa quy trình này và nhận thông báo ngay khi có liên kết hỏng, giúp bảo trì trang web hiệu quả hơn.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động kiểm tra hàng tuần mà không cần can thiệp thủ công.
- **Nâng cao độ tin cậy**: Nhận thông báo ngay khi có liên kết hỏng, đảm bảo trải nghiệm người dùng tốt hơn.
- **Dễ dàng theo dõi**: Danh sách liên kết hỏng được lưu trữ và có thể truy cập bất kỳ lúc nào.
- **Tích hợp Slack**: Thông báo tức thời qua Slack, giúp team nhanh chóng phản hồi và khắc phục.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Slack API Credentials**: Cần tạo một Slack App và lấy API token để gửi thông báo.
- **URL của trang web**: Địa chỉ trang web cần kiểm tra liên kết.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/6647](https://n8n.io/workflows/6647).
3. Hoặc tải file JSON về và import từ local.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Weekly Cron Trigger**: Cấu hình lịch chạy hàng tuần (ví dụ: mỗi Chủ Nhật lúc 9:00 AM).
- **Scan Blog with HTTP**: Cập nhật URL của trang web cần kiểm tra.
- **Send Slack Alert**: Cấu hình Slack API credentials và kênh nhận thông báo.

#### 3. Kích hoạt ⚡️
1. Nhấn vào nút "Execute Node" để kiểm tra workflow với dữ liệu mẫu.
2. Sau khi kiểm tra thành công, nhấn vào nút "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Google Sheets**: Lưu danh sách liên kết hỏng vào Google Sheets để theo dõi lâu dài.
- **Thêm Email Notification**: Gửi email thông báo khi có liên kết hỏng.
- **Kiểm tra định kỳ**: Thay đổi lịch chạy từ hàng tuần sang hàng ngày nếu cần độ chính xác cao hơn.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc kiểm tra liên kết hàng tuần, nâng cao độ tin cậy của trang web và tiết kiệm thời gian quý giá. Hãy áp dụng ngay để nâng cao hiệu suất làm việc!