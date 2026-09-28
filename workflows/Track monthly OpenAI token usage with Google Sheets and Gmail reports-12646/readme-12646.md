---
title: "📊 Theo dõi sử dụng token OpenAI hàng tháng với Google Sheets và báo cáo Gmail"
description: "Hướng dẫn tự động hóa theo dõi chi tiết sử dụng token OpenAI hàng tháng, tạo báo cáo tự động và gửi qua email - tiết kiệm thời gian và tối ưu hóa chi phí AI"
slug: "theo-doi-su-dung-token-openai-hang-thang"
tags: [n8n, automation, no-code, openai, google-sheets]
keywords: [n8n workflow, tự động hóa, openai token, báo cáo google sheets, gmail automation]
---

# 📊 Theo dõi sử dụng token OpenAI hàng tháng với Google Sheets và báo cáo Gmail

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi quản lý chi phí OpenAI. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 2-3 giờ mỗi tháng cho việc theo dõi thủ công
- Báo cáo chi tiết về sử dụng token OpenAI theo ngày
- Tự động tính toán chi phí theo model và tổng hợp dữ liệu
- Lưu trữ báo cáo định kỳ trong Google Drive
- Nhận báo cáo PDF qua email hàng tháng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI với quyền truy cập API
- Google Sheets template có sẵn với công thức tính toán chi phí
- Tài khoản Google Drive để lưu trữ báo cáo
- Tài khoản Gmail để gửi báo cáo
- API Key OpenAI và các thông tin xác thực tương ứng
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/12646)
2. Click "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, click "Import from Clipboard" và dán JSON

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Fetch OpenAI Usage Data"**:
   - Thêm credentials OpenAI API
   - Thay thế 'your-api-key-id' bằng ID API Key thực tế

2. **Node "Append Data to Google Sheet"**:
   - Thêm credentials Google Sheets OAuth2
   - Cập nhật Spreadsheet ID và tên sheet phù hợp

3. **Node "Create Monthly Report from Template"**:
   - Thêm credentials Google Drive OAuth2
   - Cập nhật File ID của template Google Sheets
   - Thiết lập thư mục đích cho báo cáo mới

4. **Node "Email Report to Stakeholder"**:
   - Thêm credentials Gmail OAuth2
   - Thay thế 'your-email@example.com' bằng địa chỉ email nhận báo cáo

5. **Node "Monthly Report Trigger"**:
   - Thiết lập lịch chạy hàng tháng (mặc định là ngày 5 hàng tháng)

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra kết nối
2. Kiểm tra các file được tạo trong Google Drive
3. Kiểm tra email nhận được báo cáo PDF
4. Bật Active workflow sau khi xác nhận hoạt động ổn định

### ✍️ Mẹo & gợi ý nâng cao
- Thêm cảnh báo khi vượt ngưỡng chi phí bằng cách sử dụng node "IF"
- Kết hợp với Slack để nhận thông báo tức thời
- Tạo báo cáo định kỳ hàng tuần thay vì hàng tháng
- Thêm dự đoán chi phí dựa trên xu hướng sử dụng
- Theo dõi thêm các chỉ số như số lượng yêu cầu trung bình
- Hỗ trợ nhiều loại tiền tệ với tỷ giá chuyển đổi

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc theo dõi và quản lý chi phí sử dụng OpenAI. Bằng cách tự động hóa toàn bộ quy trình từ lấy dữ liệu đến gửi báo cáo, các sếp có thể tập trung vào việc tối ưu hóa sử dụng AI thay vì làm việc thủ công. Hãy thử ngay và nâng cao hiệu quả quản lý tài nguyên AI của bạn!