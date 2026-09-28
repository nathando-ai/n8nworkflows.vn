---
title: "🚀 Lưu dữ liệu từ Webhook vào file JSON - Workflow n8n đơn giản"
description: "Hướng dẫn tự động lưu dữ liệu nhận được từ webhook vào file JSON bằng workflow n8n, tiết kiệm thời gian và tránh mất dữ liệu quan trọng."
slug: "luu-du-lieu-tu-webhook-vao-json"
tags: [n8n, automation, no-code, webhook, json]
keywords: [n8n workflow, tự động hóa, webhook, lưu dữ liệu, json]
---

# 🚀 Lưu dữ liệu từ Webhook vào file JSON - Workflow n8n đơn giản

[Các sếp đang gặp khó khăn khi phải xử lý dữ liệu từ webhook một cách thủ công. Với workflow này, các sếp có thể tự động lưu dữ liệu nhận được từ webhook vào file JSON, giúp tiết kiệm thời gian và tránh mất dữ liệu quan trọng.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động lưu dữ liệu từ webhook vào file JSON, tránh mất dữ liệu quan trọng.
- Tiết kiệm thời gian xử lý dữ liệu thủ công.
- Dễ dàng quản lý và truy xuất dữ liệu.
- Hoạt động liên tục 24/7, không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n đã cài đặt và cấu hình.
- Quyền truy cập vào thư mục lưu trữ file JSON.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấp vào nút "Import from URL".
3. Dán link sau vào ô nhập liệu: [https://n8n.io/workflows/652](https://n8n.io/workflows/652).
4. Nhấp vào nút "Import".

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "On clicking 'execute'"**: Không cần cấu hình gì thêm.
- **Node "HTTP Request"**: Cấu hình URL và phương thức HTTP để nhận dữ liệu từ webhook.
- **Node "Move Binary Data"**: Không cần cấu hình gì thêm.
- **Node "Write Binary File"**: Cấu hình đường dẫn thư mục lưu trữ file JSON.

#### 3. Kích hoạt ⚡️
1. Nhấp vào nút "Execute" để test workflow.
2. Kiểm tra dữ liệu được lưu vào file JSON.
3. Bật Active workflow để chạy liên tục.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi dữ liệu được lưu thành công.
- Lưu log các lần lưu dữ liệu để theo dõi lịch sử.
- Gửi báo cáo định kỳ về dữ liệu đã lưu.

### 📌 Kết luận
Workflow này giúp các sếp tự động lưu dữ liệu từ webhook vào file JSON một cách dễ dàng và hiệu quả. Hãy áp dụng ngay để tiết kiệm thời gian và tránh mất dữ liệu quan trọng.