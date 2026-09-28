---
title: "💰 Tự Động Hóa Theo Dõi Hóa Đơn Trễ Hạn Với Tiếng Nói Thông Minh - Google Sheets + Email (N8N)"
description: "Giải pháp tự động hóa hoàn toàn không code giúp các sếp theo dõi, tính toán và gửi lời nhắc thanh toán hóa đơn trễ hạn với các giọng điệu cá nhân hóa, tiết kiệm thời gian và tối ưu hóa doanh thu."
slug: "tu-dong-hoa-theo-doi-hoa-don-tre-han-google-sheets-email"
tags: [n8n, automation, invoice-processing, google-sheets, email-automation, no-code]
keywords: [tự động hóa hóa đơn trễ hạn, n8n workflow, theo dõi hóa đơn không code, gửi lời nhắc thanh toán tự động, google sheets + email]
---

# 🚀 **Tự Động Hóa Theo Dõi Hóa Đơn Trễ Hạn Với Tiếng Nói Thông Minh**

### **Nỗi Đau Của Các Sếp**
Các sếp freelancer, công ty tư vấn, hoặc doanh nghiệp thường phải mất thời gian quý báu để theo dõi hóa đơn chưa được thanh toán, tính toán ngày quá hạn (Days Past Due - DPD), và gửi lời nhắc một cách thủ công. Điều này không chỉ tốn thời gian mà còn dễ dẫn đến:
- **Thông điệp không nhất quán** (từ quá nhẹ nhàng đến quá hung hăng).
- **Quá hạn lâu** vì quên hoặc không theo dõi kịp thời.
- **Mất doanh thu** do khách hàng không được nhắc kịp thời.

