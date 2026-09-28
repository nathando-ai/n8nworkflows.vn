---
title: "🚀 Tự động hóa phân tích hồ sơ ứng viên với Thordata + OpenAI GPT-4.1-mini"
description: "Hướng dẫn tự động hóa chuyển đổi hồ sơ ứng viên từ định dạng không cấu trúc sang JSON chuẩn JSON Resume Schema bằng n8n, tiết kiệm 80% thời gian tuyển dụng"
slug: "tu-dong-hoa-phan-tich-ho-so-ung-vien"
tags: [n8n, automation, no-code, hr, ai]
keywords: [n8n workflow, tự động hóa tuyển dụng, phân tích hồ sơ, json resume, openai]
---

# 🚀 Tự động hóa phân tích hồ sơ ứng viên với Thordata + OpenAI GPT-4.1-mini

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp tuyển dụng thường phải đối mặt với hàng trăm hồ sơ ứng viên mỗi ngày, nhưng đa số đều ở định dạng không cấu trúc (PDF, Word, trang web cá nhân...). Việc chuyển đổi thủ công này tốn thời gian, dễ gây sai sót và không thể mở rộng quy mô.

Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình từ:
1. Thu thập hồ sơ từ URL
2. Phân tích thông minh bằng AI
3. Chuyển đổi sang định dạng JSON chuẩn
4. Lưu trữ và quản lý dữ liệu

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm **80% thời gian tuyển dụng** cho các công việc chuyển đổi thủ công
- Tăng độ chính xác lên **95%** nhờ AI phân tích thông minh
- Dữ liệu được cấu trúc chuẩn JSON Resume Schema, tương thích với hầu hết hệ thống ATS hiện đại
- Tự động lưu trữ dữ liệu lên Google Sheets và hệ thống file của công ty
- Hỗ trợ quy mô lớn với khả năng xử lý hàng trăm hồ sơ mỗi ngày
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với quyền truy cập Google Sheets API
- API Key từ OpenAI (đã kích hoạt gpt-4.1-mini)
- API Key từ Thordata Universal API
- Thư mục lưu trữ file JSON trên máy chủ
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/10289](https://n8n.io/workflows/10289)
2. Chọn "Import" và sao chép JSON workflow
3. Trong n8n Editor, chọn "Import from JSON" và dán nội dung đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Set the Input Fields"**:
   - Cấu hình URL của hồ sơ ứng viên cần phân tích
   - Thiết lập các tham số đầu vào khác nếu cần

2. **Node "Perform Thordata Universal API Request"**:
   - Tạo credential mới với API Key từ Thordata
   - Kiểm tra endpoint API có hoạt động hay không

3. **Node "OpenAI Chat Model for Resume Builder"**:
   - Tạo credential mới với API Key từ OpenAI
   - Đảm bảo đã kích hoạt model gpt-4.1-mini
   - Tùy chỉnh prompt nếu cần thay đổi cấu trúc đầu ra

4. **Node "Append or update row in sheet"**:
   - Tạo credential Google Sheets OAuth2
   - Chỉ định ID của Google Sheet và tên sheet cần ghi dữ liệu
   - Thiết lập mapping giữa các trường dữ liệu và cột trong sheet

5. **Node "Write the Structured JSON resume to Disk"**:
   - Thiết lập đường dẫn thư mục lưu trữ file JSON
   - Tùy chỉnh tên file nếu cần (có thể sử dụng biến động từ các trường dữ liệu)

#### 3. Kích hoạt ⚡️
1. Chạy test với một hồ sơ mẫu để kiểm tra toàn bộ quy trình
2. Kiểm tra kết quả trên Google Sheets và thư mục lưu trữ
3. Bật chế độ Active workflow để sử dụng trong thực tế

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp Slack/Teams**: Thêm node gửi thông báo khi có hồ sơ mới được xử lý
2. **Lưu log hoạt động**: Thêm node ghi log các hồ sơ đã xử lý
3. **Xử lý hàng loạt**: Sử dụng node Loop để xử lý nhiều hồ sơ cùng lúc
4. **Báo cáo định kỳ**: Thiết lập workflow gửi báo cáo tổng hợp hàng tuần/tháng

### 📌 Kết luận
Workflow này đã giúp các sếp tuyển dụng tiết kiệm hàng giờ mỗi ngày trong việc xử lý hồ sơ ứng viên. Bằng cách tự động hóa quy trình phân tích thông minh với công nghệ AI, các công ty có thể nâng cao chất lượng tuyển dụng, giảm thiểu rủi ro và tăng tốc độ tuyển dụng lên gấp 4 lần.

Hãy thử ngay và biến đổi cách làm việc của các sếp tuyển dụng! 🚀