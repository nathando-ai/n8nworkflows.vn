---
title: "🚀 Tự động trích xuất hóa đơn PDF từ JotForm bằng AI GPT-4o-mini và Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động nhận hóa đơn PDF từ JotForm, dùng GPT-4o-mini trích xuất dữ liệu có cấu trúc và lưu vào Google Sheets 100% tự động."
slug: "trich-xuat-hoa-don-jotform-ai-google-sheets"
tags: [n8n, automation, no-code, ai, openai, google-sheets, jotform]
keywords: [n8n workflow, trích xuất hóa đơn pdf, ai extraction gpt, jotform n8n, google sheets automation]
---

# 🚀 Tự động trích xuất hóa đơn PDF từ JotForm bằng AI GPT-4o-mini và Google Sheets

Các sếp có đang mệt mỏi với việc thủ công mở từng file PDF hóa đơn gửi về từ JotForm, căng mắt đọc từng dòng để gõ lại số tiền, tên công ty, danh sách mặt hàng vào file Excel hay Google Sheets? Việc này vừa tốn thời gian, dễ gây nhầm lẫn số liệu, lại chẳng đem lại giá trị gia tăng nào cho doanh nghiệp.

Đừng lo nữa, bài toán này sẽ được giải quyết triệt để với **workflow n8n tự động hóa 100% không cần code** dưới đây. Workflow này sẽ tự động bắt dữ liệu từ JotForm, dùng sức mạnh của AI (OpenAI GPT-4o-mini kết hợp LangChain) để đọc hiểu file PDF hóa đơn, trích xuất thành các trường dữ liệu có cấu trúc chuẩn chỉnh và tự động ghi nhận vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần con người can thiệp từ khâu nhận hóa đơn đến lúc lưu trữ dữ liệu.
- **Độ chính xác cao:** Ứng dụng AI thông minh (GPT-4o-mini) để bóc tách chính xác mã hóa đơn, tên khách hàng, chi tiết sản phẩm và tổng tiền kể cả khi layout hóa đơn thay đổi.
- **Đồng bộ thời gian thực:** Dữ liệu tự động đẩy thẳng lên Google Sheets giúp việc tra cứu, làm báo cáo tài chính trở nên tức thì.
- **Lưu trữ an toàn:** Tự động lưu bản sao file JSON cấu trúc và file hóa đơn xuống ổ đĩa hệ thống.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản OpenAI:** API Key có hạn mức để sử dụng model GPT-4o-mini.
- **Tài khoản Google:** Để cấu hình kết nối Google Sheets (Google OAuth2).
- **JotForm Account:** Form thu thập hóa đơn có tích hợp Webhook.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, sau đó vào giao diện n8n Editor, chọn **Import from JSON** và dán vào để hệ thống tự động sinh ra toàn bộ 13 nodes bao gồm: *Webhook, Download Invoice, Extract from File, OpenAI Chat Models, Information Extractor, Google Sheets...*

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không gặp lỗi "lệnh không tìm thấy" hay "lỗi xác thực", các sếp cần cấu hình chính xác các node sau:

- **Node Webhook:** 
  - Lấy đường dẫn URL (Webhook URL) được cung cấp và gắn vào cấu hình Webhook/Integration bên phía JotForm để gửi dữ liệu hóa đơn dạng PDF về n8n.
- **Node Download Invoice:** 
  - Cấu hình phương thức HTTP Request để tải file PDF hóa đơn từ đường dẫn nhận được trong payload của JotForm. Kiểm tra lại thông tin xác thực (`httpBearerAuth` hoặc `httpHeaderAuth`) nếu JotForm yêu cầu quyền truy cập file bảo mật.
- **Các Node OpenAI (`OpenAI Chat Model for Structured Data`, `OpenAI Chat Model for Output Parser`,...):**
  - Chọn credential OpenAI API đã chuẩn bị sẵn.
  - Đảm bảo model được chọn là `gpt-4.1-mini` (hoặc `gpt-4o-mini` tùy phiên bản hệ thống cập nhật).
- **Node Formatted Structured Data Extract & Structured Output Parser:**
  - Kiểm tra schema JSON định nghĩa các trường dữ liệu cần trích xuất (Ví dụ: Mã hóa đơn `invoice_id`, tên công ty `company`, khách hàng `client`, danh sách mặt hàng `items`, tổng tiền `total_amount`...) để AI bóc tách đúng yêu cầu.
- **Node Append or update row in sheet (Google Sheets):**
  - Kết nối tài khoản Google Sheets qua OAuth2.
  - Chọn file Google Sheets đích và Sheet Name cụ thể, sau đó map các trường dữ liệu AI vừa trích xuất tương ứng với các cột trong Sheet.
- **Các Node Write File (`Write File from Disk...`):**
  - Đảm bảo thư mục lưu trữ file trên ổ đĩa của server n8n có quyền ghi (Read/Write Permission) để tránh lỗi không lưu được file JSON/PDF.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thực hiện một lượt submit thử nghiệm trên JotForm để test luồng chạy dữ liệu.
- Kiểm tra kết quả trên Google Sheets xem dòng dữ liệu đã được thêm vào chính xác chưa.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để workflow chính thức túc trực 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack vào cuối luồng để gửi thông báo tức thời về điện thoại mỗi khi có hóa đơn mới được xử lý thành công.
- **Báo cáo định kỳ:** Kết hợp thêm node Schedule Trigger để gom nhóm dữ liệu trong Google Sheets và gửi email tổng kết doanh thu cuối ngày cho sếp lớn.
- **Xử lý ngoại lệ (Error Handling):** Thêm Error Trigger để nếu file PDF bị lỗi font hoặc AI không đọc được, hệ thống sẽ tự động bắn tin nhắn cảnh báo để kiểm tra lại.

### 📌 Kết luận
Việc tự động hóa quy trình nhập liệu hóa đơn từ JotForm lên Google Sheets bằng AI không chỉ giúp doanh nghiệp tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần mà còn loại bỏ hoàn toàn sai sót do con người. Chúc các sếp cài đặt thành công và tối ưu hóa vận hành doanh nghiệp của mình!