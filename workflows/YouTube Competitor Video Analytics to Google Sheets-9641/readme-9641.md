---
title: "📊 Tự động hóa phân tích video YouTube của đối thủ sang Google Sheets"
description: "Hướng dẫn tự động hóa 100% không cần code để lấy dữ liệu video YouTube của đối thủ và lưu vào Google Sheets, giúp bạn phân tích thị trường và tối ưu nội dung hiệu quả hơn."
slug: "tu-dong-hoa-phan-tich-video-youtube-doi-thu-sang-google-sheets"
tags: [n8n, automation, no-code, youtube, google-sheets]
keywords: [n8n workflow, tự động hóa, phân tích video youtube, đối thủ, google sheets]
---

# 📊 Tự động hóa phân tích video YouTube của đối thủ sang Google Sheets

[Các sếp] có bao giờ tự hỏi tại sao video của đối thủ lại nhận được hàng triệu lượt xem trong khi video của mình chỉ có vài trăm lượt xem? Với workflow này, các sếp có thể tự động hóa việc lấy dữ liệu video YouTube của đối thủ và lưu vào Google Sheets, giúp phân tích thị trường và tối ưu nội dung hiệu quả hơn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phân tích thị trường**: Xem ngay video nào của đối thủ đang hot, nội dung nào đang được khán giả yêu thích.
- **Tối ưu nội dung**: Hiểu rõ xu hướng của đối thủ để tạo nội dung phù hợp hơn.
- **Theo dõi hiệu suất**: Lưu trữ dữ liệu video của đối thủ theo thời gian để theo dõi xu hướng.
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quá trình mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets API đã được kích hoạt.
- API Key của YouTube Data API (có thể lấy từ [Google Cloud Console](https://console.cloud.google.com/)).
- Tạo một Google Sheet mới để lưu dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/9641](https://n8n.io/workflows/9641).
3. Hoặc tải file JSON từ [đây](https://n8n.io/workflows/9641) và import vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "On form submission1"**:
   - Cấu hình form để nhập tên kênh YouTube của đối thủ.

2. **Node "Set Parameters1"**:
   - Điền API Key của YouTube Data API vào trường `apiKey`.

3. **Node "Append row in sheet1"**:
   - Chọn credentials `googleSheetsOAuth2Api`.
   - Điền `Spreadsheet ID` của Google Sheet mà các sếp muốn lưu dữ liệu.
   - Điền tên sheet trong trường `Sheet Name`.

#### 3. Kích hoạt ⚡️
- Nhấn vào nút "Execute Node" để test workflow với dữ liệu mẫu.
- Sau khi test thành công, nhấn vào nút "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với OpenAI**: Thêm node OpenAI để tự động tóm tắt nội dung của video hot nhất của đối thủ.
- **Thông báo qua Slack/Telegram**: Kết nối với Slack hoặc Telegram để nhận thông báo khi có video mới của đối thủ.
- **Lập lịch chạy định kỳ**: Sử dụng node "Schedule Trigger" để tự động chạy workflow hàng ngày hoặc hàng tuần.
- **Báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo định kỳ qua email hoặc Slack.

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa việc phân tích video YouTube của đối thủ và lưu dữ liệu vào Google Sheets, giúp tối ưu nội dung và tăng hiệu suất marketing. Hãy áp dụng ngay để có được thông tin cạnh tranh chi tiết và chính xác nhất!