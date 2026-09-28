---
title: "🏨 Tự động hóa Phản hồi Khách sạn với Phân tích Cảm xúc GPT-4 & Dịch vụ Khôi phục"
description: "Hướng dẫn tự động hóa quy trình xử lý phản hồi khách hàng khách sạn bằng n8n, giảm 60% đánh giá tiêu cực và tăng trải nghiệm khách hàng"
slug: "tu-dong-hoa-phan-hoi-khach-san-voi-gpt-4"
tags: [n8n, automation, no-code, khách sạn, phân tích cảm xúc]
keywords: [n8n workflow, tự động hóa khách sạn, phân tích cảm xúc khách hàng, dịch vụ khôi phục khách sạn]
---

# 🏨 Tự động hóa Phản hồi Khách sạn với Phân tích Cảm xúc GPT-4 & Dịch vụ Khôi phục

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Giảm 60% đánh giá tiêu cực
- Tự động phân loại và xử lý phản hồi khách hàng
- Tạo ưu đãi khôi phục cá nhân hóa cho khách hàng không hài lòng
- Tích hợp liền mạch với hệ thống quản lý khách sạn (PMS)
- Theo dõi hiệu suất dịch vụ qua bảng tính Google
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail để gửi email thông báo và khôi phục dịch vụ
- Tài khoản Slack để nhận thông báo khẩn cấp
- Tài khoản Google Sheets để lưu trữ dữ liệu phân tích
- Tài khoản Jotform để thu thập phản hồi khách hàng
- API Key từ OpenAI để sử dụng mô hình GPT-4
- Tài khoản PMS (hệ thống quản lý khách sạn) để tạo ticket
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/9811](https://n8n.io/workflows/9811)
2. Nhấn nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Nhấn "Import" để tải workflow vào n8n Editor

Hoặc bạn có thể copy/paste JSON workflow vào n8n Editor bằng cách:
1. Mở n8n Editor
2. Nhấn vào nút "+" ở góc trên bên trái
3. Chọn "Import from JSON"
4. Dán nội dung JSON workflow vào ô nhập liệu
5. Nhấn "Import"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Jotorm Trigger**:
   - Cấu hình credentials cho Jotform API
   - Đảm bảo form Jotform có các trường dữ liệu cần thiết: q3_guestName, q4_guestEmail, q5_roomNumber, q6_stayDates, q7_overallRating, q8_feedbackComments, q9_serviceArea
   - Tạo form Jotform miễn phí [tại đây](https://www.jotform.com/?partner=mediajade)

2. **OpenAI Chat Model**:
   - Cấu hình credentials cho OpenAI API
   - Đảm bảo tài khoản OpenAI có đủ credit để sử dụng mô hình GPT-4
   - Chọn mô hình "gpt-4.1-mini" trong node OpenAI Chat Model

3. **Gmail Nodes**:
   - Cấu hình credentials cho Gmail OAuth2
   - Đảm bảo tài khoản Gmail có quyền gửi email
   - Cấu hình các template email cho các trường hợp khác nhau (thông báo khẩn cấp, email khôi phục dịch vụ, email cảm ơn)

4. **Slack Notification**:
   - Cấu hình URL webhook của Slack
   - Đảm bảo channel Slack được cấu hình đúng để nhận thông báo

5. **Google Sheets**:
   - Cấu hình credentials cho Google Sheets OAuth2 API
   - Tạo bảng tính Google mới và chia sẻ với tài khoản dịch vụ của bạn
   - Cấu hình node "Log to Analytics Sheet" với ID bảng tính và tên sheet chính xác

6. **PMS Ticket Creation**:
   - Cấu hình URL endpoint của PMS API
   - Đảm bảo tài khoản API có quyền tạo ticket
   - Cấu hình các trường dữ liệu cần thiết cho ticket

#### 3. Kích hoạt ⚡️
1. Kiểm tra kết nối với tất cả các dịch vụ bên ngoài
2. Chạy thử với dữ liệu mẫu để đảm bảo workflow hoạt động đúng
3. Kích hoạt workflow bằng cách nhấn nút "Active" ở góc trên bên phải

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp với hệ thống CRM**: Kết nối workflow với hệ thống CRM như HubSpot hoặc Zoho để lưu trữ thông tin khách hàng và lịch sử tương tác
2. **Thêm kênh thông báo**: Kết nối với Telegram hoặc Microsoft Teams để nhận thông báo khẩn cấp
3. **Tự động hóa báo cáo**: Thiết lập báo cáo định kỳ dựa trên dữ liệu trong Google Sheets
4. **Phân tích nâng cao**: Sử dụng các công cụ phân tích dữ liệu như Google Data Studio để tạo báo cáo trực quan

### 📌 Kết luận
Workflow này giúp các sếp khách sạn tự động hóa quy trình xử lý phản hồi khách hàng, giảm thiểu đánh giá tiêu cực và tăng trải nghiệm khách hàng. Bằng cách tích hợp phân tích cảm xúc AI và dịch vụ khôi phục tự động, khách sạn có thể nâng cao chất lượng dịch vụ và xây dựng uy tín thương hiệu. Hãy áp dụng ngay để thấy kết quả ngay lập tức!