---
title: "🔒 Tự Động Hóa Báo Cáo Kiểm Tra An Toàn Tuần Kế (Gmail) - Giải Pháp SecOps Cho Doanh Nghiệp"
description: "Workflow tự động hóa kiểm tra an toàn tuần kế cho hệ thống n8n, gửi báo cáo chi tiết qua Gmail hàng tuần với phân tích rủi ro, trạng thái thực thi và đề xuất cải thiện. Giúp các sếp quản lý an toàn IT một cách hiệu quả, tiết kiệm thời gian và giảm thiểu lỗ hổng."
slug: "tu-dong-hoa-bao-cao-kiem-tra-an-toan-tuan-ke"
tags: [n8n, automation, secops, no-code, an-toan-it]
keywords: [n8n workflow secops, tự động hóa báo cáo an toàn, kiểm tra an toàn hệ thống n8n, gửi báo cáo email tự động, tự động hóa IT]
---

# 🚀 **Tự Động Hóa Báo Cáo Kiểm Tra An Toàn Tuần Kế Cho Hệ Thống n8n (Gửi qua Gmail)**

### **Giải Pháp Cho Nỗi Đau Của Các Sếp**
Quản lý an toàn hệ thống IT là một nhiệm vụ phức tạp, đòi hỏi sự chú ý liên tục và phân tích chi tiết. Các sếp thường phải:
- **Làm thủ công** kiểm tra các workflow, credentials và thiết lập an toàn hàng tuần.
- **Phải nhớ** gửi báo cáo cho team hoặc quản lý, dễ bị bỏ quên hoặc trễ hạn.
- **Không có tầm nhìn toàn cảnh** về rủi ro an toàn, dẫn đến các lỗ hổng không được phát hiện kịp thời.
- **Tốn thời gian** để tổng hợp dữ liệu từ nhiều nguồn khác nhau.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa hoàn toàn** quá trình kiểm tra an toàn hàng tuần.
✅ **Gửi báo cáo chi tiết qua email** với phân tích rủi ro, trạng thái thực thi và đề xuất cải thiện.
✅ **Hỗ trợ hai ngôn ngữ** (Tiếng Việt và Tiếng Anh) cho sự linh hoạt.
✅ **Chỉ cần cấu hình 1 lần**, sau đó hệ thống hoạt động tự động mỗi tuần.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và độ tin cậy cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải kiểm tra thủ công hàng tuần, tự động hóa hoàn toàn.
- **Báo cáo chi tiết và chuyên nghiệp**: Phân tích rủi ro, trạng thái thực thi, và đề xuất cải thiện được gửi qua email hàng tuần.
- **Tầm nhìn toàn cảnh về an toàn**: Xem được tất cả các credentials, nodes nguy hiểm và thiết lập an toàn của hệ thống.
- **Hoạt động liên tục**: Báo cáo được gửi tự động vào mỗi thứ Hai lúc 6h sáng (có thể điều chỉnh).
- **Hỗ trợ đa ngôn ngữ**: Chọn giữa Tiếng Anh (EN) hoặc Tiếng Pháp (FR) để phù hợp với nhu cầu của team.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** để gửi báo cáo (cần cấu hình OAuth2).
2. **API Key của n8n** để truy cập dữ liệu hệ thống.
3. **Thông tin cấu hình cơ bản**:
   - Email nhận báo cáo (`email_to`).
   - Tên dự án (`project_name`).
   - URL server n8n (không có dấu `/` cuối).
   - Ngôn ngữ báo cáo (`EN` hoặc `FR`).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io/workflows/10112](https://n8n.io/workflows/10112) để tải file JSON.
2. Trong n8n Editor, nhấn **Import** và chọn file JSON tải xuống.
3. Hoặc copy toàn bộ JSON và paste vào **Import Workflow** trong menu.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **9 node** chính, các sếp cần chú ý cấu hình các node sau:

##### **🔹 Node 1: Schedule Trigger (Weekly)**
- **Mô tả**: Khởi động workflow hàng tuần vào **thứ Hai lúc 6h sáng**.
- **Lưu ý**:
  - Thay đổi lịch trình nếu cần (ví dụ: hàng ngày, hàng tháng).
  - Cấu hình trong **Node Settings** của node này.

##### **🔹 Node 2: Set Config Variables**
- **Mô tả**: Cấu hình biến môi trường cho workflow.
- **Tham số cần điền**:
  ```yaml
  email_to: your.email@domain.com       # Email nhận báo cáo
  project_name: Your-Project-Name      # Tên dự án
  server_url: https://n8n.yourdomain.com # URL server (không có dấu / cuối)
  Language: "EN" or "FR"               # Chọn ngôn ngữ báo cáo
  ```
- **Lưu ý**:
  - **Không có dấu `/` cuối** trong `server_url`.
  - Ngôn ngữ phải là `"EN"` hoặc `"FR"` (in hoa).

##### **🔹 Node 3: Generate a Security Audit**
- **Mô tả**: Gọi API của n8n để tạo báo cáo kiểm tra an toàn.
- **Yêu cầu**:
  - **Tạo API Key** trong **Settings → API** của n8n.
  - Thêm **credentials** `n8nApi` vào node này.
- **Lưu ý**:
  - API Key phải có quyền **audit access**.

##### **🔹 Node 4: Filter Duplicate WorkflowID**
- **Mô tả**: Lọc bỏ các workflow trùng lặp trong kết quả kiểm tra.
- **Lưu ý**:
  - Node này **không cần cấu hình**, hoạt động tự động.

##### **🔹 Node 5: Get Last Executions**
- **Mô tả**: Lấy trạng thái thực thi gần nhất của các workflow.
- **Yêu cầu**:
  - Sử dụng **cùng API Key** như Node 3 (`n8nApi`).
- **Lưu ý**:
  - Các workflow phải được thực thi ít nhất **1 lần** để lấy được trạng thái.

##### **🔹 Node 6: If Language**
- **Mô tả**: Chuyển hướng đến node định dạng báo cáo theo ngôn ngữ (`FR` hoặc `EN`).
- **Lưu ý**:
  - Node này **không cần cấu hình**, tự động chuyển hướng dựa trên biến `Language`.

##### **🔹 Node 7: Format Audit Report - FR/EN**
- **Mô tả**: Định dạng báo cáo thành **Markdown** và **HTML** cho email.
- **Nội dung báo cáo bao gồm**:
  - Tổng số credentials và nodes nguy hiểm.
  - Phân tích rủi ro với **màu sắc** (🟩 Low, 🟧 Moderate, 🟥 High).
  - Link trực tiếp đến các workflow.
- **Lưu ý**:
  - Node này **không cần cấu hình**, tự động tạo báo cáo.

##### **🔹 Node 8: Send Gmail (HTML)**
- **Mô tả**: Gửi báo cáo định dạng HTML qua Gmail.
- **Yêu cầu**:
  - **Cấu hình OAuth2** cho Gmail trong **Credentials**.
  - **Enable Gmail API** trong [Google Cloud Console](https://console.cloud.google.com/).
- **Lưu ý**:
  - Email nhận (`email_to`) phải là địa chỉ hợp lệ.
  - Có thể thay thế bằng **SMTP** hoặc **Outlook** nếu cần.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**: Chạy thử với dữ liệu mẫu để kiểm tra cấu hình.
2. **Active Workflow**: Sau khi kiểm tra xong, bật **Active** để workflow chạy tự động hàng tuần.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thay đổi lịch trình**:
   - Mở **Node 1 (Schedule Trigger)** và thay đổi cron expression (ví dụ: `0 6 * * 1` cho thứ Hai hàng tuần).

2. **Cải thiện ngưỡng rủi ro**:
   - Mở **Node 7 (Format Audit Report)** và chỉnh sửa mã JavaScript để thay đổi điều kiện phân loại rủi ro (ví dụ: `if (totalCredentials > 5) { ... }`).

3. **Gửi báo cáo cho nhiều người**:
   - Trong **Node 8 (Send Gmail)**, thay đổi `email_to` thành một danh sách email (ví dụ: `["email1@domain.com", "email2@domain.com"]`).

4. **Lưu log báo cáo**:
   - Thêm **Node Google Sheets** hoặc **Node Notion** sau Node 8 để lưu báo cáo vào một bảng hoặc trang wiki.

5. **Kết hợp với Slack/Telegram**:
   - Thêm **Node Slack** hoặc **Node Telegram** để thông báo báo cáo mới được gửi.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa kiểm tra an toàn hệ thống n8n mà không cần viết code. Với chỉ **vài bước cấu hình**, các sếp sẽ nhận được **báo cáo chi tiết hàng tuần** về rủi ro an toàn, trạng thái thực thi và đề xuất cải thiện, giúp quản lý hệ thống một cách hiệu quả và tiết kiệm thời gian.

**Hãy áp dụng ngay và bảo vệ hệ thống của mình một cách thông minh!** 🚀

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/10112)** để bắt đầu ngay!