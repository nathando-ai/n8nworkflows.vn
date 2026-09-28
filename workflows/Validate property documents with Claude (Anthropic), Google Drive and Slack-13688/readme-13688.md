---
title: "🏡 [Tự động hóa 100% không code] Kiểm tra hợp lệ tài liệu bất động sản với Claude AI, Google Drive và Slack"
description: "Giải pháp tự động hóa hoàn chỉnh cho việc kiểm tra hợp lệ tài liệu bất động sản. Tiết kiệm thời gian, đảm bảo tuân thủ pháp luật và nâng cao hiệu quả làm việc."
slug: "tu-dong-hoa-kiem-tra-tai-lieu-bat-dong-san-voi-claude-ai-google-drive-slack"
tags: [n8n, automation, no-code, bất động sản, pháp lý, AI]
keywords: [n8n workflow, tự động hóa bất động sản, kiểm tra tài liệu pháp lý, Claude AI, Google Drive, Slack]
---

# 🏡 [Tự động hóa 100% không code] Kiểm tra hợp lệ tài liệu bất động sản với Claude AI, Google Drive và Slack

[Các sếp đang làm thủ công việc kiểm tra hàng trăm tài liệu bất động sản mỗi ngày? Bạn mệt mỏi với việc phải kiểm tra từng giấy tờ, so sánh với quy định pháp luật và gửi báo cáo thủ công? Hãy để workflow này giúp bạn tự động hóa toàn bộ quy trình này chỉ trong vài bước đơn giản.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Xử lý hàng trăm tài liệu mỗi ngày chỉ trong vài phút.
- **Đảm bảo tuân thủ pháp luật**: Kiểm tra tự động với AI theo quy định pháp lý của từng khu vực.
- **Nâng cao hiệu quả làm việc**: Giảm thiểu lỗi con người và tăng tính chính xác.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công sau khi cài đặt.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive để lưu trữ và theo dõi tài liệu.
- Tài khoản Anthropic để sử dụng mô hình AI Claude.
- Tài khoản Slack để nhận thông báo về các vấn đề pháp lý.
- Tài khoản email (SMTP) để gửi báo cáo cho người gửi.
- Tài khoản Google Sheets để lưu trữ nhật ký tuân thủ.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấp vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/13688](https://n8n.io/workflows/13688).
3. Hoặc tải file JSON về và import từ máy tính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Receive Document Submission"**: Cấu hình webhook với path là `validate-property-documents` và phương thức HTTP là POST.
- **Node "Watch Drive Intake Folder"**: Cấu hình credentials Google Drive và chỉ định thư mục để theo dõi.
- **Node "Claude AI Model"**: Cấu hình credentials Anthropic và chọn mô hình `claude-sonnet-4-20250514`.
- **Node "Email Validation Report to Submitter"**: Cấu hình credentials SMTP để gửi email báo cáo.
- **Node "Alert Legal Team on Slack"**: Cấu hình credentials Slack để gửi thông báo.
- **Node "Write Compliance Audit Record"**: Cấu hình credentials Google Sheets và chỉ định bảng tính và phạm vi để ghi nhật ký tuân thủ.

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Bật chế độ Active cho workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack**: Thêm node Slack để thông báo cho nhóm pháp lý về các vấn đề nghiêm trọng.
- **Lưu log**: Sử dụng Google Sheets để theo dõi tất cả các trường hợp kiểm tra và kết quả.
- **Gửi báo cáo định kỳ**: Tự động gửi báo cáo hàng tuần cho quản lý về các trường hợp không tuân thủ.
- **Kết nối với các hệ thống khác**: Kết nối với các hệ thống CRM hoặc ERP để cập nhật trạng thái của các trường hợp bất động sản.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình kiểm tra tài liệu bất động sản, đảm bảo tuân thủ pháp luật và tiết kiệm thời gian. Hãy áp dụng ngay để nâng cao hiệu quả làm việc và giảm thiểu rủi ro pháp lý.