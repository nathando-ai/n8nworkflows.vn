---
title: "🚀 Phân tích Mẫu Phân biệt Giới tại Nơi Làm Việc bằng AI và Glassdoor"
description: "Tự động hóa phân tích dữ liệu đánh giá công ty từ Glassdoor để phát hiện các mẫu phân biệt giới, chủng tộc và các nhóm thiểu số khác. Sử dụng n8n kết hợp ScrapingBee, OpenAI và QuickChart để tạo báo cáo trực quan."
slug: "phan-tich-phan-biet-gioi-tai-noi-lam-viec-bang-ai"
tags: [n8n, automation, no-code, HR, AI, Glassdoor, ScrapingBee, QuickChart]
keywords: [n8n workflow, tự động hóa HR, phân tích dữ liệu nhân sự, phát hiện phân biệt giới, Glassdoor, AI phân tích nhân sự]
---

# 🚀 Phân tích Mẫu Phân biệt Giới tại Nơi Làm Việc bằng AI và Glassdoor

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp HR và chuyên viên tuyển dụng thường phải đối mặt với thách thức quan trọng: phát hiện các mẫu phân biệt giới, chủng tộc và các nhóm thiểu số trong môi trường làm việc. Việc thủ công phân tích hàng trăm đánh giá từ các nền tảng như Glassdoor không chỉ tốn thời gian mà còn dễ bỏ sót các mẫu quan trọng. Workflow này giúp các sếp tự động hóa quy trình này, sử dụng công nghệ AI để phát hiện các mẫu phân biệt và tạo báo cáo trực quan.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa quy trình phân tích dữ liệu từ Glassdoor.
- Chính xác: Sử dụng AI để phát hiện các mẫu phân biệt.
- Cá nhân hóa: Tạo báo cáo trực quan cho từng công ty.
- Hoạt động liên tục: Chạy tự động định kỳ để theo dõi xu hướng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản ScrapingBee (để truy cập dữ liệu từ Glassdoor).
- Tài khoản OpenAI (để sử dụng mô hình AI phân tích dữ liệu).
- Tên công ty cần phân tích (ví dụ: "Twilio").
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from File" và chọn file JSON của workflow.
3. Hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "SET company_name"**:
   - Thay đổi giá trị của biến `company_name` thành tên công ty cần phân tích (ví dụ: "Twilio").

2. **Node "ScrapingBee Search Glassdoor"**:
   - Thêm credentials cho ScrapingBee trong n8n.
   - Đảm bảo tài khoản ScrapingBee có đủ token để chạy workflow.

3. **Node "OpenAI Chat Model1", "OpenAI Chat Model2", "OpenAI Chat Model"**:
   - Thêm credentials cho OpenAI trong n8n.
   - Đảm bảo tài khoản OpenAI có đủ credit để chạy workflow.

4. **Node "Text Analysis of Bias Data"**:
   - Thay đổi prompt nếu cần phân tích các nhóm thiểu số khác.

#### 3. Kích hoạt ⚡️
1. Nhấn vào nút "Test workflow" để chạy dữ liệu mẫu.
2. Kiểm tra kết quả từ các node QuickChart để đảm bảo dữ liệu được hiển thị đúng.
3. Bật Active workflow để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**: Thêm node để gửi báo cáo tự động đến kênh Slack/Telegram.
2. **Lưu log**: Thêm node để lưu log các lần chạy workflow.
3. **Gửi báo cáo định kỳ**: Thiết lập workflow chạy tự động hàng tuần hoặc hàng tháng.
4. **Phân tích thêm**: Thêm các nhóm thiểu số khác vào danh sách phân tích.

### 📌 Kết luận
Workflow này giúp các sếp HR tự động hóa quy trình phân tích dữ liệu đánh giá công ty từ Glassdoor, sử dụng AI để phát hiện các mẫu phân biệt và tạo báo cáo trực quan. Hãy áp dụng ngay để cải thiện môi trường làm việc và đảm bảo quyền lợi của tất cả nhân viên.