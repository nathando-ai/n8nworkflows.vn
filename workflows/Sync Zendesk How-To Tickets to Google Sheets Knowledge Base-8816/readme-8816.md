---
title: "🚀 Tự động đồng bộ vé Zendesk 'How-To' vào Google Sheets Knowledge Base"
description: "Hướng dẫn chi tiết cách tự động đồng bộ các vé Zendesk có tag 'how-to' vào Google Sheets để xây dựng cơ sở kiến thức chuyên nghiệp, tiết kiệm thời gian và đảm bảo tính chính xác cao."
slug: "tu-dong-dong-bo-ve-zendesk-how-to-vao-google-sheets"
tags: [n8n, automation, no-code, Zendesk, Google Sheets]
keywords: [n8n workflow, tự động hóa, Zendesk, Google Sheets, cơ sở kiến thức]
---

# 🚀 Tự động đồng bộ vé Zendesk 'How-To' vào Google Sheets Knowledge Base

[Các sếp đang gặp khó khăn khi phải thủ công đồng bộ các vé hỗ trợ từ Zendesk vào Google Sheets để xây dựng cơ sở kiến thức. Quá trình này tốn thời gian, dễ xảy ra lỗi và không thể tự động hóa. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình này một cách hoàn toàn không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động đồng bộ dữ liệu mà không cần can thiệp thủ công.
- Tính chính xác cao: Dữ liệu được xử lý và lưu trữ một cách chuẩn xác.
- Cá nhân hóa: Dễ dàng tùy chỉnh theo nhu cầu cụ thể của doanh nghiệp.
- Hoạt động liên tục: Workflow có thể được lập lịch chạy tự động theo thời gian.
- Theo dõi lỗi: Hệ thống ghi log lỗi chi tiết giúp dễ dàng phát hiện và khắc phục vấn đề.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Zendesk với quyền truy cập API.
- Tài khoản Google với quyền truy cập Google Sheets API.
- Credentials cho cả hai dịch vụ trên trong n8n.
- Google Sheet đã được tạo sẵn với cấu trúc phù hợp để lưu trữ dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của bạn, các sếp có thể làm theo các bước sau:

1. Truy cập vào n8n Editor của bạn.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/8816](https://n8n.io/workflows/8816).
3. Hoặc tải file JSON về và import thủ công qua nút "Import from File".

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **When clicking 'Execute workflow' (manualTrigger)**: Node này cho phép các sếp chạy workflow thủ công. Không cần cấu hình gì thêm.

- **Error Trigger (errorTrigger)**: Node này tự động kích hoạt khi bất kỳ node nào trong workflow gặp lỗi. Không cần cấu hình gì thêm.

- **Filter HowTo Tickets Only (if)**: Node này lọc các vé có tag "howto". Các sếp có thể thay đổi điều kiện lọc nếu cần.

- **Get Requester User Info (zendesk)**: Node này lấy thông tin chi tiết của người yêu cầu vé. Các sếp cần cấu hình credentials cho Zendesk API.

- **Update Knowledge Base Sheet (googleSheets)**: Node này cập nhật dữ liệu vào Google Sheets. Các sếp cần cấu hình credentials cho Google Sheets API và chỉ định ID của Google Sheet và tên của sheet.

- **Fetch All Zendesk Tickets (zendesk)**: Node này lấy tất cả các vé từ Zendesk. Các sếp cần cấu hình credentials cho Zendesk API.

- **Format Error Details (code)**: Node này định dạng thông tin lỗi. Các sếp có thể tùy chỉnh mã JavaScript trong node này để phù hợp với nhu cầu.

- **Log Error to Sheet (googleSheets)**: Node này ghi log lỗi vào Google Sheets. Các sếp cần cấu hình credentials cho Google Sheets API và chỉ định ID của Google Sheet và tên của sheet.

- **Send Error Notification (emailSend)**: Node này gửi thông báo lỗi qua email. Các sếp cần cấu hình credentials cho SMTP và chỉ định địa chỉ email người nhận.

- **Success Summary (code)**: Node này tạo báo cáo tóm tắt khi workflow chạy thành công. Các sếp có thể tùy chỉnh mã JavaScript trong node này để phù hợp với nhu cầu.

- **Log Successful Execution (googleSheets)**: Node này ghi log thành công vào Google Sheets. Các sếp cần cấu hình credentials cho Google Sheets API và chỉ định ID của Google Sheet và tên của sheet.

#### 3. Kích hoạt ⚡️
Sau khi đã cấu hình các node quan trọng, các sếp có thể kích hoạt workflow bằng cách:

1. Nhấn vào nút "Execute workflow" để chạy thử với dữ liệu mẫu.
2. Kiểm tra kết quả trên Google Sheets để đảm bảo dữ liệu được đồng bộ chính xác.
3. Bật chế độ "Active" để workflow chạy tự động theo lịch trình đã thiết lập.

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể kết hợp workflow này với Slack/Teams để nhận thông báo lỗi ngay lập tức.
- Có thể lưu log chi tiết hơn bằng cách thêm các trường dữ liệu khác vào Google Sheets.
- Có thể gửi báo cáo định kỳ về tình trạng đồng bộ dữ liệu qua email hoặc Slack.

### 📌 Kết luận
Workflow này giúp các sếp tự động đồng bộ các vé Zendesk có tag "how-to" vào Google Sheets một cách hiệu quả và đáng tin cậy. Bằng cách áp dụng workflow này, các sếp có thể tiết kiệm thời gian, đảm bảo tính chính xác và tối ưu hóa quy trình làm việc của mình.