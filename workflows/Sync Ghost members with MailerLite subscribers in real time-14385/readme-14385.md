---
title: "🔄 Tự động đồng bộ thành viên Ghost với người đăng ký MailerLite thời gian thực"
description: "Hướng dẫn tự động hóa đồng bộ thành viên Ghost với người đăng ký MailerLite bằng n8n - giải pháp không cần code, tiết kiệm thời gian và đảm bảo dữ liệu chính xác"
slug: "tu-dong-dong-bo-thanh-vien-ghost-voi-mailerlite-thoi-gian-thuc"
tags: [n8n, automation, no-code, ghost, mailerlite, email-marketing]
keywords: [n8n workflow, tự động hóa, đồng bộ dữ liệu, ghost cms, mailerlite, email marketing]
---

# 🔄 Tự động đồng bộ thành viên Ghost với người đăng ký MailerLite thời gian thực

[Các sếp] có biết rằng việc quản lý danh sách email subscriber thủ công là một công việc tốn thời gian và dễ gây lỗi? Với workflow này, các sếp có thể tự động đồng bộ danh sách thành viên Ghost với danh sách người đăng ký MailerLite ngay khi có thay đổi, mà không cần can thiệp thủ công hay xử lý file CSV.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công khi có thay đổi thành viên
- **Dữ liệu luôn đồng bộ**: Thêm/xóa thành viên Ghost ngay lập tức cập nhật đến MailerLite
- **Tiết kiệm thời gian**: Giảm thiểu công việc quản lý danh sách email thủ công
- **Chính xác cao**: Giảm thiểu lỗi do nhập liệu thủ công
- **Tùy chỉnh linh hoạt**: Bật/tắt đồng bộ cho thêm/xóa thành viên độc lập
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Ghost CMS với quyền quản trị
- Tài khoản MailerLite với quyền tạo/sửa người đăng ký
- API Key của Ghost và MailerLite
- Quyền truy cập vào n8n để import và cấu hình workflow
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/14385](https://n8n.io/workflows/14385)
2. Click vào nút "Import" trên trang workflow
3. Trong n8n Editor, chọn "Import from URL" và dán link workflow
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Cấu hình MailerLite**:
   - Trong node "Update a subscriber" và "Create a subscriber", chọn credentials MailerLite đã tạo
   - Đảm bảo API Key MailerLite có quyền tạo/sửa người đăng ký

2. **Cấu hình Ghost**:
   - Trong node "Delete webhook in Ghost" và "Add webhook in Ghost":
     - Chọn credentials Ghost đã tạo
     - Điền URL API của Ghost (ví dụ: `https://your-ghost-site.com/ghost/api/v3/admin/`)
     - Điền Admin API Key của Ghost

3. **Cấu hình n8n**:
   - Trong node "Get current workflow" và "Update current workflow with sync status":
     - Chọn credentials n8n đã tạo
     - Đảm bảo tài khoản n8n có quyền đọc/ghi workflow

4. **Cấu hình Webhook**:
   - Trong node "Webhook", lưu ý URL webhook (ví dụ: `https://your-n8n-instance.com/webhook/ghost-mailerlite`)
   - Sẽ cần nhập URL này vào form cấu hình Ghost sau này

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node quan trọng, click vào nút "Activate" trên thanh công cụ
2. Test workflow bằng cách gửi một yêu cầu POST mẫu đến webhook URL
3. Kiểm tra log để đảm bảo workflow hoạt động đúng

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**: Thêm node gửi thông báo khi có thay đổi đồng bộ thành công/lỗi
2. **Lưu log hoạt động**: Thêm node lưu log các thay đổi vào Google Sheets hoặc cơ sở dữ liệu
3. **Tự động gửi báo cáo**: Thiết lập gửi báo cáo hàng tuần về số lượng thành viên đồng bộ
4. **Xử lý lỗi nâng cao**: Thêm node xử lý lỗi và gửi cảnh báo khi có vấn đề xảy ra

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc đồng bộ thành viên Ghost với người đăng ký MailerLite một cách tự động và thời gian thực. Với việc cấu hình đơn giản và quản lý linh hoạt, các sếp có thể tiết kiệm đáng kể thời gian và công sức trong việc quản lý danh sách email. Hãy thử ngay và trải nghiệm sự tiện lợi mà tự động hóa mang lại!