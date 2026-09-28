---
title: "🚀 Tự động theo dõi đơn ứng tuyển và chuẩn bị phỏng vấn với Notion và GPT-5-mini"
description: "Hướng dẫn tự động hóa quy trình theo dõi đơn ứng tuyển và chuẩn bị phỏng vấn bằng n8n, Notion và OpenAI. Tiết kiệm thời gian và tối ưu hóa quá trình tìm việc."
slug: "tu-dong-theo-doi-don-ung-tuyen-va-chuan-bi-phong-van"
tags: [n8n, automation, no-code, Notion, OpenAI]
keywords: [n8n workflow, tự động hóa, tìm việc, phỏng vấn, Notion, OpenAI]
---

# 🚀 Tự động theo dõi đơn ứng tuyển và chuẩn bị phỏng vấn với Notion và GPT-5-mini

[Các sếp đang tìm việc thường phải đối mặt với hàng tá email xác nhận ứng tuyển, các trang web công ty và các cuộc phỏng vấn. Quá trình này không chỉ tốn thời gian mà còn dễ gây nhầm lẫn. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình từ nhận đơn đến chuẩn bị phỏng vấn, giúp các sếp tập trung vào những việc quan trọng hơn.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động xử lý các email xác nhận và trích xuất thông tin từ các trang web công ty.
- **Chuẩn bị phỏng vấn hiệu quả**: AI tạo ra các câu hỏi phỏng vấn và điểm nhấn cá nhân hóa.
- **Theo dõi đơn ứng tuyển**: Lưu trữ và quản lý tất cả các đơn ứng tuyển trong Notion với các nhắc nhở theo lịch trình.
- **Tăng cường hiệu suất**: Giảm thiểu công việc thủ công và tập trung vào các hoạt động quan trọng hơn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Notion**: Tạo một cơ sở dữ liệu với các thuộc tính yêu cầu (xem mẫu bên dưới).
- **API Key OpenAI**: Cấu hình API key cho OpenAI.
- **Tài khoản Gmail**: Cấu hình để nhận các email xác nhận ứng tuyển.
- **Slack (tùy chọn)**: Để nhận các nhắc nhở theo lịch trình.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/13104](https://n8n.io/workflows/13104).
2. Nhấn vào nút "Import" và sao chép JSON của workflow.
3. Trong n8n Editor, nhấn vào "Import from Clipboard" và dán JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Receive Job Application Form"**:
   - Đảm bảo cấu hình webhook với đường dẫn `job-application` và phương thức HTTP `POST`.

2. **Node "Check for Forwarded Applications"**:
   - Cấu hình tài khoản Gmail để nhận các email xác nhận ứng tuyển.

3. **Node "Extract Job Details with AI"**:
   - Cấu hình tài khoản OpenAI và cung cấp prompt để trích xuất thông tin từ URL công việc.

4. **Node "Generate Interview Prep Materials"**:
   - Cập nhật prompt để tạo ra các câu hỏi phỏng vấn và điểm nhấn cá nhân hóa.

5. **Node "Save Application to Notion"**:
   - Cấu hình tài khoản Notion và đảm bảo cơ sở dữ liệu có các thuộc tính yêu cầu (Company, Role, Status, Applied Date, Salary Range, Job URL, Company Research, Interview Prep, Follow Up Date, Notes).

6. **Node "Daily Follow-up Check"**:
   - Cấu hình lịch trình hàng ngày để kiểm tra các đơn ứng tuyển cần theo dõi.

#### 3. Kích hoạt ⚡️
1. **Test run dữ liệu mẫu**:
   - Gửi một URL công việc mẫu để kiểm tra quy trình trích xuất và tạo nội dung phỏng vấn.
2. **Bật Active workflow**:
   - Sau khi kiểm tra, bật workflow để bắt đầu tự động hóa quy trình.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack**: Cấu hình node "Send Slack Reminder" để nhận các nhắc nhở theo lịch trình.
- **Lưu log**: Thêm node để lưu log các hoạt động để theo dõi hiệu suất của workflow.
- **Gửi báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo hàng tuần về tiến độ đơn ứng tuyển.
- **Tích hợp với các công cụ khác**: Kết nối với các công cụ như Trello, Asana để quản lý các nhiệm vụ liên quan đến việc tìm việc.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình theo dõi đơn ứng tuyển và chuẩn bị phỏng vấn, tiết kiệm thời gian và tăng cường hiệu suất. Hãy áp dụng ngay để tối ưu hóa quá trình tìm việc của các sếp!