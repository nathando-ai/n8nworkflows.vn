---
title: "🚀 Tự động hóa xử lý hóa đơn PDF với Claude AI và tạo Vendor Bill trong Odoo 18"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động đọc hóa đơn PDF bằng Claude AI, kiểm tra trùng lặp và tạo hóa đơn nhà cung cấp (Vendor Bill) nháp trong Odoo 18."
slug: "tu-dong-hoa-xu-ly-hoa-don-pdf-claude-ai-odoo-18"
tags: [n8n, automation, odoo, claude-ai, ai-extraction, invoice-processing]
keywords: [n8n workflow, odoo 18, claude ai invoice, tự động hóa hóa đơn, trích xuất pdf ai]
---

# 🚀 Tự động hóa xử lý hóa đơn PDF với Claude AI và tạo Vendor Bill trong Odoo 18

Các sếp trong bộ phận kế toán hoặc quản trị doanh nghiệp chắc chắn đã quá quen thuộc với nỗi đau: Mỗi tháng phải nhận hàng trăm hóa đơn PDF gửi đến, ngồi đọc từng con số, tra cứu nhà cung cấp trên hệ thống ERP, rồi gõ thủ công từng dòng vào phần mềm. Công việc nhàm chán này vừa tốn thời gian, vừa dễ dẫn đến sai sót số liệu hoặc nhập trùng hóa đơn.

Workflow n8n chuyên nghiệp được chia sẻ bởi chuyên gia Florian Eiche sẽ giải quyết triệt để vấn đề này. Hệ thống sẽ tự động hóa 100% quy trình: nhận file PDF, nhờ **Claude AI** bóc tách dữ liệu thông minh, kiểm tra trùng lặp, tự động tìm/tạo nhà cung cấp và tạo bản nháp hóa đơn (**Draft Vendor Bill**) ngay trên **Odoo 18** mà các sếp không cần tốn một thao tác thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian nhập liệu:** Không còn phải gõ tay số hóa đơn, ngày tháng, tiền thuế hay tên nhà cung cấp.
- **Độ chính xác tuyệt vời:** Sức mạnh của Claude AI giúp đọc chuẩn xác ngay cả với các mẫu hóa đơn phức tạp.
- **Kiểm soát thông minh:** Tự động phát hiện hóa đơn trùng lặp dựa trên số hóa đơn, tránh việc thanh toán 2 lần.
- **An toàn dữ liệu:** Hóa đơn được tạo ở trạng thái **Draft (Nháp)** trên Odoo 18, giúp kế toán dễ dàng kiểm tra lại trước khi phê duyệt chính thức.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Hệ thống Odoo 18:** Đã cài sẵn module Invoicing và bật quyền truy cập API.
- **Anthropic API Key:** Tài khoản Anthropic để gọi Claude AI (khuyên dùng Claude Sonnet 4.5).
- **n8n Instance:** Phiên bản n8n 2.x trở lên (Cloud hoặc Self-hosted).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ JSON từ n8n template gốc.
- Mở n8n Editor, chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 24 nodes được tổ chức khoa học. Các sếp cần tập trung cấu hình kỹ các điểm sau:
- **Node `Configuration` (Set):** Điền chính xác đường dẫn URL Odoo của doanh nghiệp (`Odoo URL`), tên database (`Database`), tài khoản đăng nhập và mật khẩu/API key. Tại đây các sếp cũng có thể tùy chỉnh model Claude AI muốn sử dụng.
- **Node `Claude AI Extract` (HTTP Request):** Cần cấu hình **Credentials** loại *HTTP Header Auth* với tên `Anthropic API Key`, header name là `x-api-key` và giá trị là API key của các sếp.
- **Node `Receive Invoice PDF` (Webhook):** Lấy URL webhook để tích hợp hệ thống gửi file PDF (ví dụ gửi qua cURL, Gmail trigger hoặc ứng dụng nội bộ).
  *Test nhanh qua cURL:*
  ```bash
  curl -X POST https://your-n8n-instance.com/webhook/invoice-process -F "data=@invoice.pdf"
  ```

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Execute Workflow) với một file PDF hóa đơn mẫu để kiểm tra toàn bộ luồng từ AI trích xuất đến khi tạo thành công hóa đơn nháp trong Odoo.
- Sau khi test thành công, bật công tắc **Active** để hệ thống tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Email Trợ lý:** Thay vì nhận file qua Webhook, các sếp có thể đổi node đầu vào thành **Email Read (IMAP)** để n8n tự động bắt các email có đính kèm hóa đơn gửi đến kế toán.
- **Lưu trữ file thông minh:** Thêm node Google Drive, S3 hoặc WebDAV ngay sau bước tạo hóa đơn để lưu trữ file PDF gốc vào đúng thư mục của nhà cung cấp.
- **Thông báo qua Telegram/Slack:** Thêm một node nhắn tin để bắn thông báo về nhóm chat mỗi khi có một hóa đơn mới được bóc tách và đưa vào Odoo thành công.

:::note[Lưu ý về bảo mật dữ liệu]
Workflow này gửi tài liệu PDF lên Anthropic API để xử lý. Các sếp hãy đảm bảo đã ký thỏa thuận xử lý dữ liệu (DPA) với Anthropic và tuân thủ các quy định bảo mật dữ liệu tại địa phương (như GDPR) khi xử lý hóa đơn chứa thông tin cá nhân.
:::

### 📌 Kết luận
Tự động hóa quy trình xử lý hóa đơn đầu vào với n8n và Claude AI là bước tiến lớn giúp doanh nghiệp tối ưu hóa bộ máy kế toán, giảm thiểu sai sót và tăng tốc độ xử lý tài chính. Hãy áp dụng ngay vào hệ thống Odoo 18 của các sếp để cảm nhận sự khác biệt!