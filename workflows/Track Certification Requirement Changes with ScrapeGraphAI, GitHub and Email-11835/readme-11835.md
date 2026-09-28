---
title: "🚀 Theo dõi thay đổi yêu cầu chứng chỉ với ScrapeGraphAI, GitHub và Email"
description: "Tự động hóa việc theo dõi thay đổi yêu cầu chứng chỉ từ các trang web của cơ quan cấp chứng chỉ, nhận thông báo qua email khi có cập nhật mới."
slug: "theo-doi-thay-doi-yeu-cau-chung-chi"
tags: [n8n, automation, no-code, web-scraping, ai]
keywords: [n8n workflow, tự động hóa, theo dõi chứng chỉ, ScrapeGraphAI, GitHub]
---

# 🚀 Theo dõi thay đổi yêu cầu chứng chỉ với ScrapeGraphAI, GitHub và Email

[Các sếp] có bao giờ phải mất thời gian truy cập từng trang web của cơ quan cấp chứng chỉ để kiểm tra thay đổi yêu cầu không? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình theo dõi thay đổi yêu cầu chứng chỉ, nhận thông báo qua email ngay khi có cập nhật mới.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Không cần truy cập từng trang web để kiểm tra thay đổi.
- Chính xác: Dữ liệu được trích xuất và so sánh tự động, giảm thiểu lỗi con người.
- Cá nhân hóa: Nhận thông báo chỉ khi có thay đổi thực sự.
- Hoạt động liên tục: Theo dõi 24/7 mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản ScrapeGraphAI (để trích xuất dữ liệu từ trang web).
- Tài khoản GitHub (để lưu trữ và so sánh dữ liệu).
- Địa chỉ email (để nhận thông báo).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [trang workflow](https://n8n.io/workflows/11835).
2. Click vào nút "Download Workflow" để tải file JSON.
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Scrape Certification Page"**: Cần cấu hình credentials cho ScrapeGraphAI.
- **Node "Define Certification URLs"**: Cập nhật danh sách URL của các trang web cần theo dõi.
- **Node "GitHub – Get Previous Snapshot" và "GitHub – Upsert Snapshot"**: Cấu hình credentials cho GitHub và chỉ định repository để lưu trữ dữ liệu.
- **Node "Email Send Notification"**: Cấu hình địa chỉ email gửi và nhận thông báo.

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu bằng cách kích hoạt node "Start Manual".
2. Bật Active workflow để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- Thay thế node "Start Manual" bằng node "Schedule Trigger" để chạy workflow định kỳ (ví dụ: hàng ngày).
- Kết hợp với Slack hoặc Telegram để nhận thông báo thay vì email.
- Lưu log thay đổi vào Google Sheets hoặc Notion để theo dõi lịch sử thay đổi.
- Gửi báo cáo định kỳ (ví dụ: hàng tuần) về các thay đổi quan trọng.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc theo dõi thay đổi yêu cầu chứng chỉ, tiết kiệm thời gian và giảm thiểu lỗi. Hãy áp dụng ngay để tối ưu hóa quá trình quản lý chứng chỉ của mình!