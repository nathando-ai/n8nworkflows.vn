---
title: "🚀 Tự động đồng bộ hóa các khóa bản địa hóa iOS thiếu với Google Sheets và GitHub PR Placeholders"
description: "Hướng dẫn tự động hóa quy trình đồng bộ các khóa bản địa hóa iOS thiếu với Google Sheets và tạo pull request trên GitHub bằng n8n"
slug: "tu-dong-dong-bo-khoa-ban-dia-hoa-ios-thieu-voi-google-sheets-va-github-pr-placeholders"
tags: [n8n, automation, no-code, iOS, localization, Google Sheets, GitHub]
keywords: [n8n workflow, tự động hóa, đồng bộ hóa iOS, localization, Google Sheets, GitHub PR]
---

# 🚀 Tự động đồng bộ hóa các khóa bản địa hóa iOS thiếu với Google Sheets và GitHub PR Placeholders

[Các sếp] có biết rằng việc quản lý các khóa bản địa hóa iOS là một công việc tẻ nhạt và dễ gây lỗi? Với workflow này, các sếp có thể tự động hóa quy trình đồng bộ các khóa bản địa hóa thiếu với Google Sheets và tạo pull request trên GitHub một cách nhanh chóng và chính xác.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa quy trình đồng bộ các khóa bản địa hóa thiếu.
- Chính xác: Giảm thiểu lỗi do thủ công.
- Cá nhân hóa: Tùy chỉnh các khóa bản địa hóa theo nhu cầu.
- Hoạt động liên tục: Workflow chạy tự động 24/7.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets.
- Tài khoản GitHub với quyền truy cập vào repository.
- API keys cho Google Sheets và GitHub.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL".
3. Dán link sau vào ô nhập liệu: `https://n8n.io/workflows/7577`.
4. Nhấn "Import".

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Webhook**:
   - Thay đổi `path` trong node Webhook để phù hợp với nhu cầu của các sếp.
   - Ví dụ: `path: "new-pathss"`.

2. **Config**:
   - Cấu hình các biến môi trường cần thiết trong node Config.

3. **Process File Tree**:
   - Chỉnh sửa mã trong node Process File Tree để xử lý cây tệp theo nhu cầu.

4. **Get Source File**:
   - Cấu hình credentials cho GitHub API.
   - Thay đổi URL để lấy tệp nguồn từ repository GitHub.

5. **Find Missing Keys**:
   - Chỉnh sửa mã trong node Find Missing Keys để tìm các khóa thiếu.

6. **Google Sheets**:
   - Cấu hình credentials cho Google Sheets OAuth2 API.
   - Thay đổi `spreadsheetId` và `range` để chỉ định bảng tính và phạm vi cần cập nhật.

7. **Get GitHub Tree**:
   - Cấu hình credentials cho GitHub API.
   - Thay đổi URL để lấy cây tệp từ repository GitHub.

8. **Merge**:
   - Cấu hình node Merge để hợp nhất dữ liệu từ các node trước đó.

9. **Edit Fields**:
   - Cấu hình các trường cần chỉnh sửa trong node Edit Fields.

10. **HTTP Request**:
    - Cấu hình node HTTP Request để gửi yêu cầu đến GitHub API.

11. **Code**:
    - Chỉnh sửa mã trong node Code để xử lý dữ liệu theo nhu cầu.

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu.
2. Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi workflow hoàn thành.
- Lưu log các hoạt động vào Google Sheets để theo dõi.
- Gửi báo cáo định kỳ về trạng thái của các khóa bản địa hóa.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình đồng bộ các khóa bản địa hóa iOS thiếu với Google Sheets và tạo pull request trên GitHub một cách nhanh chóng và chính xác. Hãy áp dụng ngay để tiết kiệm thời gian và giảm thiểu lỗi!