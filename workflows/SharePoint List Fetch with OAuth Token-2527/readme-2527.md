---
title: "🚀 Tự động lấy dữ liệu từ SharePoint List với OAuth Token - Workflow n8n"
description: "Hướng dẫn tự động hóa việc lấy dữ liệu từ SharePoint List bằng workflow n8n với OAuth Token, tiết kiệm thời gian và nâng cao hiệu suất làm việc."
slug: "tu-dong-lay-du-lieu-sharepoint-list-oauth-token"
tags: [n8n, automation, no-code, sharepoint, oauth]
keywords: [n8n workflow, tự động hóa, sharepoint, oauth token, sharepoint list]
---

# 🚀 Tự động lấy dữ liệu từ SharePoint List với OAuth Token - Workflow n8n

[Các sếp đang làm việc với SharePoint List chắc hẳn đã gặp khó khăn khi phải lấy dữ liệu thủ công từ các danh sách dài, đặc biệt là khi cần cập nhật thường xuyên. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình lấy dữ liệu từ SharePoint List bằng OAuth Token, giúp tiết kiệm thời gian và nâng cao hiệu suất làm việc.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa việc lấy dữ liệu từ SharePoint List, không cần phải làm thủ công.
- Tăng hiệu suất: Dữ liệu được cập nhật tự động theo lịch trình đã đặt.
- Bảo mật: Sử dụng OAuth Token để đảm bảo tính bảo mật cho dữ liệu.
- Tích hợp dễ dàng: Dữ liệu có thể được sử dụng cho các workflow khác hoặc lưu trữ trong các hệ thống khác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản SharePoint với quyền truy cập vào danh sách cần lấy dữ liệu.
- Thông tin xác thực OAuth Token bao gồm:
  - `tenant_id`
  - `client_id`
  - `client_secret`
- URL của SharePoint List cần lấy dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và nhập URL sau: [https://n8n.io/workflows/2527](https://n8n.io/workflows/2527).
3. Hoặc, tải file JSON từ link trên và import vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Generate OAuth Token"**:
   - Cấu hình các tham số sau:
     - `tenant_id`: ID của tenant SharePoint.
     - `client_id`: ID của client OAuth.
     - `client_secret`: Secret của client OAuth.
   - Lưu ý: Không bao giờ hard code các giá trị này trong workflow. Luôn lưu trữ chúng trong các vault bảo mật như HashiCorp hoặc GCP Secret Manager.

2. **Node "Fetch SharePoint List"**:
   - Cấu hình các tham số sau:
     - `URL`: URL của SharePoint List cần lấy dữ liệu.
     - `Authentication`: Chọn "OAuth2" và sử dụng token đã được tạo từ node "Generate OAuth Token".

3. **Node "Schedule Trigger"**:
   - Cấu hình lịch trình để workflow chạy tự động theo nhu cầu của các sếp.

4. **Node "setTenant"**:
   - Cấu hình các tham số cần thiết để thiết lập tenant cho workflow.

#### 3. Kích hoạt ⚡️
1. Nhấn vào nút "Execute Workflow" để kiểm tra workflow chạy đúng hay không.
2. Kiểm tra dữ liệu đầu ra để đảm bảo rằng dữ liệu từ SharePoint List đã được lấy đúng.
3. Nếu mọi thứ đều ổn, nhấn vào nút "Activate Workflow" để kích hoạt workflow và chạy tự động theo lịch trình đã đặt.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với các workflow khác để tự động hóa các tác vụ khác như gửi email, lưu dữ liệu vào Google Sheets, hoặc tích hợp với các hệ thống khác.
- Sử dụng các vault bảo mật để lưu trữ các thông tin xác thực OAuth Token.
- Tùy chỉnh lịch trình chạy workflow để phù hợp với nhu cầu cập nhật dữ liệu của các sếp.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc lấy dữ liệu từ SharePoint List một cách dễ dàng và bảo mật. Bằng cách sử dụng OAuth Token và lịch trình chạy tự động, các sếp có thể tiết kiệm thời gian và nâng cao hiệu suất làm việc. Hãy áp dụng ngay workflow này để tối ưu hóa quy trình làm việc của các sếp!