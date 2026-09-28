---
title: "🚀 Tự động tải và đổi tên video lên Google Drive từ URL"
description: "Hướng dẫn tự động hóa tải video từ URL lên Google Drive và đổi tên file một cách nhanh chóng và chính xác bằng n8n"
slug: "tu-dong-tai-va-doi-ten-video-len-google-drive-tu-url"
tags: [n8n, automation, no-code, google-drive, video]
keywords: [n8n workflow, tự động hóa, google drive, video, đổi tên file]
---

# 🚀 Tự động tải và đổi tên video lên Google Drive từ URL

[Các sếp đang gặp khó khăn khi phải tải và đổi tên video thủ công trên Google Drive. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài phút, tiết kiệm thời gian và giảm thiểu lỗi.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động tải video từ URL lên Google Drive một cách nhanh chóng và chính xác.
- Đổi tên video một cách tự động theo quy tắc đã định sẵn.
- Giảm thiểu thời gian và công sức cho việc tải và đổi tên thủ công.
- Tăng tính chuyên nghiệp và hiệu quả trong quản lý nội dung video.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive với quyền truy cập đầy đủ.
- URL của video cần tải lên.
- Quyền truy cập vào n8n để import và cấu hình workflow.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL".
3. Dán link sau vào ô nhập liệu: `https://n8n.io/workflows/3815`.
4. Nhấn "Import" để tải workflow vào n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Node "When clicking ‘Test workflow’"**: Đây là node kích hoạt workflow. Các sếp có thể để nguyên hoặc thay đổi để kích hoạt theo các điều kiện khác.
- **Node "Rename Uploaded Video"**:
  - Chọn credentials là `googleDriveOAuth2Api`.
  - Đảm bảo tài khoản Google Drive có quyền truy cập đầy đủ.
  - Cấu hình tham số `operation` là `update`.
- **Node "Send URL to GDrive Script and Upload"**:
  - Cấu hình URL của video cần tải lên.
  - Đảm bảo URL hợp lệ và có thể truy cập được.

#### 3. Kích hoạt ⚡️
- Nhấn vào nút "Test workflow" để kiểm tra hoạt động của workflow.
- Kiểm tra kết quả trên Google Drive để đảm bảo video đã được tải lên và đổi tên đúng theo quy tắc đã định sẵn.
- Bật Active workflow để sử dụng trong thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với các công cụ khác như Slack hoặc Telegram để thông báo khi video đã được tải lên thành công.
- Lưu log hoạt động của workflow để theo dõi và kiểm tra lại khi cần thiết.
- Tự động gửi báo cáo định kỳ về các video đã được tải lên và quản lý.

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình tải và đổi tên video lên Google Drive một cách nhanh chóng và chính xác. Hãy áp dụng ngay để tiết kiệm thời gian và tăng hiệu quả công việc!