---
title: "🚀 Tự động hóa xử lý hóa đơn email từ Gmail, trích xuất dữ liệu bằng GPT-4 và lưu vào Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n thông minh giúp lọc email tài chính, trích xuất hóa đơn bằng AI Agent và lưu tự động vào Google Sheets, tiết kiệm 90% thời gian kế toán."
slug: "tu-dong-hoa-xu-ly-hoa-don-email-gmail-gpt-4-google-sheets"
tags: [n8n, automation, no-code, openai, google-sheets, gmail, ai-agent]
keywords: [n8n workflow, xử lý hóa đơn tự động, gpt-4o mini, gmail to google sheets, ai OCR hóa đơn, tự động hóa kế toán]
---

# 🚀 Tự động hóa xử lý hóa đơn email từ Gmail, trích xuất dữ liệu bằng GPT-4 và lưu vào Google Sheets

Các sếp có đang đau đầu mỗi khi cuối tháng phải rà soát hàng trăm email hóa đơn, biên nhận (receipt), chứng từ tài chính từ các nhà cung cấp khác nhau? Việc copy/paste thủ công vào file Excel/Google Sheets không chỉ tốn hàng giờ đồng hồ mà còn dễ xảy ra sai sót, nhầm lẫn số tiền hay mã hóa đơn.

Workflow **Inbox2Ledger** này chính là "vũ khí tối thượng" giúp các sếp biến hộp thư rộn ràng thành một sổ cái tài chính sạch sẽ, chuẩn chỉnh 100% tự động nhờ sức mạnh của AI và n8n!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Gom toàn bộ hóa đơn từ Gmail, phân loại thông minh bằng AI Guardrails, không bỏ sót chứng từ nào.
- **Trích xuất chuẩn xác:** Sử dụng AI Agent kết hợp GPT-4o-mini để bóc tách thông tin (Nhà cung cấp, Ngày, Mã hóa đơn, Số tiền, Tiền tệ, Danh mục).
- **Kiểm tra & Xác thực tự động:** Kiểm tra lỗi, chuẩn hóa định dạng dữ liệu và tạo mã định danh (Case ID) độc nhất cho từng giao dịch.
- **Lưu trữ trực quan:** Đổ thẳng dữ liệu sạch vào Google Sheets sẵn sàng cho bộ phận kế toán hoặc các bước tự động hóa tiếp theo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Gmail** (Cấu hình OAuth2 để n8n đọc email).
- **Google Sheets** (Chuẩn bị sẵn file Google Sheet để ghi dữ liệu log hóa đơn).
- **OpenAI API Key** (Sử dụng cho các mô hình GPT-4o-mini / GPT-4.1 để xử lý ngôn ngữ tự nhiên và OCR).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp tiến hành copy mã JSON của workflow hoặc import file JSON trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các node quan trọng sau đây:

- **`Enter Date till which you want email to be fetched` (Form Trigger):** Node này dùng để khởi động workflow bằng cách chọn mốc thời gian fetch email. Các sếp có thể thay thế bằng Schedule Trigger nếu muốn chạy tự động theo lịch định kỳ.
- **`Get Email Content` (Gmail):** Kết nối tài khoản Gmail của các sếp (chọn credential `gmailOAuth2`), cấu hình thư mục cần quét (Inbox hoặc nhãn dán cụ thể).
- **`Guardrail: Is Finance?` & `Filter Finance Keywords`:** Bộ lọc thông minh giúp loại bỏ các email rác, quảng cáo và chỉ giữ lại các email liên quan đến tài chính, hóa đơn, thanh toán.
- **`gpt 4o mini` & `OpenAI Chat Model` (LM Chat OpenAI):** Cấu hình `openAiApi` credentials với API Key của OpenAI. Các node này cung cấp “bộ não” cho AI Agent.
- **`AI Agent (Email OCR)`:** Đóng vai trò đọc nội dung email/hóa đơn, trích xuất các trường thông tin dạng JSON (Vendor, Date, Invoice ID, Amount...).
- **`Validate Extraction` & `Apply Finance Rules` (Code):** Các node xử lý code JavaScript có sẵn giúp kiểm tra định dạng dữ liệu, bắt lỗi và phân loại danh mục chi phí (GL Categories), sinh Case ID.
- **`Log to Invoices Sheet` (Google Sheets):** Kết nối tài khoản Google Sheets (`googleSheetsOAuth2Api`), chọn đúng file Spreadsheet và Sheet Name để hệ thống tự động append (thêm dòng mới) các hóa đơn đã được xử lý sạch sẽ.

#### 3. Kích hoạt ⚡️
- Chạy thử một bản ghi (Test run) bằng cách submit form hoặc test thủ công một email hóa đơn mẫu.
- Kiểm tra kết quả trả về trong Google Sheets xem dữ liệu đã khớp chưa.
- Bật công tắc **Active** để workflow hoạt động tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram/Slack:** Thêm node gửi tin nhắn tức thì vào nhóm chat của phòng kế toán mỗi khi có một hóa đơn giá trị lớn được ghi nhận thành công.
- **Cảnh báo lỗi (Error Trigger):** Thiết lập nhánh bắt lỗi nếu AI Agent không đọc được hóa đơn, gửi thông báo về email quản lý để xử lý thủ công.
- **Lưu trữ file đính kèm:** Mở rộng workflow bằng cách tải các file PDF/hình ảnh hóa đơn từ Gmail lưu trực tiếp lên Google Drive kèm theo link trong Google Sheets.

### 📌 Kết luận
Với workflow **Inbox2Ledger**, việc xử lý hóa đơn giấy tờ hay email thủ công chỉ còn là dĩ vãng. Hãy cài đặt ngay hôm nay để tối ưu hóa quy trình tài chính - kế toán của doanh nghiệp các sếp!