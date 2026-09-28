---
title: "🚀 Tự động hóa gửi email tiếp cận khách hàng tiềm năng B2B với Google Gemini và Gmail"
description: "Hướng dẫn chi tiết cách tự động hóa gửi email tiếp cận khách hàng tiềm năng B2B bằng công nghệ AI Gemini và n8n. Tiết kiệm thời gian, cá nhân hóa nội dung và theo dõi hiệu quả."
slug: "tu-dong-hoa-gui-email-tiep-can-khach-hang-b2b-voi-gemini-gmail"
tags: [n8n, automation, no-code, lead nurturing, ai]
keywords: [n8n workflow, tự động hóa email, Gemini AI, gửi email tự động, tiếp cận khách hàng B2B]
---

# 🚀 Tự động hóa gửi email tiếp cận khách hàng tiềm năng B2B với Google Gemini và Gmail

[Các sếp đang mệt mỏi với việc phải gửi hàng trăm email tiếp cận khách hàng tiềm năng mỗi ngày. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ tìm kiếm thông tin đến gửi email cá nhân hóa, giúp tiết kiệm thời gian quý giá và tăng hiệu quả tiếp cận.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian lên tới 80% so với gửi email thủ công
- Tăng độ cá nhân hóa nội dung email lên 90%
- Theo dõi trạng thái lead một cách chính xác và tự động
- Hoạt động liên tục 24/7 mà không cần can thiệp
- Giảm tỷ lệ email bị đánh dấu spam nhờ tuân thủ quy tắc gửi
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace (để sử dụng Gmail API)
- API Key của Google Gemini
- Bảng dữ liệu (Data Table) trong n8n để lưu trữ thông tin leads
- Thông tin công ty và sản phẩm dịch vụ của các sếp
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/16031)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link workflow
4. Hoặc copy toàn bộ JSON workflow và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node Schedule Trigger**:
   - Cấu hình thời gian chạy workflow (ví dụ: mỗi 5 phút)

2. **Node Set Context**:
   - Cập nhật thông tin công ty, thông tin người gửi
   - Thêm prompt cho AI để tạo nội dung email phù hợp
   - Thêm ID của bảng dữ liệu leads

3. **Node Get Pending Leads**:
   - Kết nối với bảng dữ liệu leads
   - Đảm bảo cột "status" có giá trị "PENDING"

4. **Node Validate Email Format**:
   - Kiểm tra định dạng email hợp lệ
   - Cấu hình điều kiện để đánh dấu email không hợp lệ

5. **Node Fetch Lead Website**:
   - Cấu hình URL để lấy thông tin từ website lead
   - Thêm headers nếu cần thiết

6. **Node Google Gemini Flash**:
   - Kết nối với API Key của Google Gemini
   - Cấu hình model và các tham số khác

7. **Node Send Outreach Email**:
   - Kết nối với tài khoản Gmail
   - Cấu hình chủ đề email và thông tin người gửi

8. **Node Rate Limit Wait**:
   - Cấu hình thời gian chờ giữa các lần gửi email
   - Đảm bảo không bị chặn bởi dịch vụ email

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra email được gửi có đúng định dạng và nội dung cá nhân hóa
3. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi workflow chạy
- Thêm node lưu log để theo dõi hiệu suất workflow
- Tạo báo cáo định kỳ về hiệu quả của các email đã gửi
- Kết nối với CRM như Hubspot hoặc Pipedrive để quản lý leads
- Tùy chỉnh prompt cho AI để phù hợp với ngành nghề và sản phẩm của các sếp

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình gửi email tiếp cận khách hàng tiềm năng, từ tìm kiếm thông tin đến gửi email cá nhân hóa. Với sự hỗ trợ của Google Gemini AI, các sếp có thể tạo ra nội dung email chất lượng cao mà không cần tốn nhiều thời gian. Hãy áp dụng ngay để tăng hiệu quả tiếp cận khách hàng và tiết kiệm thời gian quý giá!