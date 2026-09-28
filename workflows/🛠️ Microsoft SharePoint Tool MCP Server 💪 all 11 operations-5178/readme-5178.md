---
title: "🚀 Tự động hóa Microsoft SharePoint với n8n: 11 thao tác cơ bản"
description: "Hướng dẫn tự động hóa 11 thao tác chính trên Microsoft SharePoint bằng n8n - tiết kiệm thời gian và giảm lỗi thủ công"
slug: "tu-dong-hoa-microsoft-sharepoint-voi-n8n"
tags: [n8n, automation, no-code, microsoft-sharepoint, office-365]
keywords: [n8n workflow, tự động hóa sharepoint, sharepoint automation, n8n sharepoint, office 365 automation]
---

# 🚀 Tự động hóa Microsoft SharePoint với n8n: 11 thao tác cơ bản

[Các sếp đang làm việc với Microsoft SharePoint chắc hẳn đã từng gặp những tình huống này:]

- 😫 Phải nhập liệu thủ công vào danh sách SharePoint hàng ngày
- 😫 Phải tải xuống, chỉnh sửa và tải lên lại các file thường xuyên
- 😫 Phải quản lý nhiều danh sách và thư mục khác nhau
- 😫 Phải xử lý các lỗi nhập liệu tốn thời gian

[Workflow này sẽ giúp các sếp tự động hóa hoàn toàn 11 thao tác cơ bản nhất trên Microsoft SharePoint chỉ trong vài bước đơn giản.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- 🕒 Tiết kiệm 80% thời gian làm việc thủ công
- 📊 Giảm lỗi nhập liệu đáng kể
- 🔄 Tự động hóa 11 thao tác cơ bản nhất của SharePoint
- ⚡️ Hoạt động liên tục 24/7 mà không cần can thiệp
- 📂 Quản lý tập trung các file và danh sách quan trọng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Microsoft 365 với quyền truy cập SharePoint
- API Key cho Microsoft SharePoint (có thể lấy từ Azure AD)
- Danh sách các thư mục và danh sách SharePoint cần quản lý
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/5178)
2. Click vào nút "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON vừa sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình lại các node quan trọng sau:

1. **Microsoft SharePoint Tool MCP Server** (node đầu tiên):
   - Chọn credentials đã được thiết lập với Microsoft SharePoint
   - Điền Site URL của SharePoint site cần quản lý

2. **Các node Microsoft SharePoint Tool khác**:
   - Điền Site URL và List Name cho từng thao tác
   - Cấu hình các tham số cần thiết cho từng thao tác cụ thể:
     - Download file: Điền File Path
     - Update file: Điền File Path và File Content
     - Upload file: Điền File Path và File Content
     - Create item: Điền các trường dữ liệu cần tạo
     - Update item: Điền ID item và các trường dữ liệu cần cập nhật
     - Delete item: Điền ID item cần xóa
     - Get item: Điền ID item cần lấy
     - Get many items: Điền các tham số lọc nếu cần
     - Get list: Điền List Name
     - Get many lists: Điền các tham số lọc nếu cần

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, click vào nút "Execute Workflow" để test
2. Kiểm tra kết quả và điều chỉnh nếu cần
3. Khi đã ổn định, click vào nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Teams**: Thêm node gửi thông báo khi các thao tác hoàn thành
2. **Lập lịch tự động**: Sử dụng node Schedule Trigger để chạy workflow theo lịch
3. **Lưu log hoạt động**: Thêm node lưu log các thao tác vào Google Sheets hoặc Database
4. **Xử lý lỗi tự động**: Thêm node xử lý lỗi và gửi báo cáo khi có lỗi xảy ra

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn 11 thao tác cơ bản nhất trên Microsoft SharePoint, tiết kiệm thời gian đáng kể và giảm lỗi nhập liệu. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của đội ngũ!