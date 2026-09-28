---
title: "🚀 Tự động hóa Dịch Phụ Đề SRT với Google Translate - Workflow n8n"
description: "Hướng dẫn chi tiết cách tự động hóa dịch phụ đề SRT sang nhiều ngôn ngữ bằng Google Translate với n8n. Tiết kiệm thời gian và đảm bảo độ chính xác cao."
slug: "tu-dong-hoa-dich-phu-de-srt-voi-google-translate"
tags: [n8n, automation, no-code, google-translate, subtitle]
keywords: [n8n workflow, tự động hóa, dịch phụ đề, google translate, srt]
---

# 🚀 Tự động hóa Dịch Phụ Đề SRT với Google Translate - Workflow n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể khi dịch hàng loạt phụ đề SRT.
- Đảm bảo độ chính xác cao nhờ sử dụng dịch vụ Google Translate.
- Tự động hóa hoàn toàn quy trình dịch phụ đề, giảm thiểu lỗi do làm thủ công.
- Hỗ trợ nhiều ngôn ngữ đích khác nhau.
- Tích hợp dễ dàng với các hệ thống khác thông qua n8n.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với API Google Translate được kích hoạt.
- File phụ đề SRT cần dịch (định dạng .srt).
- Kiến thức cơ bản về n8n và cách cấu hình credentials.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/3620](https://n8n.io/workflows/3620).
3. Hoặc tải file JSON từ link trên và import thủ công vào n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Google Translate Credentials**:
   - Truy cập [Google Cloud Console](https://console.cloud.google.com/) để lấy API key.
   - Tạo credentials mới trong n8n với tên `googleTranslateOAuth2Api`.
   - Nhập API key vào credentials.

2. **Cấu hình ngôn ngữ đích**:
   - Có thể cập nhật form để bao gồm mã ngôn ngữ đích (mà bạn đang dịch sang) bằng cách cập nhật trường dropdown với tùy chọn mới.
   - Hoặc cập nhật tùy chọn ngôn ngữ trong node Google Translate về 'fixed' và chọn ngôn ngữ đích mong muốn. Điều này sẽ bỏ qua tùy chọn form, nhưng là an toàn để làm.

3. **Node "Receive SRT File to Translate"**:
   - Đảm bảo cấu hình form để nhận file SRT đầu vào.

4. **Node "Extract text from Binary File"**:
   - Kiểm tra định dạng file đầu vào có đúng là SRT không.

5. **Node "Google Translate"**:
   - Đảm bảo ngôn ngữ đích được cấu hình đúng.
   - Kiểm tra API key và credentials đã được cấu hình chính xác.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
- Bật Active workflow để bắt đầu dịch phụ đề SRT tự động.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để thông báo khi dịch hoàn thành.
- Lưu log các file đã dịch để theo dõi lịch sử.
- Gửi báo cáo định kỳ về số lượng phụ đề đã dịch và thời gian xử lý.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình dịch phụ đề SRT sang nhiều ngôn ngữ khác nhau với độ chính xác cao. Bằng cách tích hợp với Google Translate và n8n, các sếp có thể tiết kiệm thời gian đáng kể và đảm bảo chất lượng dịch tốt nhất. Hãy áp dụng ngay để nâng cao hiệu suất làm việc!