---
title: "🚀 Tự động đồng bộ file Markdown từ Google Drive lên trang Confluence"
description: "Hướng dẫn tự động hóa đồng bộ nội dung Markdown từ Google Drive lên Confluence bằng n8n, tiết kiệm thời gian và đảm bảo tính nhất quán của tài liệu."
slug: "tu-dong-dong-bo-markdown-google-drive-confluence"
tags: [n8n, automation, no-code, google-drive, confluence]
keywords: [n8n workflow, tự động hóa tài liệu, đồng bộ nội dung, google drive, confluence]
---

# 🚀 Tự động đồng bộ file Markdown từ Google Drive lên trang Confluence

[Các sếp làm việc với tài liệu kỹ thuật thường gặp khó khăn khi phải chuyển đổi và cập nhật nội dung giữa các hệ thống khác nhau. Với workflow này, các sếp có thể tự động đồng bộ nội dung Markdown từ Google Drive lên trang Confluence, đảm bảo tính nhất quán và tiết kiệm thời gian đáng kể.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động đồng bộ nội dung Markdown từ Google Drive lên Confluence.
- Tiết kiệm thời gian và giảm thiểu lỗi do thủ công.
- Đảm bảo tính nhất quán của tài liệu giữa các hệ thống.
- Tự động cập nhật nội dung khi có thay đổi trong Google Drive.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive với quyền truy cập vào các file Markdown cần đồng bộ.
- Tài khoản Confluence với quyền tạo và chỉnh sửa trang.
- API Key hoặc Credentials cho Google Drive và Confluence.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Google Drive Trigger**: Cấu hình để theo dõi các thay đổi trong thư mục Google Drive.
- **Extract from File**: Trích xuất nội dung từ file Markdown.
- **HTTP Request**: Gửi yêu cầu API để tạo hoặc cập nhật trang Confluence.
- **Markdown**: Chuyển đổi nội dung Markdown thành định dạng HTML phù hợp với Confluence.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack để thông báo khi đồng bộ thành công hoặc thất bại.
- Lưu log các hoạt động đồng bộ để theo dõi và kiểm tra.
- Tự động gửi báo cáo định kỳ về trạng thái đồng bộ.

### 📌 Kết luận
Với workflow này, các sếp có thể tự động đồng bộ nội dung Markdown từ Google Drive lên trang Confluence, đảm bảo tính nhất quán và tiết kiệm thời gian đáng kể. Hãy áp dụng ngay để nâng cao hiệu quả làm việc!