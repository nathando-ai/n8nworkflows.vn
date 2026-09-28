---
title: "🚀 Tạo Link UTM & QR Code Tự Động + Báo Cáo Google Analytics Định Kỳ"
description: "Tự động hóa hoàn toàn quá trình tạo link UTM, QR code và báo cáo hiệu suất từ Google Analytics - tiết kiệm thời gian và nâng cao hiệu quả marketing"
slug: "tao-link-utm-qr-code-google-analytics"
tags: [n8n, automation, marketing, google-analytics, airtable]
keywords: [n8n workflow, tự động hóa marketing, tạo link UTM, báo cáo analytics, marketing automation]
---

# 🚀 Tạo Link UTM & QR Code Tự Động + Báo Cáo Google Analytics Định Kỳ

[Các sếp marketing] đang gặp khó khăn khi phải tạo thủ công hàng trăm link UTM, quản lý QR code và theo dõi hiệu suất từng chiến dịch. Quá trình này tốn thời gian, dễ xảy ra lỗi và không thể tự động hóa được. Workflow này sẽ giúp các sếp giải quyết hoàn toàn những vấn đề này với giải pháp tự động hóa 100% không cần code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động tạo hàng trăm link UTM với các tham số tùy chỉnh (source, medium, campaign...)
- Tự động lưu trữ link vào Airtable để quản lý tập trung
- Tạo QR code từ link UTM một cách nhanh chóng
- Nhận báo cáo Google Analytics định kỳ về hiệu suất từng chiến dịch
- Tiết kiệm thời gian lên tới 80% cho các công việc lặp lại
- Giảm thiểu lỗi do nhập liệu thủ công
- Theo dõi hiệu suất marketing một cách khoa học và chính xác
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Analytics với quyền truy cập dữ liệu
- Tài khoản Airtable để lưu trữ link UTM
- Tài khoản Gmail để gửi báo cáo
- API Key từ OpenAI (để sử dụng LLM phân tích dữ liệu)
- Tài khoản Google Cloud với quyền tạo QR code
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/2921](https://n8n.io/workflows/2921)
2. Click vào nút "Import" trên trang workflow
3. Copy toàn bộ JSON workflow và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "OpenAI Chat Model1"**:
   - Chọn credentials "openAiApi"
   - Đảm bảo model được chọn là "gpt-4o-mini"

2. **Node "Google Analytics"**:
   - Chọn credentials "googleAnalyticsOAuth2"
   - Cấu hình các view ID và metrics theo nhu cầu báo cáo

3. **Node "Submit UTM Link To Database"**:
   - Chọn credentials "airtableTokenApi"
   - Cấu hình base ID và table name trong Airtable
   - Đảm bảo các trường dữ liệu (Website Link UTM, QR Code URL...) được ánh xạ đúng

4. **Node "Send Summary Report To Marketing Manager"**:
   - Chọn credentials "gmailOAuth2"
   - Cấu hình địa chỉ email nhận báo cáo

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra kết quả:
   - Link UTM được tạo đúng với các tham số
   - Link được lưu vào Airtable
   - QR code được tạo từ link UTM
   - Báo cáo Google Analytics được gửi đúng thời gian
3. Bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack để nhận thông báo khi báo cáo được gửi
2. Lưu log các báo cáo đã gửi để theo dõi lịch sử
3. Tạo báo cáo định kỳ hàng tuần/tháng cho các bộ phận liên quan
4. Kết hợp với Google Sheets để lưu trữ và phân tích dữ liệu dài hạn

### 📌 Kết luận
Workflow này sẽ giúp các sếp marketing tự động hóa hoàn toàn quá trình tạo link UTM, quản lý QR code và theo dõi hiệu suất chiến dịch. Với giải pháp này, các sếp có thể tập trung vào việc phân tích dữ liệu và tối ưu hóa chiến dịch thay vì phải làm thủ công các công việc lặp lại. Hãy áp dụng ngay để nâng cao hiệu quả marketing của doanh nghiệp!