---
title: "🚀 Tự động đăng Reels Instagram từ Google Sheets với AI DeepSeek tạo caption"
description: "Hướng dẫn chi tiết cách tự động đăng Reels lên Instagram từ nội dung trong Google Sheets và Google Drive với caption được tạo bởi AI DeepSeek. Giải pháp hoàn toàn không cần code cho người quản lý nội dung và doanh nghiệp."
slug: "tu-dong-dang-reels-instagram-tu-google-sheets-voi-ai-deepseek"
tags: [n8n, automation, social media, ai, google sheets]
keywords: [n8n workflow, tự động hóa Instagram, AI caption, Google Sheets, DeepSeek]
---

# 🚀 Tự động đăng Reels Instagram từ Google Sheets với AI DeepSeek tạo caption

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp đang quản lý nội dung cho Instagram chắc hẳn đã từng gặp tình trạng này: có hàng trăm video chất lượng trong Google Drive nhưng lại không có thời gian để đăng lên. Hoặc có thể các sếp đã cố gắng lên kế hoạch đăng bằng Google Sheets nhưng lại quên hoặc không có thời gian thực hiện. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quá trình từ lấy nội dung đến đăng lên Instagram với caption được tạo bởi AI DeepSeek.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động đăng Reels hàng ngày mà không cần can thiệp thủ công.
- Tăng tương tác: Caption được tạo bởi AI DeepSeek giúp tăng tỷ lệ tương tác lên đến 30%.
- Quản lý nội dung hiệu quả: Theo dõi và quản lý nội dung qua Google Sheets và Airtable.
- Hoạt động liên tục: Workflow chạy tự động mỗi 12 giờ hoặc khi có hàng mới trong Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets và Google Drive.
- Tài khoản Instagram Business với quyền truy cập API.
- API Key của DeepSeek AI.
- Tài khoản Airtable (tùy chọn).
- Server SSH (tùy chọn).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và dán link: https://n8n.io/workflows/13759.
3. Hoặc tải file JSON về và import từ local.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Trigger: New Row in Sheet** và **Trigger: Every 12 Hours**:
   - Cấu hình Google Sheets Trigger để theo dõi bảng chứa danh sách video.
   - Điền ID của Google Sheet và tên của sheet.

2. **Fetch Unposted Videos**:
   - Cấu hình Google Sheets để lấy danh sách video chưa đăng.
   - Điền ID của Google Sheet và tên của sheet.

3. **Download Video from Drive**:
   - Cấu hình Google Drive để tải video về.
   - Điền ID của file video trong Google Drive.

4. **Process Video with FFmpeg**:
   - Cấu hình lệnh FFmpeg để xử lý video.
   - Ví dụ: `ffmpeg -i input.mp4 -vf "drawtext=fontfile=/path/to/font.ttf:text='Your Text':fontcolor=white:fontsize=24:x=(w-text_w)/2:y=(h-text_h)/2" output.mp4`

5. **Upload to Server via SSH**:
   - Cấu hình SSH để upload video lên server.
   - Điền thông tin SSH (host, username, port) và đường dẫn lưu trữ.

6. **Generate Caption with DeepSeek**:
   - Cấu hình DeepSeek Chat Model để tạo caption.
   - Điền API Key của DeepSeek.

7. **Store Caption in Airtable**:
   - Cấu hình Airtable để lưu caption.
   - Điền API Key và ID của bảng trong Airtable.

8. **Publish Reel to Instagram**:
   - Cấu hình Facebook Graph API để đăng Reels.
   - Điền Access Token của Instagram và ID của trang.

9. **Mark as Posted**:
   - Cấu hình Google Sheets để đánh dấu video đã đăng.
   - Điền ID của Google Sheet và tên của sheet.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có lỗi hoặc khi video được đăng thành công.
- Lưu log các hoạt động vào Google Sheets hoặc Airtable để theo dõi hiệu suất.
- Gửi báo cáo hàng tuần về số lượng video đã đăng và tỷ lệ tương tác.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình đăng Reels lên Instagram từ nội dung trong Google Sheets và Google Drive với caption được tạo bởi AI DeepSeek. Các sếp chỉ cần chuẩn bị nội dung và cấu hình một lần, sau đó workflow sẽ chạy tự động mỗi 12 giờ hoặc khi có hàng mới trong Google Sheets. Hãy áp dụng ngay để tiết kiệm thời gian và tăng hiệu suất quản lý nội dung!