---
title: "🚀 Cập nhật vai trò người dùng Zammad từ Excel - Workflow n8n tự động hóa"
description: "Hướng dẫn tự động hóa cập nhật vai trò người dùng Zammad từ file Excel bằng workflow n8n. Tiết kiệm thời gian và giảm lỗi thủ công."
slug: "cap-nhat-vai-tro-zammad-tu-excel"
tags: [n8n, automation, no-code, zammad, excel]
keywords: [n8n workflow, tự động hóa, zammad, excel, cập nhật vai trò]
---

# 🚀 Cập nhật vai trò người dùng Zammad từ Excel - Workflow n8n tự động hóa

[Các sếp đang gặp khó khăn khi phải cập nhật vai trò người dùng Zammad thủ công từ file Excel. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài bước đơn giản.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể khi cập nhật hàng loạt vai trò người dùng
- Giảm thiểu lỗi thủ công trong quá trình cập nhật
- Tự động hóa toàn bộ quy trình cập nhật vai trò
- Dễ dàng quản lý và theo dõi quá trình cập nhật
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Zammad với quyền truy cập API
- File Excel chứa danh sách người dùng và vai trò cần cập nhật
- API token từ Zammad để xác thực
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Click vào "Import from URL" và nhập URL: https://n8n.io/workflows/2598
3. Hoặc copy nội dung JSON từ link trên và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Download Excel"**:
   - Cập nhật URL của file Excel chứa danh sách người dùng và vai trò
   - Đảm bảo file Excel có định dạng .xlsx

2. **Node "Find Zammad User by email"**:
   - Tạo một HTTP Header Auth với:
     - Name: Authorization
     - Value: Bearer [API token của Zammad]

3. **Node "Update User Roles"**:
   - Tạo một HTTP Header Auth tương tự như node trước
   - Đảm bảo vai trò được cập nhật trong file Excel khớp với các vai trò có sẵn trong Zammad

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra kết quả cập nhật vai trò trong Zammad
3. Bật Active workflow để sử dụng trong thực tế

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi email báo cáo kết quả cập nhật
- Kết hợp với Slack để thông báo khi có lỗi xảy ra
- Tự động hóa quá trình backup file Excel trước khi cập nhật
- Thiết lập lịch chạy định kỳ cho workflow

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình cập nhật vai trò người dùng Zammad từ file Excel, tiết kiệm thời gian và giảm thiểu lỗi. Hãy thử ngay và trải nghiệm sự tiện lợi mà tự động hóa mang lại!