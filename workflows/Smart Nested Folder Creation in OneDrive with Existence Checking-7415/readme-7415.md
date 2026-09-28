---
title: "📂 Tự động tạo thư mục lồng nhau trong OneDrive với kiểm tra tồn tại"
description: "Hướng dẫn tự động hóa tạo thư mục lồng nhau trong OneDrive bằng n8n, tiết kiệm thời gian và tránh lỗi trùng lặp thư mục"
slug: "tu-dong-tao-thu-muc-long-nhau-trong-onedrive"
tags: [n8n, automation, no-code, OneDrive, file-management]
keywords: [n8n workflow, tự động hóa, OneDrive, tạo thư mục, quản lý file]
---

# 📂 Tự động tạo thư mục lồng nhau trong OneDrive với kiểm tra tồn tại

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quá trình tạo thư mục lồng nhau trong OneDrive
- Kiểm tra tồn tại thư mục trước khi tạo, tránh lỗi trùng lặp
- Tiết kiệm thời gian đáng kể so với làm thủ công
- Đảm bảo cấu trúc thư mục nhất quán và chính xác
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Microsoft 365 với quyền truy cập OneDrive
- Quyền truy cập vào n8n instance (self-hosted hoặc cloud)
- Thông tin xác thực Microsoft OneDrive OAuth2
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link sau: [https://n8n.io/workflows/7415](https://n8n.io/workflows/7415)
3. Hoặc tải file JSON về và import từ local

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "When Executed by Another Workflow"**:
   - Đảm bảo workflow này được cấu hình để chạy như một sub-workflow
   - Kiểm tra biến đầu vào `$folder` chứa đường dẫn thư mục lồng nhau

2. **Node "Paths" (Code)**:
   - Kiểm tra và chỉnh sửa giá trị mặc định nếu cần (ví dụ: `Foobar/Barfur/Furbar`)
   - Đảm bảo định dạng đường dẫn đúng (các thư mục phân cách bởi dấu '/')

3. **Node "Search" (Microsoft OneDrive)**:
   - Cấu hình credentials cho Microsoft OneDrive OAuth2
   - Kiểm tra quyền truy cập của tài khoản có đủ để tìm kiếm thư mục

4. **Node "Create a folder" (Microsoft OneDrive)**:
   - Cấu hình credentials cho Microsoft OneDrive OAuth2
   - Kiểm tra quyền tạo thư mục trong OneDrive

#### 3. Kích hoạt ⚡️
1. Test run với dữ liệu mẫu (ví dụ: `Foobar/Barfur/Furbar`)
2. Kiểm tra kết quả trong OneDrive để xác nhận thư mục đã được tạo đúng
3. Bật Active workflow sau khi xác nhận hoạt động ổn định

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack/Teams để thông báo khi tạo thư mục thành công
2. Lưu log các hoạt động tạo thư mục vào Google Sheets/Excel
3. Tự động gửi báo cáo hàng tuần về các thư mục mới được tạo
4. Kết hợp với workflow khác để tự động di chuyển file vào thư mục mới tạo

### 📌 Kết luận
Workflow này là giải pháp hoàn hảo cho các sếp cần tự động hóa việc tạo thư mục lồng nhau trong OneDrive một cách chính xác và hiệu quả. Với khả năng kiểm tra tồn tại trước khi tạo, workflow giúp tránh các lỗi trùng lặp và đảm bảo cấu trúc thư mục luôn nhất quán. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu suất làm việc!