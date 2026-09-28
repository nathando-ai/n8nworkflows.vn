---
title: "🚀 Tự động trích xuất hóa đơn PDF thành JSON cấu trúc bằng Mistral OCR và AI trong n8n"
description: "Hướng dẫn chi tiết xây dựng workflow n8n tự động hóa quy trình xử lý hóa đơn PDF/hình ảnh bằng Mistral OCR và LLM, trả về dữ liệu JSON chuẩn xác."
slug: "tu-dong-trich-xuat-hoa-don-pdf-thanh-json-mistral-ocr-n8n"
tags: [n8n, automation, no-code, mistral-ai, ocr, invoice-processing]
keywords: [n8n workflow, trích xuất hóa đơn, mistral ocr, ai llm json, tự động hóa kế toán]
useHeader: true
---

# 🚀 Tự động trích xuất hóa đơn PDF thành JSON cấu trúc bằng Mistral OCR và AI

Các sếp kế toán hoặc vận hành chắc chắn đã quá ngán ngẩm cảnh phải đọc từng file hóa đơn PDF, tra cứu thủ công rồi gõ lại từng con số, tên công ty, tiền thuế vào Excel hay hệ thống phần mềm. Vừa tốn thời gian, dễ nhầm lẫn, lại cực kỳ căng thẳng vào mỗi kỳ quyết toán.

Bài toán này sẽ được giải quyết triệt để 100% không cần code với một workflow n8n cực kỳ thông minh: nhận file PDF/hình ảnh hóa đơn qua Webhook, sử dụng **Mistral OCR** để đọc chữ cực nét, kết hợp với sức mạnh của **LLM** để bóc tách thành một cấu trúc JSON hoàn chỉnh, đồng thời tự động kiểm tra độ tin cậy (`Confidence >= 0.5`) để phân luồng xử lý tự động hoặc cần review lại!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Nhận file đầu vào, xử lý qua OCR và AI rồi trả về kết quả JSON ngay lập tức mà không cần con người can thiệp.
- **Độ chính xác cao:** Ứng dụng công nghệ OCR tiên tiến từ Mistral AI kết hợp LLM giúp hiểu ngữ cảnh hóa đơn cực tốt, kể cả các hóa đơn phức tạp.
- **Kiểm soát thông minh:** Tự động phân loại trạng thái (`ok` hoặc `review_needed`) dựa trên mức độ tin cậy, giúp hạn chế rủi ro sai sót dữ liệu.
- **Tích hợp linh hoạt:** Dễ dàng kết nối API trả về kết quả JSON cho các hệ thống ERP, CRM hoặc phần mềm kế toán sẵn có của doanh nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động (Self-hosted hoặc n8n Cloud).
- **Mistral AI API Key** (dùng cho node *Mistral OCR* và có thể dùng cho LLM).
- **OpenAI API Key** hoặc API key của LLM tương đương (dùng cho node *LLM Extract JSON*).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã nguồn JSON của workflow hoặc tải file JSON về, sau đó vào giao diện n8n chọn **Add workflow** -> Dấu ba chấm (...) -> **Import from File / Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 8 nodes chính xử lý từ khâu nhận file đến trả kết quả:
- **Webhook**: Lắng nghe yêu cầu POST tại đường dẫn `/webhook/ocr-to-json`. File PDF hoặc hình ảnh cần được gửi lên qua property dạng binary tên là `data`.
- **Mistral OCR**: Nơi thực hiện quét chữ từ file. Các sếp nhớ tạo và gắn **Mistral AI credentials** vào node này.
- **Normalize OCR Text** (Code node): Xử lý chuẩn hóa định dạng văn bản thô vừa quét được từ OCR.
- **LLM Extract JSON** (HTTP Request node): Gửi text đã chuẩn hóa sang mô hình ngôn ngữ lớn (LLM) để trích xuất ra định dạng JSON theo cấu trúc mong muốn. Các sếp cần cấu hình API key (OpenAI hoặc Mistral) tại đây.
- **Clean JSON** (Code node): Làm sạch dữ liệu JSON, loại bỏ các ký tự thừa để đảm bảo đầu ra sạch sẽ, hợp lệ.
- **Confidence >= 0.5?** (If node): Kiểm tra độ tin cậy của bản trích xuất. 
  - Nếu $\ge 0.5$, chuyển đến **Respond OK** trả về trạng thái `status: ok`.
  - Nếu $< 0.5$, chuyển đến **Respond Review** trả về trạng thái `status: review_needed` để nhân sự kiểm tra lại thủ công.

#### 3. Kích hoạt ⚡️
- Thực hiện một request POST thử nghiệm gửi file hóa đơn mẫu lên endpoint webhook `/webhook/ocr-to-json` để kiểm tra kết quả trả về.
- Sau khi test ngon lành, gạt công tắc **Active** ở góc trên bên phải để workflow chính thức vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu vào Google Sheets / Airtable**: Mở rộng workflow bằng cách thêm node Google Sheets sau bước `Clean JSON` để tự động ghi log mọi hóa đơn đã xử lý thành một bảng quản lý tài chính.
- **Gửi thông báo Telegram/Slack**: Nếu hóa đơn rơi vào trạng thái `review_needed`, hãy bắn một tin nhắn kèm link file PDF vào nhóm Telegram của bộ phận kế toán để họ xử lý ngay lập tức.
- **Mở rộng phạm vi tài liệu**: Ngoài hóa đơn (invoices), các sếp có thể tinh chỉnh prompt trong phần LLM để áp dụng cho phiếu thu chi (receipts), đơn đặt hàng (purchase orders) hoặc các loại biểu mẫu khác.

### 📌 Kết luận
Việc tự động hóa trích xuất dữ liệu hóa đơn bằng AI không chỉ giúp doanh nghiệp tiết kiệm hàng chục giờ nhập liệu thủ công mỗi tháng mà còn loại bỏ triệt để sai sót do con người. Hãy tiến hành "lên đồ" ngay cho hệ thống n8n của các sếp ngày hôm nay!