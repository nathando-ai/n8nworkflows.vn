---
title: "🚀 Tự động trích xuất hóa đơn từ Gmail vào Airtable bằng Mistral OCR và GPT-4.1-mini"
description: "Xây dựng hệ thống tự động xử lý hóa đơn đến từ Gmail, trích xuất dữ liệu thông minh bằng Mistral OCR kết hợp GPT-4.1-mini và lưu trữ an toàn vào Airtable mà không cần thao tác thủ công."
slug: "tu-dong-trich-xuat-hoa-don-gmail-airtable-mistral-gpt"
tags: [n8n, automation, no-code, invoice-processing, airtable, gpt-4, mistral-ai]
keywords: [n8n workflow, tự động hóa hóa đơn, trích xuất hóa đơn gmail airtable, mistral ocr, gpt-4.1-mini n8n]
---

# 🚀 Tự động trích xuất hóa đơn từ Gmail vào Airtable với Mistral OCR và GPT-4.1-mini

Các sếp có đang cảm thấy mệt mỏi mỗi cuối tháng khi phải ngồi "bới tung" hòm thư Gmail, tải từng file PDF/ảnh hóa đơn, đọc thủ công các con số rồi cặm cụi gõ lại vào Airtable hay Excel? Công việc nhàm chán này không chỉ ngốn hàng giờ đồng hồ quý giá mà còn cực kỳ dễ xảy ra sai sót (như nhầm tiền, lệch mã hóa đơn, trùng lặp dữ liệu).

Đừng lo, giải pháp ở đây rồi! Workflow n8n siêu việt này sẽ thay các sếp làm toàn bộ quy trình từ **A đến Z**: tự động bắt email có hóa đơn, đẩy qua AI đọc hiểu, kiểm tra trùng lặp và lưu trữ gọn gàng vào Airtable. 100% tự động, không cần đụng tay!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh copy-paste thủ công hàng trăm hóa đơn mỗi tháng.
- **Độ chính xác tuyệt đối:** Ứng dụng sức mạnh của Mistral OCR và GPT-4.1-mini giúp đọc chuẩn xác các thông tin phức tạp trên hóa đơn.
- **Chống trùng lặp thông minh:** Tự động quét và ngăn chặn việc lưu lại hóa đơn đã từng được xử lý trước đó.
- **Vận hành 24/7:** Email vừa đến là hệ thống xử lý ngay lập tức, có cơ chế bắt lỗi và gửi email thông báo nếu dữ liệu không hợp lệ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow này "lên đồ" mượt mà, các sếp cần chuẩn bị sẵn các tài khoản sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Gmail** (để cấu hình Trigger nhận email và gửi email cảnh báo lỗi).
- **Tài khoản Airtable** kèm theo Base quản lý hóa đơn.
- **ImgBB API Key** (dùng cho HTTP Request node `host image` để tạo public URL cho file ảnh/hóa đơn).
- **Mistral AI API Key** (cho node `Extract text`).
- **OpenAI API Key** (cho node `OpenAI Chat Model` sử dụng GPT-4.1-mini).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, vào giao diện n8n chọn **New Workflow**, nhấn tổ hợp `Ctrl + V` (hoặc `Cmd + V`) để dán toàn bộ các nodes lên màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 16 nodes được thiết kế mạch lạc, các sếp cần chú ý cấu hình các node cốt lõi sau:

- **Gmail Trigger:** Kết nối tài khoản Gmail của các sếp qua `gmailOAuth2`. Đảm bảo bật tính năng tải tệp đính kèm (attachments) trong cài đặt node để hệ thống bắt được file hóa đơn.
- **host image (HTTP Request):** Node này dùng để đẩy file ảnh hóa đơn lên dịch vụ lưu trữ (ví dụ ImgBB) nhằm lấy một đường dẫn (public URL) phục vụ cho việc đọc OCR. Các sếp cần điền API Key của dịch vụ ảnh vào mục credentials tương ứng.
- **Extract text (Mistral AI):** Kết nối `mistralCloudApi`. Node này chịu trách nhiệm bóc tách toàn bộ chữ viết thô từ hình ảnh hóa đơn.
- **OpenAI Chat Model & Analyze Invoices (Agent):** Chọn model `gpt-4.1-mini` và kết nối `openAiApi`. Node AI này cùng với **Structured Output Parser** sẽ chuyển đổi văn bản thô từ OCR thành các trường dữ liệu gọn gàng (Tên nhà cung cấp, Tổng tiền, Ngày tháng, Mã hóa đơn...).
- **Search Existing Invoices & upload invoice & details (Airtable):** Kết nối `airtableTokenApi`. Các sếp trỏ đúng đến Base quản lý hóa đơn của mình (Base mẫu tham khảo từ tác giả: `appU9XzFqL5Aovj2M/shrnanmtZpUgbVsEo`). Node **Check for Duplicates (Switch)** sẽ dựa vào kết quả tìm kiếm này để chặn hóa đơn trùng.
- **Send Error Email (Gmail):** Cấu hình nếu dữ liệu hóa đơn không hợp lệ (`Validate Data` qua `If` node), hệ thống sẽ kích hoạt `Invalid Data Handler` và tự động gửi email cảnh báo cho quản lý.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một email thử nghiệm có đính kèm file hóa đơn vào Gmail để kiểm tra luồng dữ liệu.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động hoạt động ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh chat:** Thay vì chỉ gửi email báo lỗi, các sếp có thể đổi node `Send Error Email` thành **Telegram** hoặc **Slack** để nhận thông báo tức thời ngay trên điện thoại khi có lỗi xảy ra.
- **Mở rộng lưu trữ:** Có thể bổ sung thêm bước đồng bộ dữ liệu sang Google Sheets hoặc phần mềm kế toán nếu doanh nghiệp dùng đa nền tảng.
- **Gắn nhãn Gmail (Label):** Sau khi xử lý xong, có thể thêm một node Gmail để tự động đánh dấu nhãn "Processed" nhằm dễ dàng quản lý hòm thư.

### 📌 Kết luận
Xử lý hóa đơn thủ công đã là chuyện của quá khứ. Với sự kết hợp hoàn hảo giữa Gmail, Mistral OCR, GPT-4.1-mini và Airtable, các sếp đã có trong tay một trợ lý tự động hóa đắc lực, vừa tiết kiệm thời gian, vừa tối ưu chi phí vận hành. Triển khai ngay thôi nào!