---
title: "🚀 Tự động đồng bộ vé Zendesk với chủ sở hữu liên hệ Pipedrive"
description: "Hướng dẫn tự động hóa đồng bộ vé từ Zendesk sang Pipedrive để quản lý liên hệ hiệu quả hơn, tiết kiệm thời gian và nâng cao trải nghiệm khách hàng."
slug: "tu-dong-dong-bo-ve-zendesk-voi-chu-so-huu-lien-he-pipedrive"
tags: [n8n, automation, no-code, Zendesk, Pipedrive]
keywords: [n8n workflow, tự động hóa, Zendesk, Pipedrive, quản lý liên hệ]
---

# 🚀 Tự động đồng bộ vé Zendesk với chủ sở hữu liên hệ Pipedrive

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động đồng bộ vé từ Zendesk sang Pipedrive hàng ngày, giảm thiểu công việc thủ công.
- Tăng tính chính xác: Dữ liệu được đồng bộ chính xác, tránh sai sót do nhập liệu thủ công.
- Nâng cao trải nghiệm khách hàng: Chủ sở hữu liên hệ Pipedrive có thể theo dõi và tương tác với khách hàng một cách hiệu quả hơn.
- Hoạt động liên tục: Workflow chạy tự động hàng ngày vào lúc 9:00 sáng, đảm bảo dữ liệu luôn được cập nhật.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Zendesk với quyền truy cập API.
- Tài khoản Pipedrive với quyền truy cập API.
- API keys của cả hai dịch vụ trên.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/1807](https://n8n.io/workflows/1807).
3. Hoặc tải file JSON về và import từ file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Node "Get Zendesk comments for tickets"**: Cần cấu hình credentials của Zendesk API.
- **Node "Search persons by email"**: Cần cấu hình credentials của Pipedrive API.
- **Node "Every day at 09:00"**: Có thể điều chỉnh thời gian chạy workflow theo nhu cầu.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi workflow chạy thành công hoặc gặp lỗi.
- Lưu log hoạt động của workflow để theo dõi hiệu suất và phát hiện lỗi.
- Gửi báo cáo định kỳ về số lượng vé đã đồng bộ để giám sát hiệu quả của workflow.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quá trình đồng bộ vé từ Zendesk sang Pipedrive, tiết kiệm thời gian và nâng cao hiệu quả quản lý liên hệ. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của bạn!