---
title: "🚀 Gửi cảnh báo tồn kho thấp hàng tuần từ WooCommerce tới Slack và Jira"
description: "Workflow tự động kiểm tra tồn kho, gửi cảnh báo tới Slack và tạo ticket Jira khi tồn kho quá thấp."
slug: "send-weekly-low-stock-alerts-from-woocommerce-to-slack-and-jira"
tags: [n8n, automation, no-code, WooCommerce, Slack, Jira]
keywords: [n8n workflow, tự động hóa, WooCommerce, Slack, Jira, cảnh báo tồn kho]
---

# 🚀 Gửi cảnh báo tồn kho thấp hàng tuần từ WooCommerce tới Slack và Jira

Bạn đang phải mất hàng giờ mỗi tuần để kiểm tra tồn kho, gửi email cảnh báo và tạo ticket Jira thủ công? Workflow này sẽ giúp bạn **đánh trừ công việc lặp đi lặp lại** và **đảm bảo đội ngũ luôn được thông báo kịp thời** khi hàng tồn kho xuống mức nguy hiểm.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn phải chạy thủ công, tự động chạy vào lúc 00:00 Chủ Nhật.  
- **Độ chính xác cao**: Dữ liệu lấy trực tiếp từ WooCommerce, tránh sai sót do nhập liệu.  
- **Cá nhân hóa cảnh báo**: Định nghĩa ngưỡng tồn kho theo danh mục, gửi tới kênh Slack phù hợp.  
- **Hoạt động liên tục**: Jira issue được tạo ngay khi tồn kho quá thấp, giúp đội ngũ xử lý ngay lập tức.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **WooCommerce**: API key (Consumer Key & Consumer Secret).  
- **Slack**: Bot token và ID kênh cho cảnh báo thấp và cảnh báo khẩn cấp.  
- **Jira**: API token, Project ID, Issue type, Assignee, Priority.  
- **n8n**: Đã cài đặt và chạy (Self-hosted hoặc n8n.cloud).  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/13276) hoặc sao chép nội dung JSON.  
2. Mở **n8n Editor**, chọn **Import** → **Import from file** hoặc **Import from clipboard**.  
3. Chọn file JSON hoặc dán nội dung, rồi nhấn **Import**.  

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên | Cấu hình cần chỉnh | Ghi chú |
|------|-----|---------------------|---------|
| **Inventory Check Scheduler** | `Inventory Check Scheduler` | *Schedule* → *Every Monday at 00:00* | Đảm bảo workflow chạy đúng lịch. |
| **Get many products from WooCommerce** | `Get many products from WooCommerce` | *Credentials* → `wooCommerceApi` | Đảm bảo API key có quyền đọc sản phẩm. |
| **Separate products to low stock and very low stock** | `Separate products to low stock and very low stock` | *Code* → Đặt ngưỡng `lowStockThreshold` và `urgentStockThreshold` theo danh mục. | Ví dụ: `{"electronics": {"low": 10, "urgent": 3}}`. |
| **Format Low Stock Message** | `Format Low Stock Message` | *Code* → Định dạng tin nhắn Slack cho danh sách sản phẩm thấp. | Sử dụng `items.lowStock` trong `return`. |
| **Format Urgent Low Stock Message** | `Format Urgent Low Stock Message` | *Code* → Định dạng tin nhắn Slack cho danh sách sản phẩm khẩn cấp. | Sử dụng `items.urgentStock`. |
| **Format Urgent Low Stock Message for Jira** | `Format Urgent Low Stock Message for Jira` | *Code* → Tạo mô tả chi tiết cho issue Jira. | Sử dụng `items.urgentStock`. |
| **Create an Issue in Jira** | `Create an Issue in Jira` | *Credentials* → `jiraSoftwareCloudApi` <br>*Project* → ID dự án <br>*Issue Type* → `Task` hoặc `Bug` <br>*Assignee* → User ID <br>*Priority* → `High` | Đảm bảo quyền tạo issue. |
| **Send Urgent Low Stock Alert to Slack** | `Send Urgent Low Stock Alert to Slack` | *Credentials* → `slackApi` <br>*Channel ID* → Kênh khẩn cấp | Sử dụng `{{ $json["message"] }}`. |
| **Send Low Stock Alert to Slack** | `Send Low Stock Alert to Slack` | *Credentials* → `slackApi` <br>*Channel ID* → Kênh thông báo thấp | Sử dụng `{{ $json["message"] }}`. |

> **Tip**: Nếu bạn muốn thay đổi ngưỡng tồn kho, chỉ cần chỉnh trong node **Separate products to low stock and very low stock** mà không cần sửa code ở các node khác.

### 3. Kích hoạt ⚡️

1. **Test run**: Chạy workflow với dữ liệu mẫu (bấm **Execute Workflow**). Kiểm tra log, đảm bảo không có lỗi.  
2. **Bật Active**