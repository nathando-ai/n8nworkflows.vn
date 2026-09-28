---
title: "🔄 Cập nhật tất cả vai trò Zammad về giá trị mặc định"
description: "Hướng dẫn tự động hóa cập nhật vai trò người dùng Zammad về giá trị mặc định bằng n8n, tiết kiệm thời gian và đảm bảo tính nhất quán trong quản lý hỗ trợ khách hàng."
slug: "cap-nhat-vai-tro-zammad-ve-gia-tri-mac-dinh"
tags: [n8n, automation, no-code, zammad, support]
keywords: [n8n workflow, tự động hóa, zammad, quản lý vai trò, hỗ trợ khách hàng]
---

# 🔄 Cập nhật tất cả vai trò Zammad về giá trị mặc định

[Các sếp quản lý hệ thống hỗ trợ khách hàng thường gặp khó khăn khi phải cập nhật vai trò người dùng Zammad thủ công, đặc biệt khi có nhiều người dùng và vai trò phức tạp. Workflow này sẽ giúp các sếp tự động hóa quy trình này một cách hoàn toàn không cần code, đảm bảo tính nhất quán và tiết kiệm thời gian đáng kể.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động cập nhật vai trò người dùng Zammad về giá trị mặc định một cách nhanh chóng và chính xác.
- Giảm thiểu lỗi do thao tác thủ công.
- Tiết kiệm thời gian đáng kể trong việc quản lý vai trò người dùng.
- Đảm bảo tính nhất quán trong quản lý hỗ trợ khách hàng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Zammad với quyền truy cập API.
- API Key của Zammad để cấu hình credentials trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/2597).
2. Copy toàn bộ JSON workflow.
3. Trong n8n Editor, nhấn vào "Import from Clipboard" và dán JSON đã copy.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get all Users"**:
   - Cấu hình credentials là `zammadTokenAuthApi`.
   - Đảm bảo API Key của Zammad đã được nhập chính xác.

2. **Node "Get all Roles"**:
   - Cấu hình URL API của Zammad để lấy danh sách vai trò.
   - Ví dụ: `https://your-zammad-instance.com/api/v1/roles`.

3. **Node "Update Users to default Role(s)"**:
   - Cấu hình URL API của Zammad để cập nhật vai trò người dùng.
   - Ví dụ: `https://your-zammad-instance.com/api/v1/users/{{$node["Get all Users"].json["id"]}}`.

#### 3. Kích hoạt ⚡️
1. Nhấn vào nút "Test workflow" để kiểm tra dữ liệu mẫu.
2. Sau khi kiểm tra thành công, nhấn vào nút "Active workflow" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để thông báo khi workflow hoàn thành cập nhật.
- Lưu log cập nhật vào Google Sheets để theo dõi lịch sử thay đổi.
- Tự động gửi báo cáo định kỳ về các thay đổi vai trò người dùng.

### 📌 Kết luận
Workflow này giúp các sếp quản lý vai trò người dùng Zammad một cách tự động, tiết kiệm thời gian và đảm bảo tính nhất quán. Hãy áp dụng ngay để nâng cao hiệu quả quản lý hỗ trợ khách hàng!