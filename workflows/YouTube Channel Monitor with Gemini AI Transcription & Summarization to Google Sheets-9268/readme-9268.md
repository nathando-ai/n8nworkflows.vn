---
title: "🚀 Theo dõi kênh YouTube với AI Gemini tự động ghi âm và tóm tắt lên Google Sheets"
description: "Tự động hóa toàn bộ quy trình theo dõi video YouTube, ghi âm và tóm tắt nội dung bằng AI Gemini, lưu kết quả lên Google Sheets - giải pháp tiết kiệm thời gian 100% không cần code"
slug: "theo-doi-youtube-voi-gemini-google-sheets"
tags: [n8n, automation, no-code, youtube, google-sheets, ai, gemini]
keywords: [n8n workflow, tự động hóa youtube, ghi âm video, tóm tắt nội dung, google sheets, ai gemini]
---

# 🚀 Theo dõi kênh YouTube với AI Gemini tự động ghi âm và tóm tắt lên Google Sheets

[Các sếp đang gặp khó khăn khi phải theo dõi hàng loạt kênh YouTube, ghi âm video và tóm tắt nội dung thủ công. Workflow này sẽ tự động hóa toàn bộ quy trình này với AI Gemini, tiết kiệm thời gian và đảm bảo chính xác 100%.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động theo dõi hàng loạt kênh YouTube
- Ghi âm và tóm tắt nội dung video bằng AI Gemini
- Lưu kết quả lên Google Sheets với cấu trúc dữ liệu rõ ràng
- Tiết kiệm thời gian lên tới 90% so với làm thủ công
- Hoạt động liên tục 24/7 với lịch trình tự động
- Dữ liệu được cập nhật liên tục và chính xác
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với API key cho Google Gemini
- Tài khoản Google với Google Sheets API được kích hoạt
- Danh sách kênh YouTube cần theo dõi (có thể lưu trong Google Sheets)
- API key cho YouTube Data API (nếu cần truy cập thông tin chi tiết)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/9268)
2. Click vào nút "Copy Workflow to Clipboard"
3. Trong n8n Editor, click vào "Import from Clipboard" và dán nội dung đã copy

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Google Gemini Chat Model13**:
   - Chọn credentials cho Google Gemini
   - Đảm bảo API key còn hạn sử dụng

2. **Get row(s) in sheet** và **Get row(s) in sheet1**:
   - Cấu hình Google Sheets credentials
   - Điền chính xác Spreadsheet ID và Sheet Name
   - Đảm bảo tài khoản có quyền truy cập vào bảng tính

3. **RSS Read (youtube channel videos)**:
   - Điền URL kênh YouTube cần theo dõi (hoặc sử dụng node trước đó để lấy danh sách kênh)

4. **Videos Posted in Last X days (change on line 6)**:
   - Chỉnh số ngày theo nhu cầu (ví dụ: 7 để theo dõi video trong 7 ngày qua)

5. **Schedule Trigger**:
   - Cấu hình lịch chạy workflow (ví dụ: hàng ngày lúc 8h sáng)

#### 3. Kích hoạt ⚡️
1. Test run workflow với 1 kênh YouTube mẫu
2. Kiểm tra kết quả trên Google Sheets
3. Sau khi xác nhận hoạt động ổn định, bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack/Telegram để nhận thông báo khi có video mới
2. Thêm node để gửi email báo cáo hàng tuần
3. Lưu log hoạt động để theo dõi hiệu suất workflow
4. Tự động phân loại video theo chủ đề bằng AI

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc theo dõi và phân tích nội dung YouTube. Với khả năng tự động ghi âm, tóm tắt và lưu trữ dữ liệu lên Google Sheets, các sếp có thể tập trung vào phân tích nội dung quan trọng hơn. Hãy thử ngay và nâng cao hiệu quả làm việc của mình!