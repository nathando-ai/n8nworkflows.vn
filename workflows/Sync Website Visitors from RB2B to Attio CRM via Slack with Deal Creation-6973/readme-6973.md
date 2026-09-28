---
title: "🚀 Tự động đồng bộ khách truy cập website từ RB2B sang Attio CRM với tạo deal thông minh"
description: "Hướng dẫn chi tiết cách tự động hóa việc đồng bộ khách truy cập website từ RB2B sang Attio CRM với tạo deal thông minh, tiết kiệm thời gian và nâng cao hiệu quả chăm sóc khách hàng"
slug: "tu-dong-dong-bo-khach-truy-cap-website-rb2b-sang-attio-crm"
tags: [n8n, automation, no-code, crm, sales]
keywords: [n8n workflow, tự động hóa, rb2b, attio, slack, lead generation]
---

# 🚀 Tự động đồng bộ khách truy cập website từ RB2B sang Attio CRM với tạo deal thông minh

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý thủ công lên tới 90%
- Giảm thiểu lỗi nhập liệu nhờ tự động hóa hoàn toàn
- Tăng cường hiệu quả chăm sóc khách hàng với dữ liệu chính xác
- Hoạt động liên tục 24/7 mà không cần can thiệp
- Tạo cơ hội bán hàng tiềm năng từ khách truy cập website
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản RB2B với tích hợp Slack đã kích hoạt
- Tài khoản Attio CRM với quyền truy cập API
- Không gian làm việc Slack với quyền hạn bot
- API Key từ RB2B và Attio CRM
- Kênh Slack được chỉ định để nhận thông báo từ RB2B
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/6973](https://n8n.io/workflows/6973)
2. Nhấn nút "Import" trên trang workflow
3. Trong n8n Editor, chọn "Import from URL" và dán link workflow
4. Hoặc copy toàn bộ JSON workflow và chọn "Import from JSON"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node RB2B New Message**:
   - Thêm credentials Slack API
   - Chọn kênh Slack được chỉ định để nhận thông báo từ RB2B

2. **Node Get Person**:
   - Thêm credentials HTTP Custom Auth và HTTP Header Auth
   - Cấu hình URL API Attio để tìm kiếm người dùng
   - Đảm bảo có quyền "read" trong Attio API

3. **Node Create Person**:
   - Thêm credentials HTTP Custom Auth và HTTP Header Auth
   - Cấu hình URL API Attio để tạo người dùng mới
   - Đảm bảo có quyền "write" trong Attio API

4. **Node Create Deal**:
   - Thêm credentials HTTP Header Auth
   - Cấu hình URL API Attio để tạo deal mới
   - Đảm bảo có quyền "write" trong Attio API

5. **Node Create Associated Deal**:
   - Thêm credentials HTTP Header Auth
   - Cấu hình URL API Attio để tạo deal liên quan
   - Đảm bảo có quyền "write" trong Attio API

6. **Node Update Deal Stage**:
   - Thêm credentials HTTP Header Auth
   - Cấu hình URL API Attio để cập nhật giai đoạn deal
   - Đảm bảo có quyền "write" trong Attio API

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra kết nối và xử lý dữ liệu
2. Kích hoạt workflow bằng cách nhấn nút "Active" trên thanh công cụ

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack để nhận thông báo khi có khách truy cập mới
2. Thêm node gửi email thông báo cho đội ngũ bán hàng
3. Tích hợp với Google Sheets để lưu trữ dữ liệu khách truy cập
4. Tự động hóa việc gửi email chào mừng cho khách truy cập mới

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình đồng bộ khách truy cập website từ RB2B sang Attio CRM, tạo cơ hội bán hàng tiềm năng và nâng cao hiệu quả chăm sóc khách hàng. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả kinh doanh!