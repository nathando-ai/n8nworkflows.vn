---
title: "🚀 Tự động gửi link từ Telegram Channel đến Hoarder và Readeck"
description: "Workflow n8n tự động hóa việc lấy link từ Telegram Channel và gửi đến Hoarder và Readeck, giúp tiết kiệm thời gian và tự động hóa quy trình quản lý nội dung."
slug: "tu-dong-gui-link-tu-telegram-channel-den-hoarder-va-readeck"
tags: [n8n, automation, no-code, telegram, hoarder, readeck]
keywords: [n8n workflow, tự động hóa, telegram, hoarder, readeck]
---

# 🚀 Tự động gửi link từ Telegram Channel đến Hoarder và Readeck

[Các sếp đang làm việc với nhiều kênh Telegram và muốn tự động hóa việc gửi link đến các dịch vụ lưu trữ và quản lý nội dung như Hoarder và Readeck. Với workflow này, các sếp có thể tiết kiệm thời gian và tự động hóa quy trình này một cách dễ dàng.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa việc lấy link từ Telegram Channel và gửi đến Hoarder và Readeck.
- Tăng hiệu quả: Các link được lưu trữ và quản lý một cách tự động, giúp các sếp tập trung vào công việc quan trọng hơn.
- Tăng cường trải nghiệm người dùng: Các link được gửi đến các dịch vụ lưu trữ và quản lý nội dung một cách nhanh chóng và chính xác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram với quyền truy cập vào kênh cần lấy link.
- Tài khoản Hoarder và Readeck với API key.
- Tài khoản n8n đã được cài đặt và cấu hình.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và nhập URL: [https://n8n.io/workflows/3436](https://n8n.io/workflows/3436).
3. Nhấn vào nút "Import" để hoàn tất quá trình import.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Schedule Trigger**: Cấu hình thời gian chạy workflow.
- **channel_items_tg**: Cấu hình API key của Telegram và ID của kênh cần lấy link.
- **channel_links_tg**: Cấu hình code để lấy link từ Telegram.
- **not_saved_links_hd**: Cấu hình code để kiểm tra link chưa được lưu trong Hoarder.
- **not_saved_links_rd**: Cấu hình code để kiểm tra link chưa được lưu trong Readeck.
- **saved_links_hd**: Cấu hình biến để lưu trữ link đã được lưu trong Hoarder.
- **saved_links_rd**: Cấu hình biến để lưu trữ link đã được lưu trong Readeck.
- **save_link_hd**: Cấu hình API key của Hoarder và URL để lưu link.
- **save_link_rd**: Cấu hình API key của Readeck và URL để lưu link.
- **get_links_hd**: Cấu hình API key của Hoarder và URL để lấy link đã lưu.
- **get_links_rd**: Cấu hình API key của Readeck và URL để lấy link đã lưu.

#### 3. Kích hoạt ⚡️
1. Nhấn vào nút "Execute Workflow" để kiểm tra workflow.
2. Nhấn vào nút "Activate Workflow" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack hoặc Telegram để thông báo khi có link mới được lưu.
- Lưu log các link đã được lưu để theo dõi và quản lý.
- Gửi báo cáo định kỳ về số lượng link đã được lưu và quản lý.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc lấy link từ Telegram Channel và gửi đến Hoarder và Readeck, giúp tiết kiệm thời gian và tăng hiệu quả công việc. Các sếp chỉ cần cấu hình các thông số cần thiết và kích hoạt workflow để bắt đầu tự động hóa quy trình này.