**Giải pháp này tự động hóa toàn bộ quy trình theo dõi hóa đơn, gửi lời nhắc cá nhân hóa với giọng điệu phù hợp dựa trên mức độ quá hạn, giúp các sếp **tiết kiệm thời gian, tăng hiệu quả thu hồi và duy trì mối quan hệ với khách hàng**.**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted) để tránh giới hạn của phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần theo dõi hóa đơn thủ công hàng ngày.
- **Tính toán chính xác**: Tự động tính **Days Past Due (DPD)** và phân loại mức độ quá hạn.
- **Giọng điệu cá nhân hóa**: Lời nhắc **nhẹ nhàng** cho hóa đơn quá hạn 1-3 ngày, **chuyên nghiệp** cho 4-7 ngày, và **cẩn trọng** cho quá 7 ngày.
- **Hoạt động liên tục**: Cron Trigger chạy hàng ngày, không phụ thuộc vào người dùng.
- **Dễ mở rộng**: Có thể kết nối với **WhatsApp, Slack, Notion** để đa kênh thông báo.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Google Sheets** chứa dữ liệu hóa đơn với các cột bắt buộc:
   - `client_name` (Tên khách hàng)
   - `email` (Email liên hệ)
   - `due_date` (Ngày đến hạn)
   - `invoice_number` (Số hóa đơn)
   - `status` (Trạng thái: "Paid" hoặc "Unpaid")
   *(Tham khảo mẫu [Google Sheets Invoice Template](https://docs.google.com/spreadsheets/d/1XYZ/edit))*

2. **Tài khoản Email** để gửi lời nhắc:
   - **SMTP** (ví dụ: Gmail, Outlook) hoặc **Gmail API** (nếu sử dụng Gmail).
   - **Credentials** cho node `emailSend` (tên miền, mật khẩu ứng dụng, port...).

3. **API Key Google Sheets OAuth2** (để node `googleSheets` có quyền đọc dữ liệu).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/6192](https://n8n.io/workflows/6192) và import vào **n8n Editor**.
- **Copy/paste JSON** từ link trên vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này gồm **6 node chính**, các sếp cần chú ý cấu hình sau:

##### **A. Node `Daily Trigger` (Cron)**
- **Cấu hình**: Chọn `0 0 * * *` (chạy hàng ngày lúc 00:00).
- **Lưu ý**: Nếu muốn chạy vào giờ khác, chỉnh sửa biểu thức cron (ví dụ: `0 9 * * *` để chạy lúc 9h sáng).

##### **B. Node `Load Invoices` (Google Sheets)**
- **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước khi import).
- **Sheet ID**: Thay thế `YOUR_SHEET_ID` bằng **ID của Google Sheet** của các sếp (tìm trong URL: `https://docs.google.com/spreadsheets/d/[ID]/edit`).
- **Range**: Đặt là `Sheet1!A:Z` (hoặc tên sheet cụ thể nếu khác).

##### **C. Node `Filter Overdue Invoices` (Function)**
- **Code mặc định** đã phân loại hóa đơn quá hạn (`status = "Unpaid"` và `due_date < today`).
- **Lưu ý**: Nếu dữ liệu có cấu trúc khác, các sếp cần chỉnh sửa logic trong **Function Code** (mở node này và chỉnh sửa phần `javascript`).

##### **D. Node `Calculate DPD` (Function)**
- **Logic**: Tính số ngày quá hạn (`DPD = today - due_date`).
- **Lưu ý**: Nếu cột `due_date` là dạng `text` (ví dụ: "2024-05-15"), cần chuyển thành `date` trước khi tính toán.

##### **E. Node `Generate Message` (Function)**
- **Tiếng nói cá nhân hóa**:
  - **1-3 ngày quá hạn**: Tôn trọng, nhẹ nhàng.
  - **4-7 ngày quá hạn**: Chuyên nghiệp, nhắc nhở.
  - **>7 ngày quá hạn**: Cẩn trọng, đề xuất giải pháp.
- **Lưu ý**: Các sếp có thể **chỉnh sửa template** trong Function Code để phù hợp với brand của mình.

##### **F. Node `Send Email` (EmailSend)**
- **Credentials**: Chọn tài khoản email đã cấu hình (ví dụ: Gmail SMTP).
- **From Email**: Điền email gửi (ví dụ: `billing@companyname.com`).
- **Subject**: Thay thế bằng tiêu đề phù hợp (ví dụ: `Lời nhắc thanh toán hóa đơn #{{$node["Load Invoices"].json()["invoice_number"]}}`).
- **HTML Content**: Sử dụng nội dung từ node `Generate Message`.

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy node `Daily Trigger` và kiểm tra:
     - Dữ liệu hóa đơn được tải từ Google Sheets.
     - Hóa đơn quá hạn được lọc và tính DPD.
     - Email mẫu được gửi thành công.
2. **Bật Active** workflow sau khi kiểm tra xong.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với WhatsApp/Slack**:
   - Thêm node `whatsappSend` hoặc `slackSend` sau `Send Email` để gửi thông báo đa kênh.
   - Ví dụ: Gửi email cho khách hàng và thông báo nội bộ trên Slack.

2. **Lưu Log Theo Dõi**:
   - Thêm node `googleSheets` sau `Send Email` để ghi lại lịch sử lời nhắc vào sheet mới (cột: `follow_up_date`, `message_sent`).

3. **Báo Cáo Định Kỳ**:
   - Sử dụng node `googleSheets` để tạo **báo cáo tổng hợp** hóa đơn quá hạn hàng tuần/tháng, gửi cho bộ phận tài chính.

4. **Hỗ Trợ Penalty**:
   - Thêm logic trong node `Generate Message` để **giảm giá** hoặc **áp dụng phí trễ** sau 14 ngày quá hạn.

5. **Gửi PDF Hóa Đơn**:
   - Kết nối với node `googleDrive` để tự động gửi **bản PDF hóa đơn** kèm theo email nhắc nhở.

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc theo dõi hóa đơn thủ công, đồng thời **tăng cường hiệu quả thu hồi** bằng cách gửi lời nhắc **cá nhân hóa và chuyên nghiệp**. Với **n8n Self-hosted**, các sếp có thể **yên tâm** workflow chạy 24/7 mà không phụ thuộc vào phiên bản miễn phí.

**Hành động ngay hôm nay**:
1. **Cài đặt n8n trên VPS** (sử dụng mã giảm giá **VPSN8N**).
2. **Import workflow** và **cấu hình dữ liệu**.
3. **Bật Active** và **theo dõi kết quả**!

**Cần hỗ trợ?** Đăng ký tại [n8n Community](https://community.n8n.io/) hoặc liên hệ với **Bheta Maranatha** (tác giả workflow).

---