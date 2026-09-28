---
title: "🚀 Tự động tạo hóa đơn PDF chuyên nghiệp từ Airtable và Google Sheets với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa toàn bộ quy trình xuất hóa đơn PDF có danh mục sản phẩm/dịch vụ (line items) từ Airtable và Google Sheets mà không cần viết code."
slug: "tu-dong-tao-hoa-don-pdf-tu-airtable-google-sheets-n8n"
tags: [n8n, automation, airtable, google-sheets, invoice-processing]
keywords: [n8n workflow, tự động hóa hóa đơn, tạo invoice pdf tự động, airtable google sheets n8n]
---

# 🚀 Tự động tạo hóa đơn PDF chuyên nghiệp từ Airtable và Google Sheets

Các sếp có đang cảm thấy mệt mỏi mỗi cuối tháng khi phải ngồi copy/paste thông tin khách hàng, tính toán từng dòng dịch vụ (line items), thủ công tạo hóa đơn PDF và đồng bộ ngược lại vào CRM không? Việc này không chỉ tốn hàng giờ đồng hồ mà còn rất dễ xảy ra sai sót số liệu.

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ (được thiết kế bởi chuyên gia Sergio Medina). Workflow này giúp tự động hóa 100% quy trình từ khâu nhận dữ liệu qua **Webhook**, bóc tách danh mục dịch vụ, lưu vào **Airtable**, nhân bản template trên **Google Sheets/Drive** để xuất ra hóa đơn PDF hoàn chỉnh và đồng bộ ngược về CRM. Toàn bộ diễn ra hoàn toàn tự động mà không cần can thiệp thủ công!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Biến dữ liệu JSON đầu vào thành một hóa đơn PDF chuyên nghiệp chỉ trong tích tắc.
- **Hỗ trợ danh mục chi tiết (Line Items):** Xử lý mượt mà danh sách nhiều dịch vụ/sản phẩm khác nhau trong cùng một hóa đơn mà không bị rối số liệu.
- **Đồng bộ CRM thông minh:** Tự động lưu thông tin hóa đơn, liên kết khách hàng trên Airtable và lưu file PDF trực tiếp lên Google Drive.
- **Loại bỏ sai sót thủ công:** Đảm bảo mã hóa đơn được đánh số tuần tự chính xác, tính toán tổng tiền chuẩn xác 100%.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Airtable:** Đã chuẩn bị sẵn Base với 3 bảng: *Clients*, *Invoices*, và *Services* (có thể tham khảo mẫu [Airtable Template tại đây](https://airtable.com/appUL5P7KN2Kqsgsf/shr5vCMwg2o4Z5wZI)).
- **Tài khoản Google Drive / Google Sheets:** Chuẩn bị sẵn một file Template Google Sheets chứa các placeholder như `{{clientName}}` (tham khảo [Google Sheets Template tại đây](https://docs.google.com/spreadsheets/d/1XF9vcbsgYqDDgQwBn4RNtnzCkBjbk3jmKU7MBgIXtbo/edit?usp=sharing)).
- **Credentials:** Kết nối tài khoản Airtable và Google Drive vào n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này, sau đó vào n8n Editor chọn **Add from JSON** và dán vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 15 nodes được chia thành các nhóm xử lý logic rõ ràng. Các sếp cần chú ý cấu hình các node sau:

- **Webhook:** Cấu hình đường dẫn endpoint (`path`) và phương thức `POST`. Đây là nơi nhận payload JSON từ hệ thống frontend/CRM của các sếp (cần gửi kèm `clientId` và mảng `services`).
- **Get Client Info & Airtable Nodes (`Create a record1`, `Add Service to DB`, `Get Previous Invoices`, `Update record`...):** Chọn đúng credentials Airtable của các sếp, sau đó map lại đúng Base ID và Table ID cho 3 bảng: *Clients*, *Invoices*, và *Services*.
- **Split Services & Formatting Data (Code Node):** Node `Split Services` (`splitOut`) sẽ bóc tách mảng dịch vụ thành các dòng đơn lẻ, sau đó node `Formatting Data` (`code`) sẽ chuẩn hóa cấu trúc dữ liệu để chuẩn bị đẩy vào database.
- **Generate Invoice # (Code Node):** Node này tính toán và sinh mã hóa đơn tự động dựa trên danh sách hóa đơn cũ lấy từ Airtable (`Get Previous Invoices`).
- **Copy Invoice Template (Google Drive):** Cấu hình để hệ thống nhân bản file Google Sheets mẫu thành một file hóa đơn mới cho khách hàng.
- **HTTP Request Nodes (`Add Services to Invoice`, `Add Client Info`, `Add Invoice Summary Info`):** Dùng để gọi API chèn chi tiết dịch vụ, thông tin khách hàng và tổng kết hóa đơn trực tiếp vào file Google Sheets mới tạo.
- **Share file (Google Drive):** Cấu hình quyền chia sẻ file (ví dụ: Anyone with the link can view) để tạo ra đường dẫn tải PDF công cộng.

#### 3. Kích hoạt ⚡️
- Gửi một lượng dữ liệu mẫu (JSON payload) qua Webhook bằng Postman hoặc cURL để **Test run** toàn bộ workflow.
- Kiểm tra lại kết quả trên Airtable và Google Drive xem hóa đơn đã được tạo và điền đúng số liệu chưa.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để hệ thống chính thức vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để gửi thông báo tức thì về team kế toán mỗi khi có hóa đơn mới được tạo thành công.
- **Tự động gửi Email:** Kết hợp thêm node Gmail hoặc Resend để tự động gửi trực tiếp file PDF hóa đơn đến email của khách hàng ngay sau khi tạo xong.
- **Lưu Log lỗi:** Sử dụng nhánh Error Trigger để bắt các lỗi phát sinh (ví dụ: thiếu thông tin khách hàng, lỗi kết nối Airtable) và gửi cảnh báo về kênh chat nội bộ của doanh nghiệp.

### 📌 Kết luận
Workflow tự động hóa tạo hóa đơn PDF từ Airtable và Google Sheets này là mảnh ghép hoàn hảo giúp tối ưu hóa quy trình tài chính - bán hàng, tiết kiệm hàng chục giờ làm việc thủ công mỗi tháng cho doanh nghiệp. Hãy áp dụng ngay hôm nay để nâng tầm chuyên nghiệp cho hệ thống vận hành của các sếp!