---
title: "🚀 Đồng bộ bài viết từ Zendesk Knowledge Base sang Airtable với chuyển đổi Markdown"
description: "Hướng dẫn chi tiết cách tự động hóa việc đồng bộ nội dung từ Zendesk sang Airtable, bao gồm chuyển đổi HTML sang Markdown để dễ dàng sử dụng và chia sẻ."
slug: "dong-bo-zendesk-airtable-markdown"
tags: [n8n, automation, no-code, zendesk, airtable]
keywords: [n8n workflow, tự động hóa, zendesk, airtable, markdown]
---

# 🚀 Đồng bộ bài viết từ Zendesk Knowledge Base sang Airtable với chuyển đổi Markdown

[Các sếp đang gặp khó khăn khi phải chuyển đổi và quản lý nội dung từ Zendesk sang các hệ thống khác một cách thủ công. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này một cách dễ dàng, tiết kiệm thời gian và giảm thiểu lỗi.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quá trình đồng bộ nội dung từ Zendesk sang Airtable.
- Chất lượng dữ liệu: Chuyển đổi nội dung từ HTML sang Markdown để dễ dàng sử dụng và chia sẻ.
- Tính nhất quán: Đảm bảo dữ liệu được cập nhật liên tục và đồng bộ hóa một cách chính xác.
- Tính linh hoạt: Có thể sử dụng dữ liệu trong nhiều hệ thống khác nhau như Notion, Google Sheets, v.v.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Zendesk với quyền truy cập API (đọc quyền cho các bài viết trong trung tâm trợ giúp).
- Tài khoản Airtable với cơ sở dữ liệu đã được thiết lập theo [mẫu này](https://airtable.com/apptzJnbB6FphIprO/shrA6AhTkogTgrRn5).
- API key của Zendesk và Airtable.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào trang [n8n.io/workflows/5876](https://n8n.io/workflows/5876).
2. Nhấp vào nút "Import" để tải xuống file JSON của workflow.
3. Trong n8n Editor, nhấp vào nút "Import from File" và chọn file JSON đã tải xuống.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Set base_url**: Cập nhật URL cơ sở của Zendesk trong node "Set base_url".
- **Airtable Credentials**: Thêm thông tin xác thực Airtable trong node "Store Zendesk articles to Airtable".
- **Zendesk Credentials**: Thêm thông tin xác thực Zendesk trong node "Get articles since last run" và "Get all articles".
- **Airtable Base ID**: Cập nhật ID cơ sở dữ liệu Airtable trong node "Store Zendesk articles to Airtable".
- **Airtable Table Name**: Cập nhật tên bảng Airtable trong node "Store Zendesk articles to Airtable".

#### 3. Kích hoạt ⚡️
1. Nhấp vào nút "Execute workflow" để thực hiện đồng bộ dữ liệu lần đầu tiên.
2. Sau đó, cấu hình node "Schedule Trigger" để chạy workflow tự động theo lịch trình.
3. Nhấp vào nút "Active workflow" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm các node để gửi thông báo khi workflow hoàn thành hoặc gặp lỗi.
- **Lưu log**: Thêm các node để lưu log hoạt động của workflow để theo dõi và giải quyết vấn đề.
- **Gửi báo cáo định kỳ**: Thêm các node để gửi báo cáo định kỳ về số lượng bài viết đã đồng bộ.
- **Tích hợp với Notion**: Sử dụng dữ liệu Markdown để tạo các trang trong Notion.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc đồng bộ nội dung từ Zendesk sang Airtable một cách dễ dàng và chính xác. Với các tính năng chuyển đổi Markdown và cập nhật liên tục, các sếp có thể quản lý và sử dụng nội dung một cách hiệu quả hơn. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu suất làm việc!