---
title: "🚀 Tự động hóa báo cáo Jenkins hàng ngày với Google Sheets và AI Gemini"
description: "Hướng dẫn chi tiết cách tự động hóa báo cáo Jenkins hàng ngày bằng n8n, Google Sheets và AI Gemini. Tiết kiệm thời gian và nâng cao hiệu quả làm việc cho các chuyên viên kiểm thử."
slug: "tu-dong-hoa-bao-cao-jenkins-hang-ngay-voi-google-sheets-va-ai-gemini"
tags: [n8n, automation, no-code, Jenkins, Google Sheets, AI, Gemini]
keywords: [n8n workflow, tự động hóa Jenkins, báo cáo kiểm thử, AI Gemini, Google Sheets]
---

# 🚀 Tự động hóa báo cáo Jenkins hàng ngày với Google Sheets và AI Gemini

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các chuyên viên kiểm thử khi phải tổng hợp báo cáo Jenkins hàng ngày. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm **80% thời gian** tổng hợp báo cáo hàng ngày
- **Tự động hóa hoàn toàn** quy trình báo cáo kiểm thử
- **Nâng cao chất lượng báo cáo** nhờ AI tổng hợp thông minh
- **Hoạt động liên tục 24/7** mà không cần can thiệp
- **Tăng tính chính xác** trong báo cáo kiểm thử
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với Google Sheets API đã kích hoạt
- API Key của Google Gemini
- Quyền truy cập vào Jenkins server của bạn
- Google Sheet đã được cấu hình với các cột: BaseUrl, Environment, FeatureClass, Feature, MailingList
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Google Gemini Chat Model**
   - Chọn credentials cho Google Gemini
   - Đảm bảo API Key đã được kích hoạt và có đủ credit

2. **Retrieve Google Sheet data**
   - Cấu hình Google Sheets credentials
   - Nhập ID của Google Sheet chứa dữ liệu Jenkins
   - Điền tên sheet chứa dữ liệu cần tổng hợp

3. **Perform HTTP Request to Jenkins Server for build numbers**
   - Cấu hình URL cơ bản của Jenkins server
   - Đảm bảo có quyền truy cập vào Jenkins API

4. **Send the test results based on the MailingList**
   - Cấu hình Gmail credentials
   - Điền địa chỉ email gửi báo cáo
   - Đảm bảo đã bật quyền truy cập ứng dụng kém an toàn (nếu cần)

5. **Trigger workflow daily on set time**
   - Thiết lập thời gian chạy hàng ngày (ví dụ: 8:00 AM)
   - Chọn múi giờ phù hợp với địa điểm của bạn

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Teams để nhận thông báo tức thì
- Lưu log báo cáo vào Google Drive cho việc theo dõi lâu dài
- Thiết lập báo cáo định kỳ hàng tuần/tháng
- Tích hợp với các công cụ báo cáo khác như TestRail

### 📌 Kết luận
Workflow này giúp các chuyên viên kiểm thử tiết kiệm thời gian quý giá và nâng cao chất lượng báo cáo kiểm thử nhờ sự kết hợp hoàn hảo giữa tự động hóa và trí tuệ nhân tạo. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của đội ngũ kiểm thử!