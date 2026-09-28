---
title: "🚀 Theo dõi thay đổi hồ sơ LinkedIn với Google Sheets & Thông báo Slack"
description: "Tự động theo dõi thay đổi hồ sơ LinkedIn của khách hàng tiềm năng, cập nhật Google Sheets và nhận thông báo Slack ngay lập tức khi có thay đổi."
slug: "theo-doi-thay-doi-ho-so-linkedin-voi-google-sheets-slack"
tags: [n8n, automation, no-code, sales, linkedin]
keywords: [n8n workflow, tự động hóa, theo dõi linkedin, google sheets, slack notifications]
---

# 🚀 Theo dõi thay đổi hồ sơ LinkedIn với Google Sheets & Thông báo Slack

[Các sếp đang làm việc với khách hàng tiềm năng trên LinkedIn chắc hẳn đã gặp khó khăn khi phải theo dõi thủ công các thay đổi trên hồ sơ của họ. Từ việc cập nhật thông tin cá nhân đến thay đổi kinh nghiệm làm việc, việc theo dõi thủ công không chỉ tốn thời gian mà còn dễ bỏ sót những cơ hội quan trọng. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quá trình theo dõi, cập nhật và thông báo thay đổi một cách nhanh chóng và chính xác.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động theo dõi thay đổi hồ sơ LinkedIn mà không cần can thiệp thủ công.
- **Chính xác cao**: Không bỏ sót bất kỳ thay đổi nào nhờ vào quá trình tự động hóa.
- **Cá nhân hóa**: Nhận thông báo Slack ngay lập tức khi có thay đổi quan trọng.
- **Hoạt động liên tục**: Theo dõi 24/7 mà không cần giám sát.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets đã được thiết lập.
- Tài khoản Slack với quyền truy cập vào kênh thông báo.
- API Key từ [Ghost Genius API](https://www.ghostgenius.fr/) để scrape dữ liệu LinkedIn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấp vào nút "Import from URL" và nhập URL sau: [https://n8n.io/workflows/5052](https://n8n.io/workflows/5052).
3. Hoặc tải file JSON từ [đây](https://n8n.io/workflows/5052) và import vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Read Profiles List"**:
   - Chọn credentials "googleSheetsOAuth2Api".
   - Cấu hình Spreadsheet ID và Sheet Name trong Google Sheets.

2. **Node "Scrape New Profiles" và "Scrape Current Data"**:
   - Chọn credentials "httpHeaderAuth".
   - Cấu hình URL và headers cho API Ghost Genius.

3. **Node "Alert First Name", "Alert Last Name",... và các node Slack khác**:
   - Chọn credentials "slackOAuth2Api".
   - Cấu hình Channel ID và thông điệp cần gửi.

4. **Node "Update First Name", "Update Last Name",... và các node Google Sheets khác**:
   - Chọn credentials "googleSheetsOAuth2Api".
   - Cấu hình Spreadsheet ID và Sheet Name trong Google Sheets.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
- Bật Active workflow để bắt đầu theo dõi thay đổi.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack**: Thêm các thông báo Slack cho các thay đổi khác như "Open to Work" hoặc "Hiring Status".
- **Lưu log**: Thêm node để lưu log các thay đổi vào Google Sheets hoặc cơ sở dữ liệu khác.
- **Gửi báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo tổng hợp các thay đổi hàng tuần.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình theo dõi thay đổi hồ sơ LinkedIn, cập nhật Google Sheets và thông báo Slack ngay lập tức. Với việc áp dụng workflow này, các sếp có thể tiết kiệm thời gian, đảm bảo không bỏ sót bất kỳ thay đổi quan trọng nào và duy trì sự liên tục trong quá trình theo dõi khách hàng tiềm năng. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của mình!