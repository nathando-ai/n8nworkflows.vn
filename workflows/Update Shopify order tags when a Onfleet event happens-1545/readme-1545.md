---
title: "🚀 Tự động cập nhật tags đơn hàng Shopify khi sự kiện Onfleet xảy ra"
description: "Workflow n8n tự động cập nhật tags đơn hàng Shopify khi trạng thái đơn hàng thay đổi trên Onfleet, giúp quản lý đơn hàng hiệu quả hơn."
slug: "tu-dong-cap-nhat-tags-don-hang-shopify-khi-su-kien-onfleet-xay-ra"
tags: [n8n, automation, no-code, shopify, onfleet]
keywords: [n8n workflow, tự động hóa, shopify, onfleet, quản lý đơn hàng]
---

# 🚀 Tự động cập nhật tags đơn hàng Shopify khi sự kiện Onfleet xảy ra

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động cập nhật tags đơn hàng Shopify khi trạng thái đơn hàng thay đổi trên Onfleet.
- Giảm thiểu công việc thủ công, tiết kiệm thời gian cho nhân viên.
- Quản lý đơn hàng hiệu quả hơn với thông tin cập nhật liên tục.
- Tăng tính chính xác và đồng bộ hóa dữ liệu giữa hai nền tảng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Shopify với quyền truy cập API.
- Tài khoản Onfleet với quyền truy cập API.
- API keys hoặc credentials cho cả hai nền tảng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Onfleet Trigger**: Cấu hình để lắng nghe các sự kiện từ Onfleet. Các sếp cần cung cấp API key của Onfleet và chọn các sự kiện cần theo dõi (ví dụ: "task_completed", "task_started").
- **Shopify**: Cấu hình để cập nhật tags đơn hàng. Các sếp cần cung cấp API key của Shopify và chỉ định các tham số cần thiết như "order_id" và "tags".

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để thông báo khi có sự kiện xảy ra.
- Lưu log các sự kiện để theo dõi lịch sử thay đổi.
- Gửi báo cáo định kỳ về trạng thái đơn hàng.

### 📌 Kết luận
Workflow này giúp các sếp tự động cập nhật tags đơn hàng Shopify khi trạng thái đơn hàng thay đổi trên Onfleet, giảm thiểu công việc thủ công và quản lý đơn hàng hiệu quả hơn. Hãy áp dụng ngay để tối ưu hóa quy trình kinh doanh